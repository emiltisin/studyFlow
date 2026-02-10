# 🏗️ StudyFlow - Архитектура и техническая документация

## 📋 Содержание
1. [Архитектурный обзор](#архитектурный-обзор)
2. [Структура проекта](#структура-проекта)
3. [Модели данных](#модели-данных)
4. [Сервисы](#сервисы)
5. [Экраны и навигация](#экраны-и-навигация)
6. [Конфигурация](#конфигурация)

---

## 🏗️ Архитектурный обзор

### Общая архитектура
```
┌──────────────────────────────────────────────────┐
│              FLUTTER APPLICATION                │
│                (StudyFlow)                      │
└──────────────────────────────────────────────────┘
           ↓
┌──────────────────────────────────────────────────┐
│            PRESENTATION LAYER                   │
│  (Screens, Widgets, Pages)                      │
│  ├─ LoginPage          (Auth)                   │
│  ├─ HomePage           (Dashboard)              │
│  ├─ TaskListPage       (Task Management)        │
│  ├─ TaskCreatePage     (Create/Edit)            │
│  ├─ QuickAddModal      (Quick add modal)        │
│  ├─ CalendarPage       (Calendar view)          │
│  ├─ SubjectsPage       (Subject management)     │
│  ├─ StatisticsPage     (Analytics)              │
│  └─ ExamPrepPage       (Exam prep mode)         │
└──────────────────────────────────────────────────┘
           ↓
┌──────────────────────────────────────────────────┐
│            BUSINESS LOGIC LAYER                 │
│  (Services)                                     │
│  ├─ StorageService     (Hive persistence)       │
│  ├─ ThemeService       (Theme management)       │
│  ├─ ApiService         (REST API ready)         │
│  └─ NotificationService(Notifications)          │
└──────────────────────────────────────────────────┘
           ↓
┌──────────────────────────────────────────────────┐
│            DATA LAYER                           │
│  (Models)                                       │
│  ├─ Task               (Domain model)           │
│  ├─ Subject            (Domain model)           │
│  ├─ StudyStats         (Domain model)           │
│  ├─ TaskHiveModel      (Serialization)          │
│  └─ SubjectHiveModel   (Serialization)          │
└──────────────────────────────────────────────────┘
           ↓
┌──────────────────────────────────────────────────┐
│            STORAGE LAYER                        │
│  ├─ Hive Local Database                         │
│  │  ├─ tasks box                                │
│  │  ├─ subjects box                             │
│  │  └─ theme_settings box                       │
│  └─ (Future: REST API)                          │
└──────────────────────────────────────────────────┘
```

### Технологический стек
```
FRONTEND:
├─ Flutter 3.0+           (UI Framework)
├─ Dart 3.0+              (Programming Language)
├─ Material Design 3      (Design System)
└─ cupertino_icons        (iOS Icons)

STATE MANAGEMENT:
├─ StatefulWidget         (Current)
└─ Provider/Riverpod      (Future option)

LOCAL DATABASE:
├─ Hive 2.2.3            (Local storage)
│  ├─ Boxes for Tasks
│  ├─ Boxes for Subjects
│  └─ Boxes for Settings

NOTIFICATIONS:
├─ flutter_local_notifications 17.0.0

DATES & INTERNATIONALIZATION:
├─ intl 0.19.0           (Date formatting)
└─ Russian locale support

BUILD TOOLS:
├─ pubspec.yaml          (Dependency management)
└─ analysis_options.yaml (Lint rules)
```

---

## 📁 Структура проекта

### Дерево каталогов
```
lib/
├── main.dart                          ← Точка входа приложения
├── app.dart                           ← Класс StudyFlowApp с MaterialApp
│
├── models/                            ← Модели данных
│   ├── task_model.dart               ← Основная модель Task
│   ├── subject_model.dart            ← Модель Subject
│   ├── stats_model.dart              ← Модель StudyStats
│   └── task_hive_model.dart          ← Модели для Hive сериализации
│
├── services/                          ← Бизнес-логика и услуги
│   ├── storage_service.dart          ← Hive DB integration (static)
│   ├── theme_service.dart            ← Theme management (static)
│   ├── api_service.dart              ← REST API endpoints (ready)
│   └── notification_service.dart     ← Push notifications (placeholder)
│
└── features/                          ← Экраны по функциональности
    ├── auth/
    │   └── login_page.dart           ← Login/Onboarding
    │
    └── tasks/
        ├── home_page.dart            ← Dashboard/Home
        ├── task_list_page.dart       ← Task list view
        ├── task_create_page.dart     ← Create new task (full form)
        ├── quick_add_modal.dart      ← Quick add bottom sheet
        ├── calendar_page.dart        ← Calendar view
        ├── subjects_page.dart        ← Subject management
        ├── statistics_page.dart      ← Analytics & stats
        └── exam_prep_page.dart       ← Exam preparation mode

build/                                ← Build artifacts (compiled)
test/                                 ← Unit & widget tests
pubspec.yaml                         ← Dependencies & metadata
analysis_options.yaml                ← Lint configuration
```

---

## 📊 Модели данных

### 1. Task - Основная модель задачи

#### Структура класса
```dart
class Task {
  final String id;              // Уникальный ID
  final String title;           // Название задачи (обязательно)
  final String description;     // Описание (опционально)
  final String subjectId;       // ID предмета (обязательно)
  final DateTime deadline;      // Дата/время дедлайна (обязательно)
  final int priorityIndex;      // 0=Низкий, 1=Средний, 2=Высокий, 3=Срочно
  final int statusIndex;        // 0=Ожидание, 1=В процессе, 2=Выполнено
  final DateTime createdAt;     // Когда создана
  final DateTime? completedAt;  // Когда выполнена (null если не выполнена)
}
```

#### Перечисления (Enums)
```dart
enum TaskPriority {
  low,      // 🟢 Низкий приоритет
  medium,   // 🟡 Средний приоритет
  high,     // 🟠 Высокий приоритет
  urgent    // 🔴 СРОЧНО
}

enum TaskStatus {
  pending,   // ⏳ Ожидание
  inProgress, // ▶️ В процессе
  completed  // ✅ Выполнено
}
```

#### Пример создания Task
```dart
Task task = Task(
  id: 'task_001',
  title: 'Решить задачи по математике',
  description: 'Задачи 1-50 из учебника',
  subjectId: 'math_101',
  deadline: DateTime(2026, 2, 13, 18, 0),
  priorityIndex: 2, // Высокий
  statusIndex: 0,   // Ожидание
  createdAt: DateTime.now(),
  completedAt: null,
);
```

### 2. Subject - Модель предмета

#### Структура класса
```dart
class Subject {
  final String id;                // Уникальный ID
  final String name;              // Название предмета (обязательно)
  final Color color;              // Цвет для визуализации
  final String? teacher;          // Имя преподавателя (опционально)
  final DateTime createdAt;       // Когда добавлен
}
```

#### Встроенные предметы
```dart
static final subjects = [
  Subject(
    id: 'math',
    name: 'Математика',
    color: Color(0xFF6366F1),  // Indigo
    teacher: 'Иван Петрович',
  ),
  Subject(
    id: 'history',
    name: 'История',
    color: Color(0xFFF59E0B),  // Orange
    teacher: 'Мария Ивановна',
  ),
  Subject(
    id: 'english',
    name: 'Английский язык',
    color: Color(0xFF10B981),  // Green
    teacher: 'Виктор Сергеевич',
  ),
  Subject(
    id: 'chemistry',
    name: 'Химия',
    color: Color(0xFF14B8A6),  // Teal
    teacher: 'Инна Ивановна',
  ),
];
```

### 3. StudyStats - Модель статистики

#### Структура класса
```dart
class StudyStats {
  final int totalTasks;         // Всего задач
  final int completedTasks;     // Выполненных
  final int inProgressTasks;    // В процессе
  final int urgentTasks;        // Срочных
  final int tasksThisWeek;      // На эту неделю
  final double progressPercent; // % прогресса
  final DateTime lastUpdated;   // Когда обновлена статистика
}
```

### 4. TaskHiveModel & SubjectHiveModel - Модели для сериализации

#### TaskHiveModel (для Hive)
```dart
class TaskHiveModel {
  final String id;
  final String title;
  final String description;
  final String subjectId;
  final DateTime deadline;
  final int priorityIndex;
  final int statusIndex;
  final DateTime createdAt;
  final DateTime? completedAt;

  // Сериализация в Map
  Map<String, dynamic> toMap() {
    return {
      'id': id,
      'title': title,
      'description': description,
      'subjectId': subjectId,
      'deadline': deadline.toIso8601String(),
      'priorityIndex': priorityIndex,
      'statusIndex': statusIndex,
      'createdAt': createdAt.toIso8601String(),
      'completedAt': completedAt?.toIso8601String(),
    };
  }

  // Десериализация из Map
  factory TaskHiveModel.fromMap(Map<String, dynamic> map) {
    return TaskHiveModel(
      id: map['id'] ?? '',
      title: map['title'] ?? '',
      // ... остальные поля ...
    );
  }
}
```

---

## 🔧 Сервисы

### 1. StorageService - Управление локальной БД

#### Инициализация (main.dart)
```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  
  // Инициализация Hive
  await Hive.initFlutter();
  
  // Инициализация ThemeService
  await ThemeService.init();
  
  // Инициализация StorageService
  await StorageService.init();
  
  runApp(const StudyFlowApp());
}
```

#### API методов
```dart
class StorageService {
  // Инициализация
  static Future<void> init()
  
  // CRUD для задач
  static Future<void> saveTask(Task task)
  static Future<List<Task>> getAllTasks()
  static Future<Task?> getTaskById(String id)
  static Future<List<Task>> getTasksBySubject(String subjectId)
  static Future<void> deleteTask(String id)
  static Future<void> deleteAllTasks()
  
  // CRUD для предметов
  static Future<void> saveSubject(Subject subject)
  static Future<List<Subject>> getAllSubjects()
  static Future<Subject?> getSubjectById(String id)
  static Future<void> deleteSubject(String id)
  
  // Utility
  static Future<void> clearAllData()
}
```

#### Пример использования
```dart
// Сохранить задачу
await StorageService.saveTask(myTask);

// Получить все задачи
List<Task> allTasks = await StorageService.getAllTasks();

// Получить задачи по предмету
List<Task> mathTasks = await StorageService
  .getTasksBySubject('math');

// Удалить задачу
await StorageService.deleteTask('task_001');
```

### 2. ThemeService - Управление темой

#### Инициализация
```dart
// В main.dart
await ThemeService.init();

// В app.dart initState
if (await ThemeService.isDarkMode()) {
  _isDarkMode = true;
}
```

#### API методов
```dart
class ThemeService {
  // Инициализация
  static Future<void> init()
  
  // Получение состояния темы
  static Future<bool> isDarkMode()
  
  // Переключение темы
  static Future<void> toggleTheme()
  static Future<void> setDarkMode(bool isDark)
  
  // Получение ThemeData
  static ThemeData getLightTheme()
  static ThemeData getDarkTheme()
}
```

#### Пример использования
```dart
// Переключить тему
await ThemeService.toggleTheme();

// Установить конкретную тему
await ThemeService.setDarkMode(true);

// Проверить текущую тему
bool isDark = await ThemeService.isDarkMode();

// Получить MaterialApp тему
themeData: isDark 
  ? ThemeService.getDarkTheme()
  : ThemeService.getLightTheme(),
```

### 3. NotificationService - Уведомления (Placeholder)

#### Структура
```dart
class NotificationService {
  static Future<void> init() async {
    // Инициализация flutter_local_notifications
  }
  
  static Future<void> showTaskReminder(Task task) async {
    // Показать напоминание о задаче
  }
  
  static Future<void> scheduleNotification(
    Task task,
    Duration beforeDeadline,
  ) async {
    // Запланировать уведомление
  }
}
```

#### Интеграция в будущих версиях
```dart
// Когда добавляется задача
DateTimeReminder = deadline - Duration(hours: 1);
await NotificationService.scheduleNotification(
  task: newTask,
  beforeDeadline: Duration(hours: 1),
);

// Рабочее напоминание (15 минут перед дедлайном)
// Утреннее собрание (8:00 AM)
// Вечернее резюме (20:00)
```

### 4. ApiService - REST API (Ready for integration)

#### Конфигурация
```dart
class ApiService {
  static const String BASE_URL = 'https://api.studyflow.com/v1';
  
  // Endpoints готовы к использованию:
  // POST /api/tasks/create
  // GET /api/tasks/all
  // PUT /api/tasks/{id}
  // DELETE /api/tasks/{id}
  // GET /api/subjects/all
  // POST /api/sync
  
  // Когда будет реализована облачная синхронизация:
  // 1. Сохранить локально в Hive (быстро)
  // 2. Отправить на сервер в фоне
  // 3. Синхронизировать на других устройствах
}
```

---

## 💻 Экраны и навигация

### 1. LoginPage - Вход и Onboarding
```dart
class LoginPage extends StatefulWidget {
  final VoidCallback onThemeToggle;
  
  // Поля формы:
  // ├─ Email (демо)
  // ├─ Password (демо)
  // └─ Login button
  
  // При успешном входе:
  // └─ Переход на HomePage
}
```

### 2. HomePage - Главный экран/Дашборд
```dart
class HomePage extends StatefulWidget {
  final VoidCallback onThemeToggle;
  
  // Содержит:
  // ├─ Header с приветствием
  // ├─ Карточка прогресса
  // ├─ Статистические карточки
  // ├─ Список срочных задач
  // ├─ Сетка предметов с прогрессом
  // ├─ Bottom Navigation (6 табов)
  // └─ FAB для добавления (QuickAddModal)
  
  // Tabы:
  // 1. 🏠 Home
  // 2. ✅ Tasks
  // 3. 📅 Calendar
  // 4. 🎓 Subjects
  // 5. 📊 Statistics
  // 6. ⚙️ More / Exam Prep
}
```

### 3. TaskListPage - Список задач
```dart
class TaskListPage extends StatefulWidget {
  // Показывает:
  // ├─ Фильтры (Всё/Ожидание/Выполнено)
  // ├─ Список всех задач с карточками
  // │  └─ Каждая карточка:
  // │      ├─ Чекбокс ☐/☑
  // │      ├─ Icon предмета
  // │      ├─ Название и описание
  // │      ├─ Дата/время дедлайна
  // │      ├─ Приоритет с цветом
  // │      ├─ Кнопка редактирования ⚙️
  // │      └─ Кнопка удаления 🗑️
  // ├─ FAB для новой задачи
  // └─ Пустое состояние (если нет задач)
}
```

### 4. TaskCreatePage - Создание/Редактирование задачи
```dart
class TaskCreatePage extends StatefulWidget {
  final Task? taskToEdit; // Если редактируем
  
  // Форма с полями:
  // ├─ 📝 Название (TextInput)
  // ├─ 📄 Описание (TextArea)
  // ├─ 📚 Предмет (Dropdown)
  // ├─ 📅 Дата (DatePicker)
  // ├─ 🕐 Время (TimePicker)
  // ├─ 🚩 Приоритет (ButtonGroup × 4)
  // └─ ✅ Кнопка создания/сохранения
  
  // Валидация:
  // ├─ Название обязательно
  // ├─ Предмет обязательно
  // ├─ Дата/Время обязательны
  // └─ Приоритет обязателен
  
  // При успехе:
  // ├─ Сохранить в Hive (StorageService.saveTask)
  // ├─ Показать snackbar успеха
  // └─ Вернуться назад
}
```

### 5. QuickAddModal - Быстрое добавление
```dart
class QuickAddModal extends StatefulWidget {
  // Модаль снизу (BottomSheet) с:
  // ├─ 📝 Input для названия (с автофокусом)
  // ├─ 📚 Быстрые кнопки предметов (чипсы)
  // ├─ 🚩 Быстрые кнопки приоритета
  // ├─ ⏰ Быстрые вариусы дедлайна
  // │  ├─ [Завтра]
  // │  ├─ [3 дня]
  // │  └─ [Неделя]
  // ├─ [Отмена]
  // └─ [Создать] ✓
  
  // Особенности:
  // └─ Быстрое создание без деталей
  // └─ Предмет по умолчанию = текущий выбранный
  // └─ Время = 18:00 по умолчанию
}
```

### 6. CalendarPage - Календарь
```dart
class CalendarPage extends StatefulWidget {
  // Компоненты:
  // ├─ Заголовок с навигацией месяцев (< Февраль >)
  // ├─ Calendario (пн-вс)
  // │  └─ Каждый день:
  // │      ├─ Цифра дня
  // │      ├─ Цветная точка (если есть задачи)
  // │      └─ Кол-во задач
  // ├─ Выбранный день:
  // │  └─ Список задач на этот день
  // └─ Жесты:
  //    ├─ Тап на день = показать задачи
  //    ├─ < > = Предыдущий/Следующий месяц
  //    └─ Long tap = Создать задачу на этот день
  
  // Цветные точки:
  // ├─ 🔴 СРОЧНЫЕ задачи
  // ├─ 🟡 Средний приоритет
  // └─ 🟢 Низкий приоритет
}
```

### 7. SubjectsPage - Управление предметами
```dart
class SubjectsPage extends StatefulWidget {
  // Показывает список карточек предметов:
  // ├─ Иконка предмета (цвет)
  // ├─ Название
  // ├─ Преподаватель
  // ├─ Статистика (кол-во задач & %)
  // ├─ Прогресс-бар
  // ├─ [📋 Все задачи] = TaskListPage filtered by subject
  // └─ [➕ Добавить] = TaskCreatePage with subject pre-selected
  
  // Total: 4 карточки (Математика, История, Английский, Химия)
}
```

### 8. StatisticsPage - Аналитика
```dart
class StatisticsPage extends StatefulWidget {
  // Компоненты:
  // ├─ Выбор периода: [Неделя ▼] [Месяц ▼] [Всё ▼]
  // ├─ Общий прогресс (круговая диаграмма и %)
  // ├─ Распределение по статусам (horizontal bars)
  // ├─ Распределение по приоритетам (colored bars)
  // ├─ Прогресс по предметам (4 individual bars)
  // ├─ Достижения (6 бейджей):
  // │  ├─ 🥇 Старт (первая задача)
  // │  ├─ 🔥 Серия (7+ дней подряд)
  // │  ├─ ⭐ 100% (неделя чистая)
  // │  ├─ 🎯 Спринт (10 задач в день)
  // │  ├─ 📚 Учёный (50 слов английского)
  // │  └─ 💪 Power (50 дел в месяц)
  // └─ Легенда с объяснениями
  
  // Вычисления:
  // ├─ Прогресс = (Выполненные × Weight) / (Всего × Weight)
  // ├─ Weight = {URGENTLY: 4, HIGH: 3, MEDIUM: 2, LOW: 1}
  // └─ Обновляется Live при изменении статуса задачи
}
```

### 9. ExamPrepPage - Режим подготовки к экзамену
```dart
class ExamPrepPage extends StatefulWidget {
  // Компоненты:
  // ├─ 4 кнопки выбора предмета (2×2 сетка)
  // ├─ Карточка прогресса:
  // │  ├─ Кол-во выполненных задач
  // │  ├─ Всего задач
  // │  ├─ Процент (с мотивационным сообщением)
  // │  └─ Прогресс-бар
  // ├─ Список только задач выбранного предмета
  // │  └─ Чекбоксы обновляют % live
  // └─ [🚀 ИНТЕНСИВНАЯ ПОДГОТОВКА] кнопка
  //    └─ Полноэкранный режим без отвлечений
  
  // Фокусировка:
  // ├─ Скрывает все остальные предметы
  // ├─ Показывает только выбранный предмет
  // └─ Процентовка пересчитывается live
}
```

### Навигационная структура
```
┌──────────────────────────────────────┐
│          StudyFlowApp                │
│     (MaterialApp with Navigator)     │
└────────────────┬─────────────────────┘
                 │
         ┌───────┴────────┐
         ↓                ↓
    LOGIN PAGE      HOME PAGE
                      │
        ┌─────────────┼─────────────┬─────────────┬───────────────┐
        ↓             ↓             ↓             ↓               ↓
    TAB 2:        TAB 3:        TAB 4:        TAB 5:          TAB 6:
    TASKS       CALENDAR      SUBJECTS    STATISTICS      EXAM PREP
        │             │             │             │               │
        ├─ CREATE   ├─ DETAIL    ├─ DETAIL   └─ (No sub)    └─ (No sub)
        │        ├─ SELECT        │
        │        └─ LIST
        │        (filtered)
        │
    ├─ EDIT
    └─ LIST
        (filtered)

MODAL LAYERS (可 overlay):
├─ QuickAddModal
│  └─ Shows over any screen (FAB triggered)
├─ DatePicker
├─ TimePicker
├─ ConfirmDialog
└─ SnackBar (success messages)
```

---

## ⚙️ Конфигурация

### pubspec.yaml - Зависимости

```yaml
name: studyflow
description: Student Task Management Application
version: 1.2.0+4

environment:
  sdk: '>=3.0.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter
  
  # UI Framework
  cupertino_icons: ^1.0.2
  
  # Local Storage
  hive: ^2.2.3
  hive_flutter: ^1.1.0
  
  # Notifications
  flutter_local_notifications: ^17.0.0
  
  # Dates & Internationalization
  intl: ^0.19.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^3.0.0

flutter:
  uses-material-design: true
  assets:
    - assets/images/
    - assets/icons/
```

### analysis_options.yaml - Lint правила

```yaml
include: package:flutter_lints/flutter.yaml

linter:
  rules:
    - prefer_const_constructors
    - prefer_const_declarations
    - avoid_empty_else
    - avoid_print
    - avoid_relative_lib_imports
    - avoid_returning_null_for_future
    - avoid_slow_async_io
    - cancel_subscriptions
    - close_sinks
    - comment_references
    - control_flow_in_finally
    - empty_statements
    - hash_and_equals
    - invariant_booleans
    - iterable_contains_unrelated_type
```

### main.dart - Инициализация приложения

```dart
void main() async {
  // Инициализация Flutter binding
  WidgetsFlutterBinding.ensureInitialized();
  
  // Инициализация Hive
  await Hive.initFlutter();
  
  // Инициализация сервисов
  await ThemeService.init();
  await StorageService.init();
  
  // Запуск приложения
  runApp(const StudyFlowApp());
}
```

### app.dart - Конфигурация MaterialApp

```dart
class StudyFlowApp extends StatefulWidget {
  const StudyFlowApp({Key? key}) : super(key: key);

  @override
  State<StudyFlowApp> createState() => _StudyFlowAppState();
}

class _StudyFlowAppState extends State<StudyFlowApp> {
  bool _isDarkMode = false;

  @override
  void initState() {
    super.initState();
    _loadTheme();
  }

  Future<void> _loadTheme() async {
    final isDark = await ThemeService.isDarkMode();
    setState(() => _isDarkMode = isDark);
  }

  void _toggleTheme() {
    setState(() => _isDarkMode = !_isDarkMode);
    ThemeService.setDarkMode(_isDarkMode);
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'StudyFlow',
      theme: ThemeService.getLightTheme(),
      darkTheme: ThemeService.getDarkTheme(),
      themeMode: _isDarkMode ? ThemeMode.dark : ThemeMode.light,
      home: LoginPage(onThemeToggle: _toggleTheme),
    );
  }
}
```

---

## 📊 Диаграмма состояния данных

```
┌─────────────────────────────────────────────────────┐
│              HIVE STORAGE BOXES                     │
├─────────────────────────────────────────────────────┤
│                                                     │
│  BOX: "tasks"                                       │
│  ├─ Key: task_001                                   │
│  │  └─ Value: {Map with TaskHiveModel data}        │
│  ├─ Key: task_002                                   │
│  │  └─ Value: {Map...}                             │
│  └─ Key: task_NNN                                   │
│      └─ Value: {Map...}                             │
│                                                     │
│  BOX: "subjects"                                    │
│  ├─ Key: math                                       │
│  │  └─ Value: {SubjectHiveModel data}              │
│  ├─ Key: history                                    │
│  ├─ Key: english                                    │
│  └─ Key: chemistry                                  │
│                                                     │
│  BOX: "theme_settings"                              │
│  └─ Key: isDarkMode                                 │
│     └─ Value: true/false (boolean)                 │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## 🔄 Жизненный цикл приложения

```
[APP LAUNCH]
    ↓
[main() function]
    ├─ WidgetsFlutterBinding.ensureInitialized()
    ├─ Hive.initFlutter()
    ├─ ThemeService.init()
    │  └─ Читает isDarkMode из Hive
    ├─ StorageService.init()
    │  └─ Инициализирует boxes для tasks, subjects
    └─ runApp(StudyFlowApp)
       ├─ MaterialApp запускается
       ├─ StudyFlowApp._loadTheme() in initState
       │  └─ Применяет сохранённую тему
       └─ Показывает LoginPage
           ├─ Пользователь входит
           └─ Переход на HomePage
               ├─ Bottom navigation (6 табов)
               ├─ Загрузка задач в фоне (StorageService)
               └─ Отображение интерфейса

[DURING USE]
├─ Создание задачи:
│  ├─ TaskCreatePage
│  ├─ Валидация формы
│  ├─ StorageService.saveTask(Task)
│  ├─ Hive сохраняет TaskHiveModel
│  └─ Обновляется UI (setState)
│
├─ Переключение темы:
│  ├─ Клик на 🌙/☀️ кнопку
│  ├─ HomePage.onThemeToggle()
│  ├─ StudyFlowApp._toggleTheme()
│  ├─ ThemeService.setDarkMode(bool)
│  ├─ Hive сохраняет isDarkMode
│  └─ setState обновляет MaterialApp.themeMode
│
└─ При закрытии приложения:
   └─ Все изменения уже сохранены в Hive
   └─ При повторном открытии восстанавливается состояние

[FUTURE: Cloud Sync]
├─ При добавлении задачи:
│  ├─ 1. Сохранить локально в Hive (мгновенно)
│  ├─ 2. Показать успех через snackbar
│  ├─ 3. В фоне отправить на REST API сервер
│  └─ 4. Синхронизировать на других устройствах
```

---

## 🚀 Расширяемость

### Как добавить новый экран

```dart
// 1. Создайте новый файл в lib/features/[feature]/
// 2. Создайте StatefulWidget

class NewFeaturePage extends StatefulWidget {
  const NewFeaturePage({Key? key}) : super(key: key);

  @override
  State<NewFeaturePage> createState() => _NewFeaturePageState();
}

class _NewFeaturePageState extends State<NewFeaturePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('New Feature')),
      body: const Center(
        child: Text('Your content here'),
      ),
    );
  }
}

// 3. Добавьте в navigation (обычно в HomePage с IndexedStack)
```

### Как интегрировать REST API

```dart
// 1. Добавьте в pubspec.yaml:
// dependencies:
//   http: ^1.1.0

// 2. Обновите ApiService с реальными запросами:

class ApiService {
  static final http.Client _client = http.Client();
  static const String baseUrl = 'https://api.studyflow.com/v1';
  
  static Future<Task> createTask(Task task) async {
    final response = await _client.post(
      Uri.parse('$baseUrl/tasks'),
      body: jsonEncode(task.toJson()),
      headers: {'Content-Type': 'application/json'},
    );
    
    if (response.statusCode == 201) {
      return Task.fromJson(jsonDecode(response.body));
    } else {
      throw Exception('Failed to create task');
    }
  }
}

// 3. Обновите StorageService для использования API:

static Future<void> saveTask(Task task) async {
  // 1. Сохранить локально (быстро)
  await _tasksBox.put(task.id, taskHiveModel.toMap());
  
  // 2. Отправить на сервер (в фоне)
  ApiService.createTask(task).catchError((_) {
    // Если ошибка интернета - локальные данные остаются
  });
}
```

### Как использовать state management (Provider)

```dart
// 1. Добавьте в pubspec.yaml:
// dependencies:
//   provider: ^6.0.0

// 2. Создайте TaskProvider:

class TaskProvider extends ChangeNotifier {
  List<Task> _tasks = [];
  
  List<Task> get tasks => _tasks;
  
  Future<void> loadTasks() async {
    _tasks = await StorageService.getAllTasks();
    notifyListeners();
  }
  
  Future<void> addTask(Task task) async {
    await StorageService.saveTask(task);
    _tasks.add(task);
    notifyListeners();
  }
}

// 3. Используйте в UI:

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<TaskProvider>(
      builder: (context, provider, _) {
        return ListView.builder(
          itemCount: provider.tasks.length,
          itemBuilder: (context, index) {
            return TaskCard(task: provider.tasks[index]);
          },
        );
      },
    );
  }
}
```

---

## 📈 Performance Tips

### Оптимизация для больших списков
```dart
// Плохо: Загружает ВСЕ в памяти сразу
List<Task> allTasks = await StorageService.getAllTasks();

// Хорошо: Виртуальный скролл (Lazy loading)
ListView.builder(
  itemCount: tasks.length,
  itemBuilder: (context, index) => TaskCard(tasks[index]),
)

// Лучше: Пагинация для очень больших списков
const pageSize = 50;
List<Task> firstPage = tasks.sublist(0, pageSize);
// Загрузить следующие при скролле
```

### Оптимизация Hive запросов
```dart
// Плохо: Читает из диска каждый раз
List<Task> tasks = await StorageService.getAllTasks();
List<Task> urgentTasks = await StorageService.getAllTasks()
  .then((tasks) => tasks.where((t) => t.priorityIndex == 3).toList());

// Хорошо: Один запрос с фильтром
static Future<List<Task>> getTasksByPriority(int priority) async {
  final allTasks = await _tasksBox.values.toList();
  return allTasks
    .where((t) => TaskHiveModel.fromMap(Map.from(t)).priorityIndex == priority)
    .toList();
}

// Лучше: Index на Hive (будущее)
// Когда используем code generation: @HiveField(2)
```

---

**Версия документации**: 1.2  
**Дата обновления**: 11 февраля 2026 г.  
**Статус**: ✅ ДЛЯ РАЗРАБОТЧИКОВ
