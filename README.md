# Примеры технической документации

Примеры документации из разных проектов над которыми я работал. Охватывают несколько типов: архитектура и интеграция, deployment guide, описание модулей.

---

## Типы документации

| Тип | Файлы |
|-----|-------|
| Архитектура и интеграция | [WebSocket-интеграция](powerapp/websockets.md), [Система авторизации](powerapp/authentication.md) |
| Deployment Guide | [Руководство по развёртыванию](powerapp/deployment.md) |
| Описание модулей | [KeyCloak-тема](online-school/keycloak-theme.md) |
| API документация | [RoleModule](online-school/role.md) |

---

## PowerApp

IoT-платформа для аренды пауэрбанков: два серверных компонента (API + Middleware), Flutter-клиент, real-time коммуникация, MQTT-протокол для взаимодействия со станциями.

**Стек:** Laravel 12, Flutter, RoadRunner, Redis, ClickHouse, MySQL, MQTT, Docker + GitLab CI/CD.

### [websockets.md](powerapp/websockets.md): WebSocket-интеграция

Документация системы real-time коммуникации: архитектура, каналы и события (аренда, СБП), клиентская интеграция на Flutter, авторизация private-каналов, стратегии обработки ошибок и переподключения, мониторинг и метрики.

### [deployment.md](powerapp/deployment.md): Руководство по развёртыванию

Инструкция по развёртыванию: Docker, CI/CD, конфигурация окружения, фоновые процессы.

### [authentication.md](powerapp/authentication.md): Система авторизации

Архитектура авторизации без паролей: SMS и голосовые коды, Telegram Bot, JWT-токены, SMS-провайдеры, защита от спама, API эндпоинты.

---

## Online-school

Образовательная платформа с системой курсов, уроков, тестирования и виджетов.

**Стек:** NestJS, NuxtJS, KeyCloak, PostgreSQL.

### [keycloak-theme.md](online-school/keycloak-theme.md): Кастомная тема KeyCloak

Docker-конфигурация, Webpack-сборка, FreeMarker + Vue.js шаблоны, переменные окружения, flow регистрации с многошаговой формой.

### [role.md](online-school/role.md): RoleModule API

Документация модуля управления ролями: описание ролей платформы, CRUD операции, входные и выходные данные.
