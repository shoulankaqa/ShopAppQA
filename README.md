# ShoulankaQA — Портфолио QA-тестирования

Портфолио Junior QA-инженера. Ручное API и UI тестирование приложения интернет-магазина с планом перехода на автоматизированное тестирование.

---

## О проекте

Комплексное обеспечение качества для e-commerce приложения Shop (API + UI). Работа охватывает полный цикл тестирования: анализ требований, проектирование тестов, выполнение, отчётность об ошибках и трассировка.

**Статус:** 

---

## Структура проекта

```
shoulankaqa/
├── Shop_API/
│   ├── REQUIREMENTS/          # Функциональные и нефункциональные требования
│   ├── TEST_PLANS/            # Тест-планы
│   ├── TEST_CASES/            # Позитивные и негативные тест-кейсы
│   ├── TEST_REPORTS/          # Отчёты по тестированию
│   ├── BUG_REPORTS/           # Баг-репорты с серьёзностью и шагами воспроизведения
│   ├── RTM.md                 # Матрица трассировки требований
│   ├── TEST_DATA/             # Тестовые данные
│   ├── API/                   # Документация API-эндпоинтов
│   ├── AUTOMATION_SCRIPTS/    # Скрипты автоматизации (в разработке)
│   └── CHECKLISTS/            # Чек-листы тестирования
├── ANALYSIS_requirements_review.md  # Анализ пробелов в требованиях
└── README.md
```

---

## Область тестирования

| Модуль | Покрытие |
|--------|----------|
| **Auth** | Регистрация, вход, выход, восстановление пароля |
| **Products** | CRUD, фильтрация, пагинация |
| **Cart** | Добавление/удаление товаров, количество, расчёт итого |
| **Users (Admin)** | CRUD, управление ролями |
| **Wallet** | Баланс, пополнение, списание, история операций |
| **Profile** | Просмотр/редактирование профиля, смена email и пароля |
| **Settings** | Переключение темы, анимация снега, сертификатная авторизация |
| **Нефункциональные** | Производительность, безопасность, кроссбраузерность, доступность |

---

## Результаты тестирования

### Анализ требований
- Функциональные требования по модулям (AUTH, PRODUCTS, CART, USERS, WALLET, PROFILE, SETTINGS)
- Нефункциональные требования (производительность, безопасность, доступность)
- Ревью API-спецификации по документации Swagger

### Тест-кейсы
- **60+ тест-кейсов** в позитивных и негативных сценариях
- Связаны с требованиями через RTM
- Покрытие: Auth (регистрация, вход, выход, восстановление пароля), Products (CRUD, фильтрация), Cart, Profile, Settings

### Баг-репорты
- **20+ баг-репортов** по модулям
- Каждый включает: шаги воспроизведения, ожидаемый/фактический результат, серьёзность, окружение
- Модули: Auth, Cart, Products, Users, Wallet, Settings, Swagger, Common

### Матрица трассировки требований (RTM)
Полная трассировка от требований → тест-кейсов → баг-репортов по всем модулям.

### Тест-планы
Стратегия и планы тестирования, определяющие scope, подход, ресурсы и расписание.

### Отчёты по тестированию
Итоговые отчёты с результатами выполнения тестов, статистикой и выводами.

---

## Инструменты и технологии

![Postman](https://img.shields.io/badge/Postman-FF6C37?logo=postman&logoColor=white&style=flat)
![Swagger](https://img.shields.io/badge/Swagger-85EA2D?logo=swagger&logoColor=black&style=flat)
![JIRA](https://img.shields.io/badge/JIRA-0052CC?logo=jira&logoColor=white&style=flat)
![GitHub](https://img.shields.io/badge/GitHub-181717?logo=github&logoColor=white&style=flat)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white&style=flat)
![Figma](https://img.shields.io/badge/Figma-F24E1E?logo=figma&logoColor=white&style=flat)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black&style=flat)
![Chrome DevTools](https://img.shields.io/badge/DevTools-4285F4?logo=googlechrome&logoColor=white&style=flat)
![TestRail](https://img.shields.io/badge/TestRail-66CC99?style=flat)
![Charles Proxy](https://img.shields.io/badge/Charles%20Proxy-E8533E?style=flat)

---

## Навигация по проекту

- **Новичок в проекте?** Начните с [REQUIREMENTS](Shop_API/REQUIREMENTS/), чтобы понять, что тестируется
- **Нужен тест-план?** Смотрите [TEST_PLANS](Shop_API/TEST_PLANS/) — стратегия и планы тестирования
- **Хотите увидеть тест-кейсы?** Смотрите [TEST_CASES](Shop_API/TEST_CASES/) — структурированные тест-сценарии
- **Интересуют дефекты?** Изучите [BUG_REPORTS](Shop_API/BUG_REPORTS/) — реальные найденные проблемы
- **Хотите увидеть результаты?** Смотрите [TEST_REPORTS](Shop_API/TEST_REPORTS/) — отчёты по итогам тестирования
- **Нужна трассировка?** Откройте [RTM.md](Shop_API/RTM.md) — полное соответствие требований и тестов

---

## Дорожная карта

- [x] Анализ требований и выявление пробелов
- [x] Ручное API тестирование
- [x] Ручное UI тестирование
- [ ] Отчётность об ошибках
- [x] Матрица трассировки требований
- [x] Тест-планы
- [ ] Отчёты по тестированию
- [ ] Автоматизация API тестов (Postman/Newman)
- [ ] Автоматизация UI тестов
- [ ] Интеграция CI/CD

---

## Автор

**Anka** — Junior QA Engineer

[![Codewars](https://www.codewars.com/users/shoulanka/badges/small)](https://www.codewars.com/users/shoulanka)
