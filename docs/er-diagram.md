# Логическая схема базы данных

## Система доставки еды

Диаграмма сущностей, атрибутов, первичных и внешних ключей.


erDiagram
    КЛИЕНТ ||--o{ АДРЕС : "имеет"
    КЛИЕНТ ||--o{ КЛИЕНТ_ЗАКАЗ : "оформляет"
    АДРЕС ||--o{ КЛИЕНТ_ЗАКАЗ : "используется"
    РЕСТОРАН ||--o{ МЕНЮ : "создает"
    РЕСТОРАН ||--o{ КЛИЕНТ_ЗАКАЗ : "получает"
    МЕНЮ ||--o{ БЛЮДО : "содержит"
    КАТЕГОРИЯ ||--o{ БЛЮДО : "классифицирует"
    КЛИЕНТ_ЗАКАЗ ||--|{ ПОЗИЦИЯ_ЗАКАЗА : "содержит"
    БЛЮДО ||--o{ ПОЗИЦИЯ_ЗАКАЗА : "входит в"
    КУРЬЕР ||--o{ ДОСТАВКА : "выполняет"
    КЛИЕНТ_ЗАКАЗ ||--o| ДОСТАВКА : "имеет"
    КЛИЕНТ_ЗАКАЗ ||--o| ПЛАТЁЖ : "оплачивается"
    ПРОМОКОД o|--o{ КЛИЕНТ_ЗАКАЗ : "применяется"

    КЛИЕНТ {
        int client_id PK
        string имя
        string телефон
        string email
        date дата_регистрации
        string статус
    }

    АДРЕС {
        int address_id PK
        int client_id FK
        string город
        string улица
        string дом
        string квартира
        string комментарий
        boolean is_default
    }

    РЕСТОРАН {
        int restaurant_id PK
        string название
        string адрес
        string телефон
        decimal рейтинг
        string статус
        time час_открытия
        time час_закрытия
    }

    МЕНЮ {
        int menu_id PK
        int restaurant_id FK
        string версия
        date дата_с
        date дата_по
        boolean is_active
    }

    БЛЮДО {
        int dish_id PK
        int menu_id FK
        int category_id FK
        string название
        string описание
        decimal цена
        int вес_г
        int калорийность
        boolean is_available
    }

    КАТЕГОРИЯ {
        int category_id PK
        string название
        string описание
    }

    КЛИЕНТ_ЗАКАЗ {
        int order_id PK
        int client_id FK
        int address_id FK
        int restaurant_id FK
        int promo_id FK
        datetime дата_создания
        string статус
        decimal сумма_блюд
        decimal сумма_скидки
        decimal итог
    }

    ПОЗИЦИЯ_ЗАКАЗА {
        int order_item_id PK
        int order_id FK
        int dish_id FK
        int количество
        decimal цена_на_момент
    }

    КУРЬЕР {
        int courier_id PK
        string имя
        string телефон
        string транспорт
        decimal рейтинг
        string статус
        date дата_найма
    }

    ДОСТАВКА {
        int delivery_id PK
        int order_id FK, UK
        int courier_id FK
        datetime время_назначения
        datetime время_вручения
        decimal расстояние_км
        string статус
    }

    ПЛАТЁЖ {
        int payment_id PK
        int order_id FK, UK
        string способ
        decimal сумма
        datetime дата
        string статус
    }

    ПРОМОКОД {
        int promo_id PK
        string код UK
        string тип_скидки
        decimal значение
        date дата_с
        date дата_по
        int лимит_использований
        int использовано
    }
