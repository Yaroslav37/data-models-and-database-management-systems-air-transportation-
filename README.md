<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
</head>
<body>
    <h1>Тема: Авиаперевозки</h1>
    <p>ФИО: Миненков Ярослав Александрович</p>
    <p>Номер группы: 153502</p>
    <h2>Функциональные требования</h2>
    <ol>
        <li>Авторизация и управление пользователями
            <ul>
                <li>Регистрация новых пользователей с указанием имени, фамилии, адреса электронной почты и пароля</li>
                <li>Вход в систему с использованием логина и пароля</li>
            </ul>
        </li>
        <li>Управление пользователями (CRUD):
            <ul>
                <li>Создание новых пользователей с указанием основной информации</li>
                <li>Просмотр информации о пользователях</li>
                <li>Редактирование данных пользователя</li>
                <li>Удаление данных пользователя</li>
            </ul>
        </li>
        <li>Система ролей:
            <ul>
                <li>Определение различных ролей пользователей (например, администратор, сотрудник авиакомпании, клиент и т.д.)</li>
                <li>Привязка ролей к пользователям</li>
                <li>Управление правами доступа на основе ролей</li>
            </ul>
        </li>
        <li>Журналирование действий пользователя:
            <ul>
                <li>Регистрация всех действий, совершаемых пользователями в системе</li>
                <li>Запись даты, времени и идентификатора пользователя при каждом действии</li>
            </ul>
        </li>
        <li>Бронирование билетов:
            <ul>
                <li>Регистрация всех действий, совершаемых пользователями в системе</li>
                <li>Указания информации о пассажирах, включая их имена и номера документов</li>
            </ul>
        </li>
        <li>Выдача посадочных талонов:
            <ul>
                <li>Поддержка возможности регистрации пассажиров на рейсы, указанные в их билетах</li>
                <li>Генерация уникального посадочного талона с информацией о месте в самолете</li>
            </ul>
        </li>
        <li>Управление авиарейсами:
            <ul>
                <li>Добавление новых авиарейсов с указанием маршрута, даты и времени вылета и прилета, доступных мест</li>
                <li>Просмотр и редактирование информации о существующих авиарейсах</li>
                <li>Отмена или изменение расписания авиарейсов</li>
            </ul>
        </li>
        <li>Управление билетами:
            <ul>
                <li>Генерация уникального номера для каждого билета</li>
                <li>Просмотр информации о билетах в рамках конкретного бронирования</li>
            </ul>
        </li>
        <li>Управление моделями самолетов:
            <ul>
                <li>Хранение информации о моделях самолетов, их компоновках салона и распределении мест</li>
                <li>Возможность добавления новых моделей самолетов и обновления информации о существующих</li>
            </ul>
        </li>
    </ol>
    <h2>Описание сущностей БД</h2>
    <h3>Пользователь (Users):</h3>
    <ul>
        <li>user_id (Идентификатор пользователя): INT (Primary Key)</li>
        <li>role_id (Идентификатор роли): INT (Foreign Key)</li>
        <li>first_name (Имя): VARCHAR</li>
        <li>last_name (Фамилия): VARCHAR</li>
        <li>email (Адрес электронной почты): VARCHAR (уникальное значение)</li>
        <li>password (Пароль): VARCHAR (хешированный пароль)</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений</p>
        <p>Связи: Связь с сущностью Role (пользователь) Many-to-One, Booking One-to-Many.</p>
    </ul>
    <h3>Роль (Roles):</h3>
    <ul>
        <li>role_id (Идентификатор роли): INT (Primary Key)</li>
        <li>role_name (Название роли): VARCHAR (уникальное значение)</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: Связь с сущностью User (пользователь) One-to-Many, Booking One-to-Many.</p>
    </ul>
    <h3>Журнал действий пользователя (UserActionLogs):</h3>
    <ul>
        <li>action_id (Идентификатор действия): INT (Primary Key)</li>
        <li>user_id (Идентификатор пользователя): INT (Foreign Key)</li>
        <li>action_date_time (Дата и время действия): DATETIME</li>
        <li>action_description (Описание действия): VARCHAR</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: Связь с сущностью User (пользователь) Many-to-One.</p>
    </ul>
    <h3>Бронирование билетов (Bookings):</h3>
    <ul>
        <li>booking_id (Идентификатор бронирования): INT (Primary Key)</li>
        <li>created_date_time (Дата и время создания): DATETIME</li>
        <li>status (Статус бронирования): VARCHAR</li>
        </br>
        <li>user_id (Идентификатор пользователя): INT (Foreign Key) - пользователь, создавший бронирование</li>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: </p>
    </ul>
    <h3>Билет (Tickets):</h3>
    <ul>
        <li>ticket_id (Идентификатор билета): INT (Primary Key)</li>
        <li>booking_id (Идентификатор бронирования): INT (Foreign Key) - связывает билет с бронированием</li>
        <li>ticket_number (Уникальный номер билета): VARCHAR (уникальный номер билета)</li>
        <li>passenger_info (Информация о пассажире): JSON или другой формат данных для хранения информации о пассажире</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: Связь с сущностью Booking (бронирование) Many-to-One, с TicketFlights One-to-Many (по желанию).</p>
    </ul>
    <h3>Посадочный талон (BoardingPasses):</h3>
    <ul>
        <li>boarding_pass_id (Идентификатор посадочного талона): INT (Primary Key)</li>
        <li>ticket_id (Идентификатор билета): INT (Foreign Key) - связывает посадочный талон с билетом</li>
        <li>seat_info (Информация о месте в самолете): VARCHAR (информация о месте в самолете)</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: Связь с сущностью Ticket (билет) Many-to-One.</p>
    </ul>
    <h3>Авиарейс (Flights):</h3>
    <ul>
        <li>flight_id (Идентификатор рейса): INT (Primary Key)</li>
        <li>departure_airport_id (Идентификатор аэропорта отправления): INT (Foreign Key) - связывает рейс с аэропортом отправления</li>
        <li>arrival_airport_id (Идентификатор аэропорта назначения): INT (Foreign Key) - связывает рейс с аэропортом назначения</li>
        <li>departure_datetime (Дата и время вылета): DATETIME</li>
        <li>arrival_datetime (Дата и время прилета): DATETIME</li>
        <li>available_seats (Количество доступных мест): INT</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: Связь с сущностью Airport Many-to-One, TicketFlights One-to-Many (по желанию).</p>
    </ul>
    </ul>
    <h2>Схема БД</h2>
    <img src="https://github.com/Yaroslav37/data-models-and-database-management-systems-air-transportation-/assets/94055866/8406b919-9654-49ed-8d5e-102377b26769" alt="схема БД">

</body>
</html>


