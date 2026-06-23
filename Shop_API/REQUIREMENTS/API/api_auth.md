## API_AUTH_001 — Регистрация пользователя

1.1. Назначение: самостоятельная регистрация нового пользователя в системе.

1.2. Метод и URL:
- POST /register

1.3. Доступ:
- Метод доступен без авторизации.
- Access-токен не требуется.

1.4. Запрос:
- Content-Type: application/json.
- Обязательные поля: username, password.

1.4.1. Поле username:
- Обязательно.
- Тип: string.
- Должно быть уникальным в системе.
- Длина: от 6 до 32 символов.
- Допустимые символы: a-z, 0-9, _, начинается с буквы.
- Запрещены логины, начинающиеся на admin, user или seller.
- Пробелы и другие спецсимволы не допускаются.

1.4.2. Поле password:
- Обязательно.
- Тип: string.
- Должно соответствовать требованиям REQ_AUTH_001.
- Минимальные правила:
  - длина от 8 до 64 символов;
  - только английские буквы (A-Z, a-z), цифры (0-9) и символы ($!^@?);
  - хотя бы одна заглавная буква (A-Z);
  - хотя бы одна цифра (0-9);
  - хотя бы один специальный символ ($!^@?);
  - минимум 4 буквы всего.
- Пробелы в начале и в конце не допускаются.

1.4.3. Ограничения:
- Пользователь не может обходить требования к username и password.
- Регистрация через этот endpoint не должна позволять выбрать роль `admin` или `seller`.

1.5. Пример запроса:
```http
POST /register HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "username": "john_doe",
  "password": "Password1!"
}
```

1.6. Успех:
- 201 Created.
- Ответ соответствует Swagger-схеме `User`.
- По умолчанию создаётся пользователь с ролью `user`.

1.7. Пример успешного ответа:
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": "1",
  "username": "john_doe",
  "role": "user"
}
```

1.8. Ошибки:
- 1.8.1. 400 Bad Request — отсутствует обязательное поле.
- 1.8.2. 400 Bad Request — нарушены правила валидации username.
- 1.8.3. 400 Bad Request — нарушены правила валидации password.
- 1.8.4. 400 Bad Request — пользователь уже существует.
- 1.8.5. 500 Internal Server Error — внутренняя ошибка сервера.

1.9. Особые условия:
- После успешной регистрации пользователь должен иметь возможность авторизоваться через `/login` с указанными `username` и `password`.


## API_AUTH_002 — Авторизация пользователя

2.1. Назначение: авторизация пользователя по логину и паролю с выдачей `access_token`, `refresh_token` и данных пользователя.

2.2. Метод и URL:
- POST /login

2.3. Доступ:
- Метод доступен без предварительной авторизации.
- Access-токен не требуется.

2.4. Запрос:
- Content-Type: application/json.
- Обязательные поля: username, password.
- Пара `username` + `password` должна совпадать с существующей учётной записью.
- Для удалённых пользователей авторизация должна отклоняться.

2.5. Пример запроса:
```http
POST /login HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "username": "john_doe",
  "password": "Password1!"
}
```

2.6. Успех:
- 200 OK.
- Ответ содержит `access_token`, `refresh_token` и `user`.

2.7. Пример успешного ответа:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "access_token": "eyJhbGciOi...",
  "refresh_token": "eyJhbGciOi...",
  "user": {
    "id": "1",
    "username": "john_doe",
    "email": "john@example.com",
    "role": "user"
  }
}
```

2.8. Ошибки:
- 2.8.1. 400 Bad Request — некорректный формат тела запроса.
- 2.8.2. 400 Bad Request — отсутствует username.
- 2.8.3. 400 Bad Request — отсутствует password.
- 2.8.4. 401 Unauthorized — неверные учётные данные.
- 2.8.5. 500 Internal Server Error — внутренняя ошибка сервера.

2.9. Особые условия:
- `access_token` должен подходить для доступа к защищённым endpoint’ам.
- `refresh_token` должен использоваться для получения нового `access_token`.
- При нескольких успешных авторизациях все выданные `refresh_token` остаются валидными до истечения срока или инвалидции.


## API_AUTH_003 — Обновление access token

3.1. Назначение: выдача нового `access_token` по действующему `refresh_token` без повторного ввода логина и пароля.

3.2. Метод и URL:
- POST /refresh

3.3. Доступ:
- Метод доступен без заголовка `Authorization`.
- Авторизация выполняется по `refresh_token` в теле запроса.

3.4. Запрос:
- Content-Type: application/json.
- Обязательное поле: `refresh_token`.
- `refresh_token` должен быть действующим и ранее выданным.

3.5. Пример запроса:
```http
POST /refresh HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "refresh_token": "eyJhbGciOi..."
}
```

3.6. Успех:
- 200 OK.
- Ответ содержит новый `access_token`.

3.7. Пример успешного ответа:
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "access_token": "eyJhbGciOi..."
}
```

3.8. Ошибки:
- 3.8.1. 400 Bad Request — отсутствует `refresh_token`.
- 3.8.2. 400 Bad Request — некорректный формат тела запроса.
- 3.8.3. 401 Unauthorized — `refresh_token` недействителен.
- 3.8.4. 401 Unauthorized — `refresh_token` истёк.
- 3.8.5. 401 Unauthorized — `refresh_token` отозван.
- 3.8.6. 401 Unauthorized — `refresh_token` не принадлежит пользователю.
- 3.8.7. 500 Internal Server Error — внутренняя ошибка сервера.

3.9. Особые условия:
- Новый `access_token` должен быть валиден для всех защищённых endpoint’ов.


## API_AUTH_004 — Выход пользователя

4.1. Назначение: выход пользователя из системы через инвалидцию текущего `refresh_token`.

4.2. Метод и URL:
- POST /logout

4.3. Доступ:
- Метод доступен только авторизованным пользователям.
- Требуется валидный `access_token` в заголовке `Authorization: Bearer <access_token>`.

4.4. Запрос:
- Тело запроса отсутствует.

4.5. Успех:
- 204 No Content.
- `refresh_token` текущего пользователя удаляется или инвалидируется.
- Дальнейшие запросы на `/refresh` с этим `refresh_token` завершаются ошибкой 401.
- Поведение `access_token` определяется общей политикой токенов.

4.6. Ошибки:
- 4.6.1. 401 Unauthorized — отсутствует access_token.
- 4.6.2. 401 Unauthorized — access_token некорректный.

4.7. Особые условия:
- Если `refresh_token` уже отсутствует, logout всё равно возвращает 204 No Content.
- Метод влияет только на токены текущего пользователя и не должен затрагивать `refresh_token` других пользователей.