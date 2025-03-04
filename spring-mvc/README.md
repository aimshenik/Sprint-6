Необходимо сформировать проект с использованием зависимостей **spring web** и **thymeleaf**. 

Для этого можно воспользоваться https://start.spring.io

Проект должен содержать следующие реализации:

1) минимум **один сервлет** (функционал может быть любой, но предлагаю реализовать форму аутентификации)
2) минимум **два фильтра** (логирование и проверка аутентификации)
3) реализацию **контроллера mvc** (реализация с использованием представлений)
4) реализацию **контроллера rest** (json api вашего приложения)

Тема приложения - **адресная книга** в которой можно выполнять следующие функции:
1) Добавление и редактирование записей
2) Просмотр записей
3) Поиск записей
4) Простая аутентификация

Необходимо реализовать минимальное подобие аутентификации **без применения spring security**, что бы к основным ресурсам приложения был доступ 
только после ввода заранее определенной пары логин-пароль. 

Для этого можно воспользоваться следующим алгоритмом: 

1) получаем логин и пароль из формы
2) если они соответствуют сохраненной паре логин-пароль, добавляем **Cookie** с именем **auth** и временем входа

Далее при обращении к защищенным ресурсам, производим проверку в фильтре наличия Cookie с именем auth и проверяем, что время в этом значении меньше текущего. 
Eсли Cookie отсутствует или имеет неверное значение - делаем redirect на форму входа.

Таким образом, для ориентира можно использовать следующую структуру ресурсов приложения:
- /login форма входа **только публичный доступ**, остальные ресурсы будут только аутентифицированный доступ
- /app/add добавление записи
- /app/list просмотр записей и поиск если будет переданы query параметры запроса
- /app/{id}/view просмотр конкретной записи
- /app/{id}/edit редактирование конкретной записи
- /app/{id}/delete удаление конкретной записи
- /api/... с теми же действиями, но только будет применяться json для запроса и ответов.

Так же необходимо вести журнал поступающих запросов.  

В качестве базы данных для хранимых записей можно использовать ConcurrentHashMap. Бизнес-логику не стоит усложнять, в данном задании делаем упор на работу с веб-слоем (spring mvc).

Необходимо покрыть интеграционными тестами полученное приложение. Для mvc контроллеров можно воспользоваться **MockMvc** подходом. 
Для rest контроллеров и аутентификации воспользоваться подходом с **TestRestTemplate** и обращениями к локальному серверу.