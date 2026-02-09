# Project Structures

A guide to well-organized Python project structures using the `src/` layout approach.

## The `src/` Layout

The `src/` layout is the recommended approach for Python projects. Your source code lives in a `src/` directory, which prevents common import errors by ensuring tests use the installed package rather than local files.

```
my-project/
├── src/
│   └── app/
│       ├── __init__.py
│       ├── core/
│       ├── models/
│       ├── routes/
│       └── main.py
├── tests/
├── pyproject.toml
└── README.md
```

## Essential Top-Level Files

- **`pyproject.toml`** - Project metadata and dependencies
- **`README.md`** - Project overview and documentation
- **`LICENSE`** - Licensing information
- **`.gitignore`** - Files to exclude from version control

## Infrastructure-Based Folder Organization

Organize your code by architectural patterns and infrastructure roles rather than by features. This makes the codebase more maintainable and reusable across different domains.

### Core Infrastructure Folders

| Folder | Purpose | Examples |
|--------|---------|----------|
| **`core/`** | Core infrastructure components used throughout | Configuration, logging, middleware, lifecycle management |
| **`interfaces/`** | Abstract base classes defining contracts | Storage interface, cache interface, exporter ABC |
| **`connectors/`** | Concrete implementations connecting to external systems | Database, cache, message queue, cloud services |
| **`decorators/`** | Cross-cutting concern decorators that wrap functions | `@instrument`, `@cache`, `@retry`, `@rate_limit`, `@timeout` |
| **`policies/`** | Business and operational policies defining rules | Sampling policies, rate limiting, retention, access control |
| **`dispatchers/`** | Components that distribute events/data to multiple destinations | Event publisher, notification dispatcher, audit log dispatcher |
| **`handlers/`** | Event and request handlers for specific types | Domain event handlers, webhook handlers, exception handlers |
| **`validators/`** | Validation logic separated from models | Business rule validators, cross-field validators |
| **`transformers/`** | Data transformation logic | DTO transformers, format converters, schema migrators |
| **`repositories/`** | Data access layer abstracting storage | Database repositories, cache repositories |
| **`routes/`** or **`endpoints/`** | API routes (for web applications) | REST endpoints, GraphQL resolvers |
| **`models/`** | Data models and domain entities | Pydantic models, SQLAlchemy models, domain objects |

### Advanced Infrastructure Folders

Add these as your application grows:

| Folder | Purpose | Use Cases |
|--------|---------|-----------|
| **`interceptors/`** | Components that intercept and modify behavior | Request/response interceptors, query interceptors |
| **`orchestrators/`** | Coordinate multiple operations or services | Workflow orchestrators, saga coordinators |
| **`resolvers/`** | Resolve configuration/dependencies dynamically | Environment-based config, service discovery |
| **`storages/`** | Physical storage mechanism implementations | File storage (S3, Azure Blob), object storage |
| **`guards/`** | Components that protect access to resources | Authorization guards, rate limit guards, circuit breakers |
| **`filters/`** | Components that filter data or requests | Query filters, response filters, security filters |
| **`schedulers/`** | Job scheduling and background tasks | Cron jobs, periodic tasks, background workers |

## Key Principles

1. **Infrastructure-Focused** - Folders are named based on architectural role, not business domain
2. **Pattern-Based** - Many folders correspond to well-known design patterns
3. **Reusable** - Components can be used across different features
4. **Scalable** - New features can leverage existing infrastructure
5. **Clear Separation** - Each folder has a single, well-defined responsibility

## When to Use Each Folder

- **`decorators/`** - Add behavior to functions without modifying them
- **`policies/`** - Configurable rules that can change based on environment
- **`dispatchers/`** - Send data/events to multiple destinations
- **`handlers/`** - Process specific types of events or requests
- **`interceptors/`** - Modify behavior at runtime (before/after execution)
- **`orchestrators/`** - Coordinate multiple services or complex workflows
- **`resolvers/`** - Dynamic resolution of configuration or dependencies

## Testing Strategy

Place your tests in a top-level `tests/` directory that mirrors your package structure.

```
tests/
├── __init__.py
├── unit/
│   ├── test_core.py
│   └── test_models.py
└── integration/
    └── test_routes.py
```

## Layered Architecture

For larger applications, separate concerns into distinct layers:

- **User-facing interfaces** - CLIs, web frontends, REST APIs
- **Domain logic** - Business rules, use cases, application services
- **Persistence** - Databases, file systems, external services

## Design Patterns to Consider

- **Factory Pattern** - Creating objects based on configuration
- **Observer Pattern** - Managing multiple subscribers to events
- **Strategy Pattern** - Interchangeable algorithms or behaviors
- **Decorator Pattern** - Adding functionality to functions dynamically
- **Adapter Pattern** - Adapting your code to external libraries
- **Repository Pattern** - Abstracting data access

## Best Practices

- **Group code into directories** rather than scattering Python files at the root
- **Use logical subdirectories** that reflect infrastructure patterns
- **Keep essential project files at the root** for easy discovery
- **Mirror your package structure in tests** for easy navigation
- **Avoid large monolithic modules** - split code into focused modules
- **Use abstract interfaces** to define contracts between layers
- **Apply design patterns** to make your architecture clear and maintainable
