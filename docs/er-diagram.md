# Логическая схема базы данных

## Система доставки еды

Диаграмма сущностей, атрибутов, первичных и внешних ключей.

```mermaid
erDiagram
    CLIENT ||--o{ ADDRESS : has
    CLIENT ||--o{ ORDERS : creates
    RESTAURANT ||--o{ MENU : has
    MENU ||--o{ DISH : contains
    CATEGORY ||--o{ DISH : classifies
    ORDERS ||--|{ ORDER_ITEM : contains
    DISH ||--o{ ORDER_ITEM : includes
    ORDERS ||--o| DELIVERY : has
    COURIER ||--o{ DELIVERY : performs
    ORDERS ||--o| PAYMENT : has
    PROMO_CODE ||--o{ ORDERS : applies
