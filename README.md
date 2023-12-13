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
                <li>Определение различных ролей пользователей (администратор, клиент)</li>
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
        <li>Покупка билетов:
            <ul>
                <li>Регистрация всех покупок, совершаемых пользователями в системе</li>
                <li>Указания информации о пассажирах</li>
            </ul>
        </li>
        <li>Управление авиарейсами:
            <ul>
                <li>Добавление новых авиарейсов с указанием маршрута, даты и времени вылета и прилета, доступных мест</li>
                <li>Просмотр и редактирование информации о существующих авиарейсах</li>
                <li>Изменение расписания авиарейсов</li>
            </ul>
        </li>
        <li>Управление билетами:
            <ul>
                <li>Генерация уникального номера для каждого билета</li>
                <li>Просмотр информации о билетах пользователями</li>
            </ul>
        </li>
        <li>Управление моделями самолетов:
            <ul>
                <li>Хранение информации о моделях самолетов, их количества мест</li>
                <li>Возможность добавления новых моделей самолетов</li>
            </ul>
        </li>
    </ol>
    <h2>Описание сущностей БД</h2>
    <h3>Пользователь (Users):</h3>
    <ul>
        <li>user_id (Идентификатор пользователя): INT (Primary Key)</li>
        <li>role_id (Идентификатор роли): INT (Foreign Key)</li>
        <li>ticket_id (Идентификатор билета): (Foreign Key)</li>
        <li>first_name (Имя): VARCHAR</li>
        <li>last_name (Фамилия): VARCHAR</li>
        <li>email (Адрес электронной почты): VARCHAR (уникальное значение)</li>
        <li>password (Пароль): VARCHAR (хешированный пароль)</li>
        </br>
        <p>Ограничения: Email является уникальным</p>
        <p>Связи: Связь с сущностью Role (пользователь) Many-to-One, Ticket One-to-Many(optional).</p>
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
    <h3>Билет (Tickets):</h3>
    <ul>
        <li>ticket_id (Идентификатор билета): INT (Primary Key)</li>
        <li>ticket_number (Уникальный номер билета): VARCHAR (уникальный номер билета)</li>
        </br>
        <p>Ограничения:  Уникальность номера билета</p>
        <p>Связи: Связь с сущностью User Many-to-One, с TicketFlights One-to-Many (optional), с BoardingPasses One-to-Many(optional).</p>
    </ul>
    <h3>Посадочный талон (BoardingPasses):</h3>
    <ul>
        <li>boarding_pass_id (Идентификатор посадочного талона): INT (Primary Key)</li>
        <li>ticket_id (Идентификатор билета): INT (Foreign Key) - связывает посадочный талон с билетом</li>
        <li>seat_info (Информация о месте в самолете): VARCHAR (информация о месте в самолете)</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: Связь с сущностью Ticket (билет) Many(optional)-to-One.</p>
    </ul>
    <h3>Авиарейс (Flights):</h3>
    <ul>
        <li>flight_id (Идентификатор рейса): INT (Primary Key)</li>
        <li>aircraft_model_id (Идентификатор модели самолета): Уникальный целочисленный идентификатор (Foreign Key)</li>
        <li>departure_airport_id (Идентификатор аэропорта отправления): INT (Foreign Key) - связывает рейс с аэропортом отправления</li>
        <li>arrival_airport_id (Идентификатор аэропорта назначения): INT (Foreign Key) - связывает рейс с аэропортом назначения</li>
        <li>flight_no (Номер рейса): INT</li>
        <li>sheвuled_departure_datetime (Дата и время вылета по расписанию): DATETIME</li>
        <li>sheduled_arrival_datetime (Дата и время прилета по расписанию): DATETIME</li>
        <li>actual_departure_datetime (Дата и время вылета фактическое): DATETIME</li>
        <li>actual_arrival_datetime (Дата и время прилета фактическое): DATETIME</li>
        </br>
        <p>Ограничения:  Фактическое время не может быть раньше запланированного времени.</p>
        <p>Связи: Связь с сущностью Airports Many-to-Many, TicketFlights One-to-Many, Aircrafts One-to-One.</p>
    </ul>
    <h3>Модель самолета (AircraftModels):</h3>
    <ul>
        <li>aircraft_model_id (Идентификатор модели самолета): Уникальный целочисленный идентификатор (Primary Key)</li>
        <li>model_name (Название модели): Строка</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: Связь с сущностью Seats(места) One-to-Many, Flights One-to-One</p>
    </ul>
    <h3>Места (Seats):</h3>
    <ul>
        <li>aircraft_model_id (Идентификатор модели самолета): INT (Foreign Key)</li>
        <li>seat_no (Номер посадочного места): INT</li>
        <li>is_availible (информация о доступности): BOOL</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: Связь с сущностью Aircrafts Many-to-One</p>
    </ul>
    <h3>Аэропорт (Airports):</h3>
    <ul>
        <li>airport_id (Идентификатор Аэропорта): INT (Primary Key)</li>
        <li>airport_name (Название аэропорта): VARCHAR</li>
        <li>city (название города): VARCHAR</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: Связь с сущностью Flights Many-to-Many</p>
    </ul>
    <h3>Перелеты (TicketFlights):</h3>
    <ul>
        <li>ticket_id (Идентификатор билета): INT (Foreign Key)</li>
        <li>flight_id (Идентификатор рейса): INT (Foreign Key)</li>
        <li>amount (количество перелетов): INT</li>
        </br>
        <p>Ограничения: Нет дополнительных ограничений.</p>
        <p>Связи: Связь с сущностью Flights Many-to-One, Tickets Many-to-One</p>
    </ul>
    <h2>Схема БД</h2>
    <img src="https://github.com/Yaroslav37/data-models-and-database-management-systems-air-transportation-/assets/94055866/3a8f3c30-e51a-40db-8e3f-a516d4fbb18e" alt="схема БД">

</body>
</html>


