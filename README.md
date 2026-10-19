The repository does not currently have a root `README.md`. Here is a ready-to-commit version:

````markdown name=README.md
# DatingApp

DatingApp is a full-stack dating application with an ASP.NET Core Web API backend and an Angular client. It provides account registration and login, JWT-based authentication, member browsing, member profiles, photos, lists, messaging routes, and development error-handling pages.

## Stack

- **Backend:** C# with .NET 10 and ASP.NET Core Web API
- **Frontend:** Angular 21 with TypeScript
- **Database:** SQLite through Entity Framework Core
- **Authentication:** JWT bearer tokens
- **Styling:** Tailwind CSS 4 and DaisyUI
- **Testing:** Vitest through Angular CLI
- **Reactive programming:** RxJS

## Repository structure

```text
.
├── API/
│   ├── Controllers/      HTTP API endpoints
│   ├── Data/             EF Core context, repositories, migrations, and seed data
│   ├── DTOs/             Request and response data-transfer objects
│   ├── Entities/         Application domain models
│   ├── Extensions/       Mapping and service extensions
│   ├── Interfaces/       Repository and service contracts
│   ├── Middleware/       Global exception handling
│   ├── Services/         JWT token generation and application services
│   ├── Program.cs        API startup and dependency injection configuration
│   └── API.csproj        .NET project definition
├── client/
│   ├── src/
│   │   ├── app/          Application bootstrap and routing
│   │   ├── core/         Guards, interceptors, and shared services
│   │   ├── features/     Account, members, lists, messages, and error pages
│   │   ├── layout/       Shared layout components such as navigation
│   │   ├── shared/       Reusable UI and error components
│   │   └── types/        TypeScript types
│   ├── package.json      Angular scripts and dependencies
│   └── angular.json      Angular CLI configuration
└── DatingApp.slnx        .NET solution file
```

## How it works

The Angular client is bootstrapped from `client/src/main.ts` and uses the routes defined in `client/src/app/app.routes.ts`. Public routes include the home page, while member browsing, member details, lists, and messages are protected by the `authGuard`.

The ASP.NET Core API is started from `API/Program.cs`. It configures Entity Framework Core with SQLite, JWT bearer authentication, CORS for the Angular development server, repository services, and global exception handling. Database migrations and seed users are applied during application startup.

## Prerequisites

Install the following tools:

- [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0)
- [Node.js](https://nodejs.org/) with npm
- Optionally, a SQLite database viewer for inspecting `dating.db`

The project specifies npm 11.11.0 as its package manager version. Using a compatible recent Node.js and npm installation is recommended.

## Getting started

### 1. Clone the repository

```bash
git clone https://github.com/MateuszBandura/DatingApp.git
cd DatingApp
```

### 2. Configure the API

Review `API/appsettings.Development.json` and configure:

- `ConnectionStrings:DefaultConnection` — SQLite database connection string
- `TokenKey` — secret key used to sign JWTs

Do not use the sample token key outside local development. Replace it with a secure value and avoid committing real secrets to source control.

For local development, the default database configuration is:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Data source=dating.db"
  }
}
```

### 3. Restore and run the API

From the repository root:

```bash
dotnet restore
dotnet run --project API
```

The API URL is printed by `dotnet run` and may vary depending on the active launch settings.

On startup, the API automatically:

1. Applies pending Entity Framework Core migrations.
2. Creates or updates the SQLite database.
3. Seeds users from `API/Data/UserSeedData.json`.

### 4. Install and run the Angular client

Open a second terminal:

```bash
cd client
npm install
npm start
```

The Angular development server is normally available at:

```text
http://localhost:4200
```

The client is configured to communicate with the local API during development.

## API endpoints

The API uses the `/api` prefix.

### Account

| Method | Endpoint | Authentication | Description |
| --- | --- | --- | --- |
| `POST` | `/api/account/register` | Public | Register a new account |
| `POST` | `/api/account/login` | Public | Authenticate and receive a JWT |

### Members

Member endpoints require a valid JWT bearer token.

| Method | Endpoint | Authentication | Description |
| --- | --- | --- | --- |
| `GET` | `/api/members` | JWT required | Retrieve available members |
| `GET` | `/api/members/{id}` | JWT required | Retrieve a member by ID |
| `GET` | `/api/members/{id}/photos` | JWT required | Retrieve photos for a member |

Send the token using the standard HTTP header:

```http
Authorization: Bearer <token>
```

The repository also includes `BuggyController` and frontend error pages for exercising error-handling behavior during development.

## Frontend commands

Run these commands from the `client/` directory:

```bash
# Start the development server
npm start

# Build the application
npm run build

# Build continuously using the development configuration
npm run watch

# Run unit tests with Vitest
npm test
```

Angular CLI does not include an end-to-end testing framework by default. An `ng e2e` command is therefore not configured unless an e2e framework is added separately.

## Configuration and security notes

- Keep `TokenKey` private and use environment-specific configuration for real deployments.
- Do not commit production credentials, signing keys, or other secrets.
- SQLite and the local `dating.db` database are intended for development and demonstration use.
- JWTs generated by `TokenService` expire after four days.
- The API allows requests from `http://localhost:4200` and `https://localhost:4200` for local development.
- The error-testing endpoints and pages are development utilities and should be reviewed before exposing them in a production environment.
````

I couldn’t commit it because the repository’s coding agent is not enabled.
