# Как выложить портфолио на GitHub

Код уже приведён к публичному виду (секреты, ПДн, README). Осталось создать аккаунт и запушить.

## 1. Аккаунт

1. https://github.com/signup
2. Логин латиницей, коротко: `mixk`, `mkarpenko`, не `super-hacker-2026`.
3. Аватар (не дефолт), имя, город, 1–2 предложения в **About**.
4. Email в настройках: тот, с которого будете коммитить, лучше сделать **verified**.

## 2. Git на компьютере

Если `git --version` не находится: https://git-scm.com/download/win

Задайте имя и email (один раз на машину). Я git config не меняю — это ваши данные:

```bash
git config --global user.name "Ваше Имя"
git config --global user.email "тот-же@email-что-на-GitHub"
```

В каждой из пяти папок проектов плюс `github-profile` git уже инициализирован, файлы в индексе. После настройки имени:

```bash
git commit -m "Initial public snapshot."
```

## 3. Войти в GitHub из терминала

Проще всего [GitHub CLI](https://cli.github.com/):

```bash
winget install GitHub.cli
gh auth login
```

Выберите GitHub.com → HTTPS → Login with a web browser.

Либо SSH-ключ: Settings → SSH and GPG keys.

## 4. Имена репозиториев (латиница)

| Папка на диске | Имя на GitHub |
|---|---|
| `D:\Projects\bazacoop\bazacoop-master` | `bazacoop` |
| `D:\Projects\Экскаватор` | `excavator-valuation` |
| `D:\Projects\UpGrade` | `upgrade` |
| `D:\Projects\фастЕГРН` | `fast-egrn` |
| `D:\Projects\Вишлист` | `raduga-wishlist` |
| `D:\Projects\github-profile` | **точно как ваш логин** (`USERNAME/USERNAME`) |

Репозиторий с тем же именем, что логин, GitHub показывает **на главной профиля**. Туда копируется `github-profile/README.md`.

## 5. Создать репо и запушить (пример)

Из папки проекта, где уже есть `git init` и первый коммит:

```bash
cd D:\Projects\bazacoop\bazacoop-master
gh repo create bazacoop --public --source=. --remote=origin --push
```

То же для остальных, подставляя имя из таблицы.

Если `gh` нет:

1. На сайте New repository, **без** README (он уже в проекте).
2. Затем:

```bash
git remote add origin https://github.com/USERNAME/bazacoop.git
git branch -M main
git push -u origin main
```

## 6. Оформить профиль, не репозитории

На GitHub это важнее, чем «звёздочки».

1. **Pinned**: шесть карточек — все пять проектов + профиль, либо лучшие 4.
2. **About**: «Python / Java. Внутренние продукты: оценка, рынок, кадастр».
3. Профиль-README: замените `[ИМЯ]`, ссылки, Telegram.
4. В каждом репо: Topics (`fastapi`, `spring-boot`, `appraisal`, `python`) — справа Edit.
5. Не пиньте пустые WIP. Лучше 5 законченных карточек, чем 20 папок.

## 7. Чего никогда не пушить

Уже закрыто `.gitignore`, но руками не добавляйте:

- файл `env` / `.env` (в bazacoop там был пароль VPS)
- `data/chrome_profile`
- Excel-дампы объявлений, `bookings.json` с живыми ФИО
- Chrome / Avito куки

Перед пушем:

```bash
git status
git diff --cached
```

Если видите пароль, IP сервера, ФИО коллег, телефоны — `git reset`, правьте файл.

## 8. Для хакатона

Жюри смотрит 30 секунд:

1. Главная GitHub — понятно, кто вы.
2. Один репозиторий с README: зачем продукт, как запустить, стек, архитектура в 10 строк.
3. Код читается без `D:\Projects\...` и без `password=123`.

Дальше уже задача хакатона в отдельном репо, не смешивайте с этими пятью.
