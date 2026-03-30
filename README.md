# User Management Application

A Laravel 9 web application for authenticated user administration. The project includes built-in Laravel authentication and a protected user management module to create, edit, list, and delete users.

## Core Technologies

- **Laravel 9 + PHP 8**: MVC web framework and application runtime.
- **Laravel UI**: server-rendered authentication scaffolding (login/register/reset password).
- **Blade templates**: UI rendering for auth screens and user CRUD pages.
- **Eloquent ORM**: database interaction for the `users` table.
- **Form Request validation**: centralized validation rules for create/update flows.

## Key Features

- **Authentication & route protection**: only logged-in users can access user management pages.
- **User CRUD workflow**: create, list (paginated), edit, and soft delete users from the interface.
- **Validation-first forms**:
  - Create: required `name`, `email` (unique), `address`, and `password` (min 6).
  - Update: required `name`, `email` (unique except current record), and `address`.
- **Password hashing**: passwords are securely hashed before saving.
- **Session flash messages**: success notifications after create/update/delete actions.

## Environment Requirements

- PHP **8.0.2+**
- Composer
- A relational database supported by Laravel (e.g., MySQL/MariaDB/PostgreSQL)
- Node.js + npm (optional, if you need to rebuild frontend assets)

## Installation & Run

```bash
# 1) Install PHP dependencies
composer install

# 2) Create environment file
cp .env.example .env

# 3) Generate app key
php artisan key:generate

# 4) Configure DB credentials in .env, then run migrations
php artisan migrate

# 5) (Optional) seed data
php artisan db:seed

# 6) Start local server
php artisan serve
```

Open the app at `http://127.0.0.1:8000`.

## Environment Variables

Create a `.env` file in the project root and configure at minimum:

```env
APP_NAME="Laravel User Management"
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://127.0.0.1:8000

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_user_management
DB_USERNAME=root
DB_PASSWORD=
```

> The application will not run correctly without a valid `APP_KEY` and working database connection.

## Main Directory Structure

```text
app/
├── Http/
│   ├── Controllers/      # HomeController, UserController, auth controllers
│   └── Requests/         # CreateUserRequest, UpdateUserRequest
├── Models/               # Eloquent models (User)

database/
├── migrations/           # Database schema migrations
├── factories/
└── seeders/

resources/
├── views/
│   ├── auth/             # Authentication screens
│   ├── users/            # User CRUD screens
│   └── layouts/

routes/
└── web.php               # Web routes (auth + user management)
```

## Conventions & Best Practices

- Keep validation logic in **Form Request** classes instead of controllers.
- Keep business/data flow in controllers/services, not in Blade views.
- Always hash passwords before persistence (already handled in `UserController`).
- Protect sensitive routes with middleware (`auth`).
- Never commit real secrets in `.env`.

## Testing & Code Quality

```bash
# Run unit/feature tests
php artisan test

# (Alternative)
./vendor/bin/phpunit
```

## Route Summary

- `GET /` → welcome page
- Auth routes via `Auth::routes()`
- `GET /home` → dashboard/home
- Protected user routes (prefix: `/users`):
  - `GET /users` → list users
  - `GET /users/create` → create form
  - `POST /users/store` → create user
  - `GET /users/{id}/edit` → edit form
  - `PUT /users/{id}/update` → update user
  - `DELETE /users/{id}/destroy` → delete user

