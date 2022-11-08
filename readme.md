# Глеб Буткевич 053503
## 1. Тема: Интернет-магазин с играми
## 2. Функциональные требования к проекту:
### Роли пользователей:
1. Покупатель
2. Администратор
3. Магазин
### Авторизация пользователя
Пользователь должнен иметь возможность:
- Зарегистрироваться.
- Войти в аккаунт, выйти.
- Восстановить пароль
### Возможности пользователей
- Администратор
    + Создать, просмотреть, удалить, отредактировать магазины
    + Создать, просмотреть, удалить, отредактировать любого пользователя
    + Просмотр действий покупателей и магазинов

- Магазин
    + Создавать, просмотреть, отредактировать или удалить игры
    + Журналирование действий

- Покупатель
    + Просмотреть, добавить в корзину, удалить из корзины игры
    + Журналивароние действий

## 3. Список сущностей БД:
- Основа пользователя
- Покупатель
- Администратор
- Магазин
- Корзина
- Игра
- Жанр игры
- Лог пользователя

## 4. Схематично изобразить не нормальзованную схему БД:


## 5. Описать каждую сущность:

- Основа пользователя (связь с сущностями "Администратор", "Магазин", "Покупатель" типа one-to-one)

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|UserID|INT(4) | Первичный ключ | Обязательное поле, уникальный, авто-инкрементация        |
|Email         | VARCHAR(32)    | Почта пользователя      | Обязательное поле, уникальный  |
|Password      | VARCHAR(32)    | Пароль пользователя     | Обязательное поле              |

- Покупатели (связь с сущностью "Корзина" типом связи one-to-one)

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|CustomerID|INT(4)        | Первичный ключ      | Обязательное поле, уникальный, авто-инкрементация              |
|UserID    |INT(4)        | Внешний ключ к "UserBase" , для получения данных основы пользователя (пароль, почта) |Обязательное поле|
|City      |VARCHAR(32)   | Город пользователя, можно использовать для рекомендаций магазинов из родного города  |Необязательное поле, запрет на ввод чисел|

- Корзина (связь с сущностью "Покупатель" типом связи one-to-one и связь с сущностью "Игра" типом связи one-to-many)

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|CartID       |INT(4)          |Первичный ключ  | Обязательное поле, уникальный, авто-инкрементация |
|GameID       |INT(4)          | Внешний ключ к "Game" , для хранения заказанных игр в корзине |Обязательное поле |
|Total price  |INT(16)         | Общая стоимость товаров в корзине |Обязательное поле |

- Администратор

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|AdminID   |INT(4)  | Первичный ключ    |Обязательное поле, уникальный, авто-инкрементация |
|UserID    |INT(4)  | Внешний ключ к "UserBase" , для получения данных основы пользователя (пароль, почта)d|Обязательное поле |

- Игра (связь с сущностью "Корзина" типом связи one-to-many, связь с сущностью "Магазин" типом связи many-to-many, связь с сущностью "Жанр игры" типом связи many-to-many)

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|GameID  |INT(4)  |Первичный ключ     | Обязательное поле, уникальный, авто-инкрементация |
|Price   |INT(16) | Цена игры         |Обязательное поле |
|GenreID |INT(4)  | Внешний ключ к "Жанру игры", для получения жанра игры  | Обязательное поле |

- Магазин (связь с сущностью "Игра" типом связи many-to-many)

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|ShopID          |INT(4)  | Первичный ключ   | Обязательное поле, уникальный, авто-инкрементация |
|Station name    |VARCHAR(64)  | Название станции |Обязательное поле |
|UserID          |INT(4)  | Внешний ключ к "UserBase" , для получения данных основы пользователя (пароль, почта) |Обязательное поле |

- Жанр игры (связь с сущностью "Игра" типом связи many-to-many)
 
| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|GenreID    |INT(4)         |  Первичный ключ   |Обязательное поле, уникальный, авто-инкрементация | 
|GenreName  |VARCHAR(32)    |  Название жанра   |Обязательное поле  |

- Лог пользователя 

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|LogID   |INT(4)      | Первичный ключ    | Обязательное поле, уникальный, авто-инкрементация |
|UserID  |INT(4)      |Внешний ключ к "UserBase", для просмотра того, кем было сделано изменение  |Обязательное поле | 
|LogType |VARCHAR(64) | Вывод типа действия |Обязательное поле | 
|LogMsg  |VARCHAR(64) | Вывод информации о действии |Обязательное поле|