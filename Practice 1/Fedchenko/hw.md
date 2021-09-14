# Задание 1

## Условие

Вам поручено разработать онлайн-аукцион. Он позволяет продавцам продавать свои товары с помощью аукциона. Покупатели делают ставки. Выигрывает последняя самая высокая ставка. После закрытия аукциона победитель оплачивает товар с помощью кредитной карты. Продавец отвечает за доставку товара покупателю.
## Функциональные требования

### Аккаунт

1.  Регистрация аккаунта с полями
    -  Никнейм
    -  Электронная почта
    -  Пароль (в хешированном виде)
2. Авторизация с помощью логина и пароля
3. Добавление товара
4. Просмотр списка аукционов
5. Создание аукциона
6. Возможность делать ставки
7. Оплата товара

### Платформа

1. Хранение всех аукционов
2. Отображение аукционов
3. Осуществлять связь продавца и покупателя

### Аукцион

1. Иметь дату начала и конца торгов
2. Отображать статус аукциона 
3. Отображать историю ставок пользователей
4. Отображать текущую ставку
5. Отображать победителя аукциона в случае его завершения

### Товар

1. Добавление описания
2. Возможность добавить фотографии товара
3. Добавление стартовой цены товара
4. Добавление цены мгновенной покупки товара
5. Отображать статус

## Роли пользователей

Продукт должен иметь следующие роли пользователей:
1. Обычный пользователь
2. Администратор

Обычный пользователь должен иметь возможность выступать как в роли покупателя, так и в роли продавца товаров.

## Объекты

1.  Пользователь:
    - ID пользователя
    - Никнейм пользователя
    - Электронная почта
    - Пароль
	- Активен ли аккаунт пользователя (удален или нет)
	
2.  Кредитная карта:
    - ID карты
    - Номер карты
    - ID аккаунта владельца карты
    - Имя и фамилия владельца карты латиницей
    - Срок действия карты
    - Активна ли карта 
   
3.  Товар:
    - ID товара
    - ID аккаунта владельца товара
    - Описание 
    - Начальная цена
    - Цена мгновенной покупки
    - Статус

4.  Аукцион:
    - ID аукциона
    - ID товара
    - ID нынешней ставки
    - Минимальное повышение ставки
    - Дата начала аукциона
    - Дата конца аукциона
    - Статус аукциона
    - ID аккаунта победителя аукциона

5.  Ставка:
    - ID ставки
    - ID аккаунта пользователя, делающего ставку
    - ID аукциона, на котором делается ставка
    - Сумма ставки
    - Дата/время ставки
   
6.  Изображение:
    - ID фотографии
    - URL-ссылка на изображение
    - ID товара, к которому привязана фотография

## Связи между объектами
#### Один к одному

1. Пользователь - Аукцион
2. Товар - Аукцион
3. Ставка - Аукцион

#### Один ко многим:

1. Пользователь - Карта
2. Пользователь - Товар
3. Товар - Изображение
4. Аукцион - Ставка
5. Пользователь - Ставка

## Схема
[Ссылка на схему](https://drawsql.app/sevets/diagrams/auction#)

![schema](schema.png)