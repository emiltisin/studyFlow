# 📚 StudyFlow - Полносценный планировщик для студентов

> **Студенческое приложение для управления учебными задачами с календарём, статистикой и режимом подготовки к экзаменам**

[![Flutter](https://img.shields.io/badge/Flutter-v3.0%2B-blue)](https://flutter.dev)
[![Dart](https://img.shields.io/badge/Dart-v3.0%2B-green)](https://dart.dev)
[![License](https://img.shields.io/badge/License-MIT-purple)](LICENSE)
[![Status](https://img.shields.io/badge/Status-v1.2%20Stable-brightgreen)](.)

---

## 🎯 Быстрый старт

**Первый раз здесь?** Начните с [📋 DOCUMENTATION_INDEX.md](DOCUMENTATION_INDEX.md) - это ваш аэропорт для всей документации.

| Вы... | Смотрите | Время |
|------|----------|-------|
| 👥 Пользователь | [USER_GUIDE_FULL.md](USER_GUIDE_FULL.md) | 30 мин |
| 🎨 Дизайнер | [UI_VISUAL_GUIDE.md](UI_VISUAL_GUIDE.md) | 25 мин |
| 💻 Разработчик | [TECHNICAL_GUIDE.md](TECHNICAL_GUIDE.md) | 45 мин |
| 🏃 Спешите | [QUICK_REFERENCE.md](QUICK_REFERENCE.md) | 10 мин |
| 📋 Менеджер | [PROJECT_COMPLETION_SUMMARY.md](PROJECT_COMPLETION_SUMMARY.md) | 20 мин |

---

## ✨ Что это такое?

**StudyFlow** - это полнофункциональное Flutter приложение для студентов с:

### ✅ Основной функционал
- **📝 Создание задач** - с названием, дедлайном, приоритетом
- **📅 Интерактивный календарь** - визуализация нагруженности дней
- **🎓 Управление предметами** - 4 встроенных предмета с цветовой кодировкой
- **📊 Статистика** - отслеживание прогресса в % по предметам
- **🎯 Режим подготовки к экзаменам** - фокус на одном предмете
- **🌙/☀️ Светлая/Тёмная тема** - Material Design 3
- **💾 Локальное хранилище** - все данные сохраняются в Hive

### 🏆 Особенности
- ✅ Приоритеты на 4 уровня (низкий/средний/высокий/срочно)
- ✅ Чекбоксы для отметки выполнения
- ✅ Прогресс рассчитывается по взвешенной формуле
- ✅ 6 достижений для мотивации
- ✅ Material Design 3 интерфейс
- ✅ Полностью локально (без облака)

---

## 🚀 Запуск приложения

### Требования
```bash
Flutter 3.0+
Dart 3.0+
Android Studio / VS Code / Xcode
```

### Команды
```bash
# Клонировать репозиторий
git clone [repo-url]
cd study

# Установить зависимости
flutter pub get

# Запустить приложение
flutter run                    # Автоматический выбор устройства
flutter run -d windows         # Windows
flutter run -d edge           # Веб (Edge)
flutter run -d chrome         # Веб (Chrome)

# Собрать для продакшена
flutter build apk             # Android
flutter build ios             # iOS
flutter build windows         # Windows
flutter build web             # Web
```

---

## 📱 9 Основных экранов

```
1. 🔐 LOGIN PAGE          - Вход в приложение
2. 🏠 HOME PAGE          - Дашборд с прогрессом
3. ✅ TASK LIST PAGE     - Список всех задач
4. ➕ TASK CREATE PAGE   - Создание/редактирование
5. 📅 CALENDAR PAGE      - Интерактивный календарь
6. 🎓 SUBJECTS PAGE      - Управление предметами
7. 📊 STATISTICS PAGE    - Аналитика и графики
8. 🎯 EXAM PREP PAGE     - Подготовка к экзаменам
9. 💬 QUICK ADD MODAL    - Быстрое добавление (модаль)

+ Bottom Navigation с 6 табами
+ Theme switcher (светлая/тёмная)
```

---

## 🏗️ Архитектура

### Трёхслойная архитектура
```
┌─────────────────────────────────────┐
│   PRESENTATION LAYER (UI)           │
│   9 экранов + 20+ виджетов         │
└──────────────┬──────────────────────┘
               ↓
┌─────────────────────────────────────┐
│   BUSINESS LAYER (Services)         │
│   • StorageService (Hive)           │
│   • ThemeService (Themes)           │
│   • ApiService (REST ready)         │
│   • NotificationService (ready)     │
└──────────────┬──────────────────────┘
               ↓
┌─────────────────────────────────────┐
│   DATA LAYER (Models)               │
│   • Task / TaskHiveModel            │
│   • Subject / SubjectHiveModel      │
│   • StudyStats                      │
└──────────────┬──────────────────────┘
               ↓
┌─────────────────────────────────────┐
│   STORAGE LAYER                     │
│   Hive Local Database               │
│   (быстро, надежно, локально)      │
└─────────────────────────────────────┘
```

### Технологический стек
- **UI Framework**: Flutter 3.0+
- **Language**: Dart 3.0+
- **Design**: Material Design 3
- **Local DB**: Hive 2.2.3
- **Notifications**: flutter_local_notifications 17.0.0
- **Internationalization**: intl 0.19.0

---

## 📊 Статистика Проекта

```
Code Lines:         3,500+ строк Dart
Files:              18 основных файлов
Screens:            9 экранов
Models:             5 моделей данных
Services:           4 сервиса
Widgets:            20+ компонентов
Documentation:      1,500+ строк
Tests:              1 widget test ready
Status:             ✅ Production Ready
```

---

## 📚 Документация

### Для разных аудиторий
| Документ | Для кого | Содержит |
|----------|----------|----------|
| [📋 PROJECT_COMPLETION_SUMMARY.md](PROJECT_COMPLETION_SUMMARY.md) | Менеджеры, stakeholders | Обзор проекта, статистика, чек-лист |
| [🎨 UI_VISUAL_GUIDE.md](UI_VISUAL_GUIDE.md) | Дизайнеры, UX специалисты | ASCII-art макеты, цвета, типография |
| [👥 USER_GUIDE_FULL.md](USER_GUIDE_FULL.md) | Конечные пользователи | Использование, FAQ, советы |
| [💻 TECHNICAL_GUIDE.md](TECHNICAL_GUIDE.md) | Разработчики | Архитектура, код, API |
| [🚀 QUICK_REFERENCE.md](QUICK_REFERENCE.md) | Все | Шпаргалка на одной странице |
| [📊 DOCUMENTATION_INDEX.md](DOCUMENTATION_INDEX.md) | Все | Навигация по всем документам |

---

## 🎨 Дизайн

### Цветовая палитра
```
📐 Математика    #6366F1  Indigo
📖 История       #F59E0B  Orange  
🗣️ Английский    #10B981  Green
🧪 Химия         #14B8A6  Teal
```

### Темы
- ✨ **Светлая**: Свежая, яркая, для дневного использования
- 🌙 **Тёмная**: Мягкая, спокойная, для вечернего использования
- 📱 **Адаптивная**: Поддержка всех размеров экранов

---

## 💾 Данные и хранилище

### Где сохраняются данные?
```
Hive Local Database (на вашем устройстве)
├─ Box "tasks"          - все задачи
├─ Box "subjects"       - все предметы  
└─ Box "theme_settings" - ваша выбранная тема
```

### Безопасность
- ✅ Локальное хранилище (без серверов)
- ✅ Шифрование данных (Hive)
- ✅ Конфиденциальность (ничего не отправляется)

### Будущее (v2.0+)
- 🔄 REST API синхронизация
- ☁️ Облачное хранилище
- 🔄 Синхронизация между устройствами

---

## 🔧 Основные компоненты

### StorageService - Локальная БД
```dart
await StorageService.saveTask(myTask);           // Сохранить
List<Task> tasks = await StorageService.getAllTasks();  // Получить
await StorageService.deleteTask('task-id');     // Удалить
```

### ThemeService - Управление темой
```dart
await ThemeService.toggleTheme();    // Переключить
bool isDark = await ThemeService.isDarkMode();  // Проверить
```

### ApiService - REST API (готов к использованию)
```dart
// Endpoints готовы для облачной синхронизации
POST /api/tasks/create
GET /api/tasks/all
PUT /api/tasks/{id}
DELETE /api/tasks/{id}
```

---

## ✅ Выполненные требования

- [x] Создание задач
- [x] Отметки выполнения (чекбоксы)
- [x] Цветовая кодировка предметов
- [x] Интерактивный календарь
- [x] Отслеживание прогресса
- [x] Режим подготовки к экзамену
- [x] Уведомления (фреймворк готов)
- [x] Светлая/Тёмная тема
- [x] Локальное хранилище
- [x] Material Design 3 дизайн
- [x] Полная документация

---

## 🚦 Дорожная карта

### ✅ v1.2 (Текущая)
- Все основные функции готовы
- Полная документация
- Material Design 3 интерфейс
- Локальное хранилище (Hive)

### ⏳ v2.0 (Q2-Q3 2026)
- REST API синхронизация
- Облачное хранилище (Firebase/Supabase)
- Push-уведомления
- Синхронизация между устройствами

### 📅 v3.0+ (Q4 2026+)
- AI-рекомендации
- Интеграции (Google Calendar, Telegram)
- Кооперативная работа
- Мобильное приложение на нативе

---

## 🐛 Известные проблемы

| Проблема | Статус | решение |
|----------|--------|---------|
| Windows build MSB8066 | 🔧 Известна | Используй `flutter run -d edge` |
| Большие списки тормозят | ⏳ Планируется | Виртуальный скролл в v2.0 |
| Нет облачной синхронизации | ✅ Запланирована | REST API интеграция в v2.0 |

---

## 👥 Контрибьютеры

- 👨‍💻 **Разработка**: Flutter + Dart
- 🎨 **Тестирование**: Manual testing
- 📚 **Документация**: Полная

---

## 📄 Лицензия

MIT License - Свободное использование в образовательных целях

---

## 📞 Поддержка

- 📖 **Документация**: [DOCUMENTATION_INDEX.md](DOCUMENTATION_INDEX.md)
- 🐛 **Отчёт об ошибке**: Создать issue в репозитории
- 💡 **Идея**: GitHub Discussions
- 📧 **Email**: support@studyflow.com

---

## 🎓 Образовательная ценность

Этот проект демонстрирует:
- ✅ Правильную архитектуру Flutter приложения
- ✅ Использование Hive для локального хранилища
- ✅ Material Design 3 implementation
- ✅ State management с StatefulWidget
- ✅ Form validation и user input
- ✅ Navigation и routing
- ✅ Date/time handling
- ✅ Theme management
- ✅ Responsive design

**Подходит как для учёбы, так и как стартовая точка для реального проекта.**

---

## 🏁 Заключение

```
StudyFlow = полнофункциональное, задокументированное,
           производственное приложение для студентов
           с чистой архитектурой и современным дизайном
```

**Начните прямо сейчас** → Читайте [DOCUMENTATION_INDEX.md](DOCUMENTATION_INDEX.md)

---

**Версия**: 1.2.0  
**Дата обновления**: 11 февраля 2026 г.  
**Статус**: ✅ READY FOR PRODUCTION

---

## Getting Started

This is a Flutter project. To get started:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)
- [Flutter documentation](https://docs.flutter.dev/)
