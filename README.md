## api_yamdb

# Описание
Проект **YaMDb** собирает отзывы пользователей на произведения.
Произведения (***Titles***) делятся на категории (***Cathegories***): «Книги», «Фильмы», «Музыка»; и могут относиться к различным жанрам (***Genres***).
Аутентифицированные пользователи могут оставлять оценки (***Reviews***) с комментариями (***Comments***) к выбранным произведениям.

# Алгоритм регистрации пользователей
1. Пользователь отправляет запрос с параметром `email` на `/auth/email/`.
2. **YaMDB** отправляет письмо с кодом подтверждения (`confirmation_code`) на адрес  `email` .
3. Пользователь отправляет запрос с параметрами `email` и `confirmation_code` на `/auth/token/`, в ответе на запрос ему приходит `token` (JWT-токен).
4. При желании пользователь отправляет PATCH-запрос на `/users/me/` и заполняет поля в своём профайле (описание полей — в документации).

# Пользовательские роли
- **Аноним** — может просматривать описания произведений, читать отзывы и комментарии.
- **Аутентифицированный пользователь** — может, как и **Аноним**, читать всё, дополнительно он может публиковать отзывы и ставить рейтинг произведениям (фильмам/книгам/песенкам), может комментировать чужие отзывы и ставить им оценки; может редактировать и удалять **свои** отзывы и комментарии.
- **Модератор** — те же права, что и у **Аутентифицированного пользователя** плюс право удалять **любые** отзывы и комментарии.
- **Администратор** — полные права на управление проектом и всем его содержимым. Может создавать и удалять категории и произведения. Может назначать роли пользователям.
- **Администратор Django** — те же права, что и у роли **Администратор**.

# Пути для работы с API
Запросы к API начинаются с `/api/v1/`

**Произведения** - `/titles/`, `/titles/<title_id>/`
**Оценка** - `/titles/<title_id>/review/`, `/titles/<title_id>/review/<review_id>/`
**Комментарии** - `/titles/<title_id>/review/<review_id>/comment/`, `/titles/<title_id>/review/<review_id>/comment/<comment_id>/`
**Категории** - `/cathegories/`
**Произведениям** - `/genres/`

Подробное описание API приводится по адресу: `/static/redoc.yaml`
