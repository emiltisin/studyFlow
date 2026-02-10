# StudyFlow - Промт для генерации дизайна UI/UX в Midjourney / DALL-E / Stable Diffusion

## Для Midjourney (рекомендуется)

```
/imagine prompt: Modern minimalist mobile app interface for "StudyFlow", a student task management application. Shows 6 phone mockups in a grid layout:

1. Login screen: Indigo gradient background (#6366F1), white logo (school cap), "StudyFlow" title, 3 feature cards with icons (tasks, calendar, statistics), white login button.

2. Home screen: Clean white background, "StudyFlow" header + user avatar (top), gradient indigo progress card (42% completed, circular progress bar 3/7 tasks), 3 quick stat cards (completed green, in-progress blue, overdue red), urgent tasks list with colored left borders matching subjects.

3. Tasks screen: Filter chips (All, To Do, In Progress, Done), task cards with: checkbox, colored left border (subject color #6366F1, #F59E0B, #10B981), title, subject name, description, deadline with calendar icon "2 days left", status badge.

4. Calendar screen: Month navigation (prev/next arrows), calendar grid with highlighted today (indigo border), selected day (indigo background), event dots on dates, task list for selected day below.

5. Subjects screen: Subject cards with: colored icon (math indigo, history gold, english emerald, physics pink, chemistry teal), subject name, teacher name, progress bar, completed count "3/5 tasks".

6. Statistics screen: Period selector buttons (Week/Month/All), gradient progress card (42%, circular bar), horizontal stat bars for status distribution (completed green, in-progress blue, pending gray), achievement badges (bee icon green, fire streak red).

Design style: Material Design 3, modern, clean, minimalist, colorful, product screenshot quality, professional, bright natural lighting, white backgrounds, high contrast, UI elements clearly visible, rounded corners 12px, soft shadows.

Color palette: Primary indigo #6366F1, success green #10B981, danger red #EF4444, warning orange #F59E0B, info blue #3B82F6, subject colors varied, white #FFFFFF, neutral grays.

Phones: Modern iPhone or Android mockups, 6" screens, portrait orientation, no bezels visible emphasizing content.

--ar 16:9 --style raw --quality 2 --v 5.2
```

---

## Для DALL-E 3

```
Create 6 realistic mobile app interface mockups for "StudyFlow", a modern student task management application. Each mockup shows a smartphone screen with Material Design 3 style:

1. Authentication/Login Screen:
   - Full screen indigo gradient background
   - Centered white school cap logo
   - Large "StudyFlow" title
   - Subheading "Your Personal Study Coordinator"
   - Three feature cards with icons: manage tasks, plan schedule, track progress
   - White rounded login button at bottom

2. Home/Dashboard Screen:
   - White background with safe area padding
   - "StudyFlow" title and user avatar in header
   - Indigo gradient progress card showing 42% completion with circular progress indicator (3/7 tasks)
   - Three stat cards below: completed (green), in-progress (blue), overdue (red)
   - Section "Urgent Tasks" with colored task cards
   - Subject cards grid at bottom with icons and task counts

3. Tasks List Screen:
   - Header "My Tasks"
   - Horizontal filter chips: All, To Do, In Progress, Done
   - List of task cards with: checkbox, colored left border, title, subject name (colored text), description, deadline badge, status indicator
   - Floating action button at bottom right

4. Calendar Screen:
   - Month selector with navigation arrows
   - Calendar grid showing dates with weekday headers
   - Current day has indigo border, selected day has indigo background
   - Event indicator dots on dates with tasks
   - Below: selected day tasks list

5. Subjects Screen:
   - "My Subjects" title with count
   - Subject cards with: colored icon circle, subject name, teacher name, description, progress bar, completed task ratio
   - Color coded: math indigo, history orange, english green, physics pink, chemistry teal

6. Statistics Screen:
   - Period selector (Week, Month, All Time)
   - Large gradient progress card with percentage and circular indicator
   - Horizontal stat bars showing: status distribution, priority breakdown, tasks by subject
   - Achievement badges: bee icon (completed tasks), fire icon (daily streak)
   - Bottom navigation bar visible on all screens

Modern, clean, professional design with high contrast, clear typography, Material Design 3 principles, bright white backgrounds, colored accents, soft shadows, rounded corners, product photography quality.
```

---

## Для Stable Diffusion (v2.1+)

```
text "StudyFlow - Student Task Manager" --iw 1.5
{
StudyFlow mobile app interface mockup
Material Design 3 style
modern minimalist clean colorful ui
6 smartphone screens showing:
login screen with indigo gradient
home dashboard with progress cards
tasks list with filters
calendar view with event dots
subjects grid with colors
statistics with charts

indigo primary color #6366F1
green completion #10B981
red urgent #EF4444
orange medium priority #F59E0B
blue info #3B82F6
white background clean design

rounded corners 12px soft shadows
Material Design 3 bright natural lighting
professional product screenshot quality
high contrast clear typography
smartphone mockup 6 inch 1080x2400px
}

--steps 50 --scale 15 --sampler dpmpp_2m
```

---

## Быстрый промт для быстрой генерации

### Для Midjourney (краткая версия):

```
StudyFlow student task management app design, 6 iPhone mockups showing login, home dashboard with progress cards, tasks list, calendar, subjects grid, statistics dashboard. Material Design 3, indigo primary color, modern minimalist colorful UI, white backgrounds, soft shadows, product quality --ar 16:9 --style raw --quality 2
```

### Для ChatGPT + Image Generation:

```
Generate a modern mobile app UI design for "StudyFlow", a student task management application. Show 6 different screens:
1. Login screen with indigo gradient and white button
2. Home dashboard with progress indicators and stat cards
3. Tasks list with colored borders and filters
4. Calendar view with date selector
5. Subjects overview with colored cards
6. Statistics dashboard with charts

Use Material Design 3 principles, indigo color scheme, clean white backgrounds, and professional styling.
```

---

## Рекомендации для использования

### Лучшие параметры Midjourney:
- `--ar 16:9` для горизонтального формата (6 скриншотов в ряд)
- `--ar 9:16` для вертикального (показать реальный размер телефона)
- `--quality 2` для максимальной детализации
- `--style raw` для чистого результата без дополнительной обработки
- `--v 5.2` для последней версии модели

### Альтернативные команды:
```
--no blurry, watermark, text overlay
--stop 90 (для более чистых результатов)
```

### Post-processing:
После генерации можно:
1. Использовать инструменты дизайна (Figma, Adobe XD) для уточнения
2. Наложить реальные iPhone/Android mockups
3. Добавить реальный текст и иконки
4. Создать интерактивные прототипы с Prototype.app

---

## Варианты для дополнительных экранов

### Создание задачи:
```
StudyFlow create task modal, white center dialog, input fields for title, description, subject dropdown (colored options), date picker, priority selector (critical red, high orange, medium yellow, low green), task button. Material Design 3, clean minimal --v 5.2
```

### Экран экзамена:
```
StudyFlow exam prep mode screen, large exam title, progress sections by topic, timer running, study materials list, minimal design, focused ui --v 5.2
```

### Синхронизация/Настройки:
```
StudyFlow settings screen, dark mode toggle, backup and sync options, notification preferences, theme selector, material design 3, clean --v 5.2
```

