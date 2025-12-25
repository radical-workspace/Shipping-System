Shipping System
Logistics & Shipping System — a backend system for managing shipments, rates, payments, tracking, and admin features — built with Clean Architecture in C# (.NET).

Status

Work in progress — see folders for BL (Business Logic), DAL (Data Access Layer), Domains (entities), WepApi (Web API), and UI.
Table of contents
About
Key features
Architecture overview
Repository structure
Tech stack
Prerequisites
Getting started
Running with Docker
Configuration
Development notes
Contributing
License & acknowledgements
About
Shipping System is a backend-first project designed to manage the full lifecycle of shipments: creating and updating shipments, calculating and storing rates, processing payments, tracking status and location, and providing administrative operations. The project follows Clean Architecture principles to keep the domain, business rules, and infrastructure concerns well-separated and testable.

Key features
Shipment CRUD and lifecycle management
Rate calculation and price management
Payment processing (pluggable)
Tracking and status updates
Admin features for managing users, carriers and settings
Clean Architecture separation (Domains, BL, DAL, Web API)
Docker-ready for easier deployment
Architecture overview
This repository organizes code following Clean Architecture:

Domains: core entities and domain models (business rules independent of frameworks)
BL: business logic, use cases, and services
DAL: data access implementations, repositories and ORM/migrations (infrastructure)
WepApi: HTTP API controllers, DTOs, request/response handling (presentation layer)
UI: front-end or admin dashboard (if present)
This separation enables independent testing and easier substitution of implementations (e.g., swap database, payment provider).

Repository structure
.dockerignore, .gitignore — repo hygiene
ShippingSystem.sln — Visual Studio / dotnet solution
Domains/ — domain models and interfaces
BL/ — business logic (use case implementations, services)
DAL/ — data access layer (EF Core, repositories, migrations — if used)
WepApi/ — Web API host, controllers, startup/config
UI/ — front-end application (static site, SPA, or server-rendered UI)
Note: Folder names reflect the current layout in repo; adjust names in README if you rename projects.

Tech stack
C# and .NET (SDK 6.0+ or 7.0+ depending on project files)
(Optional) Entity Framework Core for DAL
Docker (Dockerfile present in repo)
HTML/CSS/JS for UI assets
Prerequisites
.NET SDK 6.0 or newer (install from https://dotnet.microsoft.com/)
Git
Docker (optional, for containerized runs)
Database (e.g., PostgreSQL / SQL Server) — check DAL config for exact provider
Getting started (local)
Clone repository: git clone https://github.com/radical-workspace/Shipping-System.git cd Shipping-System

Restore and build: dotnet restore dotnet build

Run the web API (from repo root): dotnet run --project WepApi

Or open the solution in Visual Studio and run the WepApi project.

Browse:

If WepApi uses Kestrel on default ports, open http://localhost:5000 or https://localhost:5001 (check console output)
If UI is present and served separately, follow UI/README or start the UI server
Notes:

If project uses EF Core migrations, run migrations or update database connection string before first run.
If the project expects environment variables (connection strings, API keys), supply them as described in Configuration.
Running with Docker
Build image: docker build -t shipping-system:latest .

Run container (example): docker run -e ASPNETCORE_ENVIRONMENT=Production -p 5000:80 --name shipping-system shipping-system:latest

Adjust environment variables, volumes, and ports for your setup.

Configuration
appsettings.json / appsettings.Development.json (WepApi) — primary place for configuration.
Environment variables override settings (recommended for secrets and production).
Example keys you may need to set:
ConnectionStrings:DefaultConnection
Jwt:Key, Jwt:Issuer, Jwt:Audience (if JWT auth used)
PaymentProvider:ApiKey (if integrated)
External services endpoints (tracking, carrier APIs)
Add a sample appsettings.example.json or .env file to repo to document required variables.

Development notes & suggestions
Add a top-level README per project (e.g., WepApi/README.md) describing project-specific run/setup steps (migrations, ports, Swagger endpoint).
Add example Postman collection or OpenAPI/Swagger documentation if not already present.
Add CI workflow in .github/workflows to run build and tests on PRs and pushes.
If using EF Core, include migration scripts and commands: dotnet ef migrations add InitialCreate --project DAL --startup-project WepApi dotnet ef database update --project DAL --startup-project WepApi
Tests
If tests exist, add instructions to run them. Example: dotnet test ./tests/YourTestProjectName
If there are no tests yet, consider adding unit tests for BL (business logic) and integration tests for WepApi.

Contributing
Open issues to propose features or report bugs.
Fork the repo, create feature branches, and open pull requests.
Follow conventional commits or a contribution guideline (add CONTRIBUTING.md).
Ensure new features have unit tests and documentation updates.
License & acknowledgements
Add a LICENSE file to make the project’s license explicit (e.g., MIT).
Acknowledge any external libraries, frameworks, or contributors.
Contact / Maintainers
Maintained by radical-workspace. Open an issue or PR for questions and contributions.

