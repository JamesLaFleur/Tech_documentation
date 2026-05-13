# Примеры технической документации

Примеры документации из разных проектов над которыми я работал. Охватывают несколько типов: архитектура и интеграция, API документация, deployment guide, описание модулей.

---

## Типы документации

| Тип | Файлы |
|-----|-------|
| Архитектура и интеграция | [WebSocket-интеграция](powerapp/websockets.md), [Система авторизации](powerapp/authentication.md) |
| Deployment Guide | [Руководство по развёртыванию](powerapp/deployment.md) |
| API Reference | [MindBox: заказы](4fresh/mindbox-orders.md), [Price Service](4fresh/price-service.md) |
| Описание модулей | [KeyCloak-тема](online-school/keycloak-theme.md), [KeyCloak + Nuxt.js](online-school/keycloak-frontend.md) |

---

## PowerApp

IoT-платформа для аренды пауэрбанков: два серверных компонента (API + Middleware), Flutter-клиент, real-time коммуникация, MQTT-протокол для взаимодействия со станциями.

**Стек:** Laravel 12, Flutter, RoadRunner, Redis, ClickHouse, MySQL, MQTT, Docker + GitLab CI/CD.

### [websockets.md](powerapp/websockets.md): WebSocket-интеграция

Документация системы real-time коммуникации: архитектура, каналы и события (аренда, СБП), клиентская интеграция на Flutter, авторизация private-каналов, стратегии обработки ошибок и переподключения, мониторинг и метрики.

### [deployment.md](powerapp/deployment.md): Руководство по развёртыванию

Полный deployment guide: структура Docker-образов, Traefik как reverse proxy и load balancer, blue-green deployment, GitLab CI/CD pipeline, конфигурация окружения, фоновые процессы, rollback, troubleshooting.

### [authentication.md](powerapp/authentication.md): Система авторизации

Архитектура авторизации без паролей: SMS и голосовые коды, Telegram Bot, JWT-токены, SMS-провайдеры, защита от спама, API эндпоинты.

---

## 4fresh

Российский eco/organic интернет-магазин. Микросервисная архитектура на PHP, интеграция с 1С и внешним CRM Mindbox.

**Стек:** PHP, RabbitMQ, Redis, PostgreSQL, 1С.

### [mindbox-orders.md](4fresh/mindbox-orders.md): MindBox, модуль заказов

API Reference: 5 операций (получение списка, расчёт корзины, создание заказа, изменение статуса), полные схемы входных и выходных данных с таблицами параметров и JSON-структурами.

### [price-service.md](4fresh/price-service.md): Price Service API

Документация модуля цен: эндпоинты, входные/выходные данные, логика синхронизации с 1С, health check.

---

## Online-school

Образовательная платформа с системой курсов, уроков, тестирования и виджетов.

**Стек:** NestJS, NuxtJS, KeyCloak, PostgreSQL.

### [keycloak-theme.md](online-school/keycloak-theme.md): Кастомная тема KeyCloak

Docker-конфигурация, Webpack-сборка, FreeMarker + Vue.js шаблоны, локализация, flow регистрации с мультишаговой формой.

### [keycloak-frontend.md](online-school/keycloak-frontend.md): Интеграция KeyCloak с Nuxt.js

Пакет `@nuxtjs/auth-next`, стратегия OpenIDConnect, кастомная схема авторизации, получение ролей из JWT-токена.
