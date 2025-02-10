# Alchemytics - Infra

В данном репозитории будет храниться основная информация по тому, что представляет из себя инфраструктура проекта Alchemytics, а также все необходимые инструкции для управления приложениями и сервисами

1. [Основные сервисы](#основные-сервисы)

# Основные сервисы

Целевая структура сервисов состоит из следующих компонент:

- **website** - основной вебсайт проекта (https://alchemytics.ru), который может существовать отдельно от остального проекта и по сути представляет собой MPA (Multi Page Application) реализацию блога
- **profile** - личная страничка, доступная после прохождения авторизации (https://profile.alchemytics.ru); необходима для получения доступов к демонстрационным стендам
- **api** - основное API для реализации взаимодействия сервисов между друг другом
- **db** - база данных для хранения данных
- **s3** - объектное хранилище (преимущественно для резервного копирования данных)

Визуально сервисы связаны между собой следующим образом

```mermaid
flowchart LR
    subgraph websites
    direction TB
        website@{ shape: rounded }
        profile@{ shape: rounded }

        website ~~~ profile
    end

    jWebsiteToApi@{ shape: f-circ }

    subgraph internal
    direction LR
        api@{ shape: rounded }
        db@{ shape: cyl }
        s3@{ shape: lin-cyl }

        api --> db
        api --> s3
    end

    websites --> jWebsiteToApi --> api
```
