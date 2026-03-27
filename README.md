# Laravel 12 + Inertia.js + shadcn-vue CRUD Example

A complete CRUD example using Laravel 12, Inertia.js, Vue 3, and shadcn-vue components.

## Stack

- **Backend**: Laravel 12
- **Frontend**: Vue 3 + Inertia.js
- **UI Components**: shadcn-vue (with Radix Vue)
- **Styling**: Tailwind CSS
- **Language**: TypeScript

## Features

- Full CRUD for **Posts** (Create, Read, Update, Delete)
- Post attributes: Title, Content, Published/Draft status
- Beautiful UI with shadcn-vue components
- Form validation with inline error messages
- Confirmation dialog before deleting
- Flash messages for success actions
- Responsive layout

## Prerequisites

- PHP 8.2+
- Composer
- Node.js 18+
- npm or pnpm

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/andreicvasniuc05/test-crud.git
   cd test-crud
   ```

2. **Install PHP dependencies**
   ```bash
   composer install
   ```

3. **Install Node.js dependencies**
   ```bash
   npm install
   ```

4. **Set up environment**
   ```bash
   cp .env.example .env
   php artisan key:generate
   ```

5. **Set up database** (SQLite by default)
   ```bash
   touch database/database.sqlite
   php artisan migrate
   ```

6. **Start development servers**
   ```bash
   # In terminal 1 - Laravel
   php artisan serve
   
   # In terminal 2 - Vite (frontend)
   npm run dev
   ```

7. **Open your browser** at [http://localhost:8000](http://localhost:8000)

## Project Structure

```
├── app/
│   ├── Http/Controllers/PostController.php  # CRUD controller
│   └── Models/Post.php                       # Post model
├── database/migrations/                      # Database migrations
├── resources/
│   ├── css/app.css                           # Tailwind + CSS variables
│   ├── js/
│   │   ├── app.ts                            # Inertia app entry
│   │   ├── lib/utils.ts                      # Utility functions (cn)
│   │   ├── Components/ui/                    # shadcn-vue components
│   │   ├── Layouts/AppLayout.vue             # App layout
│   │   └── Pages/Posts/                      # CRUD pages
│   └── views/app.blade.php                   # Blade template
├── routes/web.php                            # Routes
└── vite.config.ts                            # Vite configuration
```

## Available Routes

| Method | URL | Action |
|--------|-----|--------|
| GET | `/posts` | List all posts |
| GET | `/posts/create` | Show create form |
| POST | `/posts` | Store new post |
| GET | `/posts/{id}/edit` | Show edit form |
| PUT | `/posts/{id}` | Update post |
| DELETE | `/posts/{id}` | Delete post |

## License

MIT