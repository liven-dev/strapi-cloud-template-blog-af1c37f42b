# Strapi App (Temporary Test Repository)

This is a Strapi v5 application used for testing and demos. It includes a small example dataset and media assets you can import via a provided seeding script. Note: this repository is temporary and may be removed.

## Requirements
- Node.js 18.x–22.x (see `package.json` engines)
- npm (or yarn)

## Quick start
```bash
# Install dependencies
npm install

# Start in development mode (auto-reload)
npm run develop

# Build admin panel (for production)
npm run build

# Start in production mode
npm run start
```

Once running in development, open the admin at http://localhost:1337/admin and create the first admin user when prompted.

## Scripts
- `npm run develop`: Start Strapi with auto-reload
- `npm run start`: Start Strapi without auto-reload
- `npm run build`: Build the admin panel
- `npm run deploy`: Strapi Cloud deploy helper (optional)
- `npm run seed:example`: Run the example data importer

## Example data seeding
This project ships with an example dataset (articles, authors, categories, global settings, and about page) and media files in `data/`.

To import the example content:
```bash
npm run seed:example
```
Notes:
- The seeder runs a one-time guard using Strapi’s store. If you need to re-seed on SQLite, stop the server and delete the database file `.tmp/data.db`, then run the seed again.
- On Postgres/MySQL, clear the database (or drop relevant tables) before re-running the seed.

## Environment variables
Create a `.env` file in the project root. Below is a minimal example for local development with SQLite:
```env
# Server
HOST=0.0.0.0
PORT=1337
APP_KEYS=your-app-key-1,your-app-key-2,your-app-key-3,your-app-key-4
WEBHOOKS_POPULATE_RELATIONS=false

# Admin / tokens
ADMIN_JWT_SECRET=your-admin-jwt-secret
API_TOKEN_SALT=your-api-token-salt
TRANSFER_TOKEN_SALT=your-transfer-token-salt
FLAG_NPS=true
FLAG_PROMOTE_EE=true

# Database (SQLite default)
DATABASE_CLIENT=sqlite
DATABASE_FILENAME=.tmp/data.db
DATABASE_CONNECTION_TIMEOUT=60000
```

### Postgres example
```env
DATABASE_CLIENT=postgres
DATABASE_URL=postgres://USER:PASSWORD@HOST:5432/DB_NAME
DATABASE_HOST=HOST
DATABASE_PORT=5432
DATABASE_NAME=DB_NAME
DATABASE_USERNAME=USER
DATABASE_PASSWORD=PASSWORD
DATABASE_SCHEMA=public
DATABASE_SSL=false
DATABASE_POOL_MIN=2
DATABASE_POOL_MAX=10
```

### MySQL example
```env
DATABASE_CLIENT=mysql
DATABASE_HOST=HOST
DATABASE_PORT=3306
DATABASE_NAME=DB_NAME
DATABASE_USERNAME=USER
DATABASE_PASSWORD=PASSWORD
DATABASE_SSL=false
DATABASE_POOL_MIN=2
DATABASE_POOL_MAX=10
```

If you enable `DATABASE_SSL=true`, optional fields are supported:
```env
DATABASE_SSL_KEY=
DATABASE_SSL_CERT=
DATABASE_SSL_CA=
DATABASE_SSL_CAPATH=
DATABASE_SSL_CIPHER=
DATABASE_SSL_REJECT_UNAUTHORIZED=true
```

## Project structure (high level)
- `src/` — Strapi application code and bootstrap
- `config/` — Configuration for server, admin, plugins, and database
- `scripts/seed.js` — Example data seeding script
- `data/` — Example content and uploaded media used by the seeder
- `.tmp/` — SQLite database (when using the default local SQLite)

## Notes
- Default database is SQLite. For Postgres/MySQL, set env vars as shown above.
- Example content types seeded: `article`, `author`, `category`, `global`, `about`.
- This repository is intended for testing; do not use production secrets.

## Learn more
- Strapi CLI and docs: https://docs.strapi.io
- Strapi Cloud: https://cloud.strapi.io
- Community: https://discord.strapi.io
