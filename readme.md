# Глеб Буткевич 053503
## 1. Тема: Интернет-магазин с играми
## 2. Функциональные требования к проекту:
### Роли пользователей:
1. Покупатель
2. Администратор
### Авторизация пользователя
Пользователь должнен иметь возможность:
- Зарегистрироваться.
- Войти в аккаунт, выйти.
- Восстановить пароль
### Возможности пользователей
- Администратор
    + Создать, просмотреть, удалить, отредактировать игры
    + Создать, просмотреть, удалить, отредактировать любого пользователя
    + Просмотр действий покупателей и магазинов

- Покупатель
    + Просмотреть, добавить в заказ, удалить из заказа игры
    + Журналивароние действий

## 3. Список сущностей БД:
- Основа пользователя
- Покупатель
- Администратор
- Заказ
- Игра
- Жанр игры
- Издатель игры
- Лог пользователя

## 4. Схематично изобразить не нормальзованную схему БД:
![image](https://user-images.githubusercontent.com/38133117/200854103-82f2c99d-a7a5-44f1-bd00-be8571852c4c.png)



## 5. Описать каждую сущность:

- Основа пользователя (связь с сущностями "Администратор", "Покупатель" типа one-to-one)

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|UserID        |INT(4) | Первичный ключ | Обязательное поле, уникальный, авто-инкрементация        |
|Email         | VARCHAR(32)    | Почта пользователя      | Обязательное поле, уникальный  |
|Password      | VARCHAR(32)    | Пароль пользователя     | Обязательное поле              |

- Покупатели (связь с сущностью "Заказ" типом связи one-to-many)

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|CustomerID|INT(4)        | Первичный ключ      | Обязательное поле, уникальный, авто-инкрементация              |
|UserID    |INT(4)        | Внешний ключ к "UserBase" , для получения данных основы пользователя (пароль, почта) |Обязательное поле|

- Заказ (связь с сущностью "Покупатель" типом связи one-to-many и связь с сущностью "Игра" типом связи one-to-many)

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|OrderID       |INT(4)          |Первичный ключ  | Обязательное поле, уникальный, авто-инкрементация |
|GameID       |INT(4)          | Внешний ключ к "Game" , для хранения заказанных игр |Обязательное поле |
|CustomerID   |INT(4)          | Внешний ключ к "Customer" , для хранения ID заказавшего пользователя |Обязательное поле |
|Total price  |INT(16)         | Общая стоимость товаров в заказе |Обязательное поле |
|Date         |INT(16)         | Дата совершения заказа |Обязательное поле |

- Администратор

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|AdminID   |INT(4)  | Первичный ключ    |Обязательное поле, уникальный, авто-инкрементация |
|UserID    |INT(4)  | Внешний ключ к "UserBase" , для получения данных основы пользователя (пароль, почта) |Обязательное поле |

- Игра (связь с сущностью "Заказ" типом связи one-to-many, связь с сущностью "Издатель игры" типом связи many-to-many, связь с сущностью "Жанр игры" типом связи many-to-many)

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|GameID  |INT(4)  |Первичный ключ     | Обязательное поле, уникальный, авто-инкрементация |
|Price   |INT(16) | Цена игры         |Обязательное поле |
|GameName  |VARCHAR(128)    |  Название игры   |Обязательное поле  |
|GenreID |INT(4)  | Внешний ключ к "Жанру игры", для получения жанра игры  | Обязательное поле |
|PublisherID |INT(4)  | Внешний ключ к "Издателю игры", для получения издателя игры  | Обязательное поле |

- Жанр игры (связь с сущностью "Игра" типом связи many-to-many)
 
| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|GenreID    |INT(4)         |  Первичный ключ   |Обязательное поле, уникальный, авто-инкрементация | 
|GenreName  |VARCHAR(32)    |  Название жанра игры   |Обязательное поле  |

- Издатель игры (связь с сущностью "Игра" типом связи many-to-many)
 
| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|PublisherID    |INT(4)         |  Первичный ключ   |Обязательное поле, уникальный, авто-инкрементация | 
|PublisherName  |VARCHAR(32)    |  Название компании издателя   |Обязательное поле  |

- Лог пользователя 

| Имя поля | Тип    | Описание  | Ограничения   |
|----------|---------|---------|---------------|
|LogID   |INT(4)      | Первичный ключ    | Обязательное поле, уникальный, авто-инкрементация |
|UserID  |INT(4)      |Внешний ключ к "UserBase", для просмотра того, кем было сделано изменение  |Обязательное поле | 
|LogType |VARCHAR(64) | Вывод типа действия |Обязательное поле | 
|LogMsg  |VARCHAR(64) | Вывод информации о действии |Обязательное поле|
