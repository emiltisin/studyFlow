# StudyFlow - Руководство по разработке UI

## Структура проекта

```
lib/
├── models/
│   ├── task_model.dart           # Модель задачи
│   ├── subject_model.dart        # Модель предмета
│   └── stats_model.dart          # Модель статистики
├── features/
│   ├── auth/
│   │   └── login_page.dart       # Экран входа
│   └── tasks/
│       ├── home_page.dart        # Главная страница
│       ├── task_list_page.dart   # Список задач
│       ├── calendar_page.dart    # Календарь
│       ├── subjects_page.dart    # Предметы
│       ├── statistics_page.dart  # Статистика
│       └── task_page.dart        # Детали задачи (TODO)
├── widgets/
│   ├── task_card.dart            # Компонент карточки задачи (TODO)
│   ├── subject_card.dart         # Компонент карточки предмета (TODO)
│   └── progress_card.dart        # Компонент карточки прогресса (TODO)
├── services/
│   ├── notification_service.dart # Сервис уведомлений
│   ├── storage_service.dart      # Сервис хранилища (TODO)
│   └── sync_service.dart         # Сервис синхронизации (TODO)
├── app.dart                       # Корневое приложение
└── main.dart                      # Точка входа
```

## Реализованные экраны

### ✅ 1. Login Page (`lib/features/auth/login_page.dart`)
- Красивый градиент фон (индиго)
- Логотип и название приложения
- Список преимуществ с иконками
- Кнопка входа
- Переход на `HomePage`

### ✅ 2. Home Page (`lib/features/tasks/home_page.dart`)
- Bottom Navigation Bar с 5 вкладками
- Карточка прогресса с круговым индикатором
- Быстрая статистика (3 карточки)
- Список срочных задач
- Сетка предметов (2x2)
- Mock-данные для демонстрации

### ✅ 3. Task List Page (`lib/features/tasks/task_list_page.dart`)
- Фильтр по статусам (чипсы)
- Список задач с карточками
- Чекбокс для отметки выполнения
- Цветные границы по предметам
- Индикаторы приоритета и статуса
- Информация о дедлайне

### ✅ 4. Calendar Page (`lib/features/tasks/calendar_page.dart`)
- Навигация по месяцам
- Сетку календаря с выделением дней
- Индикаторы событий (точки на датах)
- Список задач для выбранного дня
- Поддержка русской локализации

### ✅ 5. Subjects Page (`lib/features/tasks/subjects_page.dart`)
- Список предметов с карточками
- Информация о преподавателе
- Прогресс-бар по выполнению задач
- Цветовая кодировка предметов
- Счётчик выполненных задач

### ✅ 6. Statistics Page (`lib/features/tasks/statistics_page.dart`)
- Переключатель периодов (неделя, месяц, всё время)
- Карточка общего прогресса
- Распределение по статусам
- Распределение по приоритетам
- Распределение по предметам
- Достижения (значки)

## Следующие шаги (TODO)

### Функциональность
1. **Локальное хранилище (Hive)**
   - Сохранение задач
   - Сохранение предметов
   - Сохранение пользовательских настроек
   - Кэширование статистики

2. **REST API интеграция**
   - Синхронизация с сервером
   - Регистрация и аутентификация
   - Загрузка / выгрузка данных
   - Обработка оффлайн режима

3. **Push-уведомления**
   - `flutter_local_notifications` для локальных уведомлений
   - OneSignal для удалённых уведомлений (опционально)
   - Напоминания о дедлайнах
   - Мотивационные сообщения

4. **Календарь устройства**
   - Экспорт задач в календарь
   - Синхронизация с Google Calendar
   - Планирование занятий

### UI/UX улучшения
1. **Дополнительные экраны**
   - Создание / редактирование задачи
   - Детали задачи
   - Редактирование предмета
   - Профиль пользователя
   - Настройки приложения

2. **Анимации**
   - Переходы между экранами
   - Заполнение прогресс-баров
   - Микровзаимодействия при нажатии

3. **Тёмный режим**
   - Тёмный вариант темы
   - Переключение режима
   - Сохранение предпочтения

4. **Интернационализация**
   - Поддержка нескольких языков
   - ARB файлы для переводов

5. **Рефакторинг компонентов**
   - Извлечение переиспользуемых виджетов
   - Создание компонент-библиотеки
   - Состояние приложения (Provider/Riverpod/Bloc)

### Тестирование
1. Unit тесты для моделей
2. Widget тесты для UI компонентов
3. Integration тесты для пользовательских сценариев

---

## Как использовать дизайн-промты

