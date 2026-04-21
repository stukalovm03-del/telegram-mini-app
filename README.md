# Halyva App

Профессиональный шаблон для разработки Telegram Mini Apps с использованием **Telegram UI** библиотеки.

## 🚀 Что внутри

- ⚡ **Vite** — молниеносная сборка и HMR
- ⚛️ **React 18** — последняя версия React
- 📘 **TypeScript** — полная типизация
- 🎨 **Telegram UI** — 60+ готовых компонентов
- 🌓 **Авто-тема** — синхронизация с темой Telegram
- 📱 **Адаптивность** — iOS и Android стили
- 🔧 **ESLint** — контроль качества кода

## 📦 Установка зависимостей

```bash
cd /home/user/Hydro9/telegram-mini-app
npm install
```

## 🛠️ Команды

### Запуск в режиме разработки

```bash
npm run dev
```

Откроет сервер на `http://localhost:5173`

### Сборка для продакшена

```bash
npm run build
```

Создаст оптимизированную сборку в папке `dist/`

### Предпросмотр продакшен сборки

```bash
npm run preview
```

### Проверка типов

```bash
npm run type-check
```

### Линтинг кода

```bash
npm run lint
```

## 📁 Структура проекта

```
telegram-mini-app/
├── public/                 # Статические файлы
├── src/
│   ├── components/        # React компоненты
│   │   ├── HomePage.tsx   # Главная страница
│   │   ├── ProfilePage.tsx # Пример профиля
│   │   └── SettingsPage.tsx # Пример настроек
│   ├── hooks/            # Кастомные хуки
│   │   └── useTelegramTheme.ts # Хук для темы
│   ├── styles/           # Глобальные стили
│   │   └── global.css
│   ├── utils/            # Утилиты
│   ├── App.tsx           # Главный компонент
│   ├── main.tsx          # Точка входа
│   └── vite-env.d.ts     # TypeScript декларации
├── index.html            # HTML шаблон
├── vite.config.ts        # Конфигурация Vite
├── tsconfig.json         # Конфигурация TypeScript
└── package.json          # Зависимости
```

## 🎨 Примеры использования компонентов

### Базовый пример

```tsx
import { AppRoot, Button, Section, Cell } from '@telegram-apps/telegram-ui';

function App() {
  return (
    <AppRoot>
      <Section header="Привет!">
        <Cell>Мое приложение</Cell>
        <Button mode="filled">Кнопка</Button>
      </Section>
    </AppRoot>
  );
}
```

### С темой Telegram

```tsx
import { useTelegramTheme } from './hooks/useTelegramTheme';

function App() {
  const { platform, appearance } = useTelegramTheme();

  return (
    <AppRoot platform={platform} appearance={appearance}>
      {/* Автоматически применится тема Telegram */}
    </AppRoot>
  );
}
```

### Работа с Telegram WebApp API

```tsx
// Показать алерт
window.Telegram?.WebApp?.showAlert('Привет!');

// Получить данные пользователя
const user = window.Telegram?.WebApp?.initDataUnsafe?.user;

// Главная кнопка
const MainButton = window.Telegram?.WebApp?.MainButton;
MainButton.setText('Продолжить');
MainButton.show();
MainButton.onClick(() => {
  console.log('Нажата главная кнопка');
});
```

## 📚 Доступные компоненты

### Основные
- `AppRoot` — корневой компонент
- `Button` — кнопки (filled, bezeled, plain)
- `Cell` — элемент списка
- `Section` — секция с заголовком
- `List` — контейнер для секций

### Формы
- `Input` — текстовое поле
- `Textarea` — многострочное поле
- `Checkbox` — чекбокс
- `Radio` — радио кнопка
- `Switch` — переключатель
- `Slider` — слайдер
- `Select` — выпадающий список

### Отображение
- `Avatar` — аватар
- `Badge` — бейдж
- `Card` — карточка
- `Modal` — модальное окно
- `Placeholder` — заглушка

### Типография
- `Title` — заголовки
- `Text` — основной текст
- `Caption` — маленький текст
- `Headline` — подзаголовки

### Обратная связь
- `Spinner` — загрузка
- `Progress` — прогресс бар
- `Snackbar` — уведомления

## 🔧 Конфигурация

### Vite

Настроен для быстрой разработки с поддержкой:
- SWC для максимальной скорости
- Алиасы путей (`@/` → `src/`)
- Code splitting для оптимизации
- Source maps для отладки

### TypeScript

Строгий режим включен для надёжности:
- Полная типизация
- Проверка неиспользуемых переменных
- Автодополнение в IDE

### ESLint

Проверка кода по лучшим практикам:
- TypeScript рекомендации
- React hooks правила
- Автоматический фикс простых проблем

## 🌐 Деплой

### 1. Соберите проект

```bash
npm run build
```

### 2. Загрузите на хостинг

Папку `dist/` можно разместить на:
- GitHub Pages
- Vercel
- Netlify
- Любой статический хостинг

### 3. Настройте Telegram Bot

```python
import requests

BOT_TOKEN = "ваш_токен"
WEB_APP_URL = "https://ваш-домен.com"

# Установка команд с Web App
requests.post(
    f"https://api.telegram.org/bot{BOT_TOKEN}/setMyCommands",
    json={
        "commands": [
            {
                "command": "start",
                "description": "Запустить приложение"
            }
        ]
    }
)

# Создать кнопку с Web App
menu_button = {
    "type": "web_app",
    "text": "Открыть App",
    "web_app": {"url": WEB_APP_URL}
}
```

## 🎯 Best Practices

1. **Всегда оборачивайте в AppRoot**
   ```tsx
   <AppRoot>{/* ваш контент */}</AppRoot>
   ```

2. **Используйте CSS переменные**
   ```tsx
   <div style={{ color: 'var(--tgui--text_color)' }}>
     Текст адаптируется под тему
   </div>
   ```

3. **Проверяйте доступность Telegram API**
   ```tsx
   if (window.Telegram?.WebApp) {
     // Код для Telegram
   } else {
     // Fallback для разработки
   }
   ```

4. **Тестируйте обе темы**
   - Светлую и тёмную тему
   - iOS и Android платформы

## 📖 Документация

- **Telegram UI**: [GitHub](https://github.com/Telegram-Mini-Apps/TelegramUI)
- **Playground**: [tgui.xelene.me](https://tgui.xelene.me/)
- **Telegram WebApps**: [Docs](https://core.telegram.org/bots/webapps)
- **Mini Apps**: [telegram.org/apps](https://telegram.org/apps)

## 🐛 Troubleshooting

### Стили не применяются

Убедитесь что импортировали стили:
```tsx
import '@telegram-apps/telegram-ui/dist/styles.css';
```

### TypeScript ошибки

Установите типы:
```bash
npm install --save-dev @types/react @types/react-dom
```

### Telegram API недоступен

Для разработки вне Telegram проверяйте:
```tsx
if (window.Telegram?.WebApp) {
  // Используем Telegram API
}
```

## 🤝 Поддержка

- Issues: [GitHub Issues](https://github.com/Telegram-Mini-Apps/TelegramUI/issues)
- Telegram: [@TelegramApps](https://t.me/TelegramApps)

## 📝 Лицензия

MIT License

---

**Готово к разработке!** 🚀

Запустите `npm install && npm run dev` и начинайте создавать своё приложение.