### Вариант 1: Генерация с Midjourney
1. Скопируй промт из `UI_DESIGN_PROMPTS.md`
2. Откройте Discord канал Midjourney
3. Напишите `/imagine prompt: [вставьте промт]`
4. Дождитесь генерации (5-10 минут)
5. Выберите лучший вариант
6. Сделайте Upscale для высокого качества

### Вариант 2: Использование DALL-E 3
1. Перейдите на ChatGPT Plus или OpenAI API
2. Скопируйте промт из раздела DALL-E 3
3. Используйте для генерации изображений
4. Скачайте высокое разрешение (4000x4000px)

### Вариант 3: Stable Diffusion (локально)
```bash
# Установка
git clone https://github.com/CompVis/stable-diffusion
pip install -r requirements.txt

# Генерация
python scripts/txt2img.py --prompt "StudyFlow..." --scale 15 --steps 50
```

---

## Интеграция дизайна в код

После получения дизайна-макета:

### 1. Создание компонентов
```dart
// lib/widgets/task_card.dart
class TaskCard extends StatelessWidget {
  final Task task;
  final Subject subject;
  final VoidCallback onTap;
  
  const TaskCard({
    required this.task,
    required this.subject,
    required this.onTap,
  });
  
  @override
  Widget build(BuildContext context) {
    // Реализация на основе макета
  }
}
```

### 2. Управление состоянием
```dart
// lib/providers/task_provider.dart (с использованием Riverpod)
final tasksProvider = StateNotifierProvider((ref) {
  return TaskNotifier();
});

class TaskNotifier extends StateNotifier<List<Task>> {
  TaskNotifier() : super([]);
  
  void addTask(Task task) => state = [...state, task];
  void updateTask(Task task) => state = [
    for (final t in state) t.id == task.id ? task : t
  ];
  void removeTask(String id) => state = [
    for (final t in state) if (t.id != id) t
  ];
}
```

### 3. Сервисы данных
```dart
// lib/services/storage_service.dart
class StorageService {
  late final Box<Task> tasksBox;
  late final Box<Subject> subjectsBox;
  
  Future<void> init() async {
    tasksBox = await Hive.openBox('tasks');
    subjectsBox = await Hive.openBox('subjects');
  }
  
  Future<void> saveTask(Task task) => tasksBox.put(task.id, task);
  Future<void> deleteTask(String id) => tasksBox.delete(id);
  List<Task> getAllTasks() => tasksBox.values.toList();
}
```

---

## Цвета и стиль

### Цветовая палитра
```dart
class AppColors {
  static const Color primary = Color(0xFF6366F1);      // Индиго
  static const Color success = Color(0xFF10B981);      // Зелёный
  static const Color danger = Color(0xFFEF4444);       // Красный
  static const Color warning = Color(0xFFF59E0B);      // Оранжевый
  static const Color info = Color(0xFF3B82F6);         // Синий
  static const Color background = Color(0xFFFFFFFF);   // Белый
  static const Color surface = Color(0xFFF3F4F6);      // Серый фон
  static const Color textPrimary = Color(0xFF1F2937);  // Чёрный
  static const Color textSecondary = Color(0xFF6B7280);// Серый текст
  static const Color border = Color(0xFFD1D5DB);       // Граница
}
```

### Тема приложения
```dart
// lib/app.dart
theme: ThemeData(
  useMaterial3: true,
  colorScheme: ColorScheme.fromSeed(
    seedColor: Colors.indigo,
    brightness: Brightness.light,
  ),
  cardTheme: CardTheme(
    elevation: 0,
    shape: RoundedRectangleBorder(
      borderRadius: BorderRadius.circular(12),
    ),
  ),
)
```

---

## Ресурсы

- **Flutter документация**: https://flutter.dev/docs
- **Material Design 3**: https://material.io/design
- **Hive база данных**: https://docs.hivedb.dev/
- **Riverpod управление состоянием**: https://riverpod.dev/
- **FlutterFlow визуальный редактор**: https://flutterflow.io/

---

## Контрольный список разработки

- [ ] Модели данных (Task, Subject, Stats) 
- [ ] Страница входа с красивым дизайном
- [ ] Главная страница с обзором
- [ ] Список задач с фильтрацией
- [ ] Календарь с выбором дат
- [ ] Экран предметов
- [ ] Страница статистики
- [ ] Создание / редактирование задачи
- [ ] Локальное хранилище (Hive)
- [ ] REST API интеграция
- [ ] Push-уведомления
- [ ] Синхронизация между устройствами
- [ ] Тёмный режим
- [ ] Тестирование
- [ ] Оптимизация производительности
- [ ] Подготовка к публикации

