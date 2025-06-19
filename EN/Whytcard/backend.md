# WhytCard Backend Code Documentation

This document describes the structure and responsibilities of the backend code located in the `backend/` directory of the WhytCard project.

## Directory Structure

```
backend/
├── config/                       # Application configuration and settings
│   ├── app_config.py            # Pydantic BaseSettings: loads .env, defines AppSettings, creates data directories
│   ├── base_schemas.py          # Generic API response models: BaseResponse, ErrorResponse, PaginatedResponse
│   ├── config_manager.py        # Singleton provider of AppSettings instance via lru_cache
│   └── __init__.py              # Package marker for config
├── core/                         # Core business logic package
│   └── __init__.py              # Package marker for core
├── dataset/                      # Dataset management: API, service layer, schemas, tasks
│   ├── api.py                   # FastAPI router for dataset CRUD, processing, preview, import, deletion
│   ├── Dataset.py               # DatasetService: handles dataset lifecycle (creation, metadata, I/O, processing)
│   ├── schemas.py               # Pydantic models for dataset request/response validation
│   └── tasks/                   # I/O-bound utilities
│       ├── data_loader.py       # Parse CSV, JSON, JSONL, Parquet into standardized record objects
│       ├── data_processor.py    # Apply configured data cleaning and transformation steps
│       └── __init__.py          # Package marker for dataset tasks
├── rag/                          # Retrieval-Augmented Generation (RAG) module
│   ├── api.py                   # FastAPI router for vector store CRUD and RAG query endpoints
│   ├── Rag.py                   # RAGService: document ingestion and query handling (stubs)
│   ├── schemas.py               # Pydantic models for vector store configuration and responses
│   └── tasks/                   # Placeholder for RAG-specific task modules
│       └── __init__.py          # Package marker for rag tasks
├── scraping/                     # Web scraping module
│   ├── api.py                   # FastAPI router for scraping job submission, status, and results
│   ├── schemas.py               # Pydantic models for scraping job config, status, and paginated results
│   └── tasks/                   # Scraping engine components (planned)
│       ├── html_scraper.py      # (To be implemented) HTML content extraction
│       ├── parser.py            # (To be implemented) Unified parsing logic
│       ├── pdf_scraper.py       # (To be implemented) PDF extraction and OCR
│       ├── robots_handler.py    # (To be implemented) robots.txt compliance
│       └── __init__.py          # Package marker for scraping tasks
├── training/                     # Machine learning training workflows
│   ├── api.py                   # FastAPI router for training orchestration endpoints
│   ├── helpers.py               # Preprocessing utilities for training data
│   ├── schemas.py               # Pydantic models for training configurations and metrics
│   └── tasks/                   # Placeholder for training tasks and pipelines
│       └── __init__.py          # Package marker for training tasks
├── utils/                        # Shared helper modules
│   ├── common_helpers.py        # Reusable utility functions across modules
│   ├── error_handlers.py        # Centralized FastAPI exception handlers
│   ├── logging_setup.py         # Loguru-based logging configuration
│   └── __init__.py              # Package marker for utils
├── Api_Orchestrator.md          # Documentation: main FastAPI router and health check aggregation (docs)
├── Api_Orchestrator.py          # Aggregates module routers under `/api/v1` and defines `/health` endpoint
├── Fonctionnality_Orchestrator.md# Documentation: high-level workflow orchestrator (docs)
├── Fonctionnality_Orchestrator.py # Stubs for multi-module workflow orchestration
├── cli_app.md                   # Documentation: CLI application placeholder (docs)
├── cli_app.py                   # Command-line interface entry point (to be implemented)
├── main.md                      # Documentation: FastAPI app setup, middlewares, lifecycle events (docs)
├── main.py                      # Application entry point: initializes FastAPI, routers, CORS, exception handlers
├── __init__.md                  # Documentation: backend package marker (docs)
└── __init__.py                  # Marks `backend` as a Python package
```

## Component Descriptions

### 1. Configuration (`config/`)

- **app_config.py**: Defines `AppSettings` using Pydantic `BaseSettings`. Loads environment variables, `.env` files, and automatically creates required directories for data, models, and logs.
- **base_schemas.py**: Provides generic response models (`BaseResponse`, `ErrorResponse`, `PaginatedResponse`) to ensure consistent API responses across modules.
- **config_manager.py**: Uses `functools.lru_cache` to create a singleton `settings` instance, avoiding repeated configuration parsing.

### 2. Core (`core/`)

- Placeholder package for fundamental business logic, domain models, and shared services used by multiple modules.

### 3. Dataset Management (`dataset/`)

- **api.py**: Exposes REST endpoints for:
  - Creating, listing, retrieving, and deleting datasets.
  - Uploading records to datasets and previewing data.
  - Launching data processing pipelines with configurable transformations.
- **Dataset.py**: Implements `DatasetService`, which handles the full dataset lifecycle, including metadata management, file I/O, processing, and cleanup.
- **schemas.py**: Defines Pydantic models for request validation and response serialization, ensuring data integrity.
- **tasks/data_loader.py**: Parses uploaded files (CSV, JSON, JSONL, Parquet) into internal record objects.
- **tasks/data_processor.py**: Applies sequential data cleaning and transformation steps (e.g., removing duplicates, handling missing values) to loaded records.

### 4. RAG Module (`rag/`)

- **api.py**: Endpoints for:
  - Creating and managing vector stores.
  - Querying vector stores for retrieval-augmented generation.
- **Rag.py**: Contains `RAGService` class stubs for:
  - Document ingestion into vector stores.
  - Query handling and response augmentation.
- **schemas.py**: Models for vector store creation requests, metadata, query requests, and query responses.
- **tasks/**: Reserved for future RAG task implementations (e.g., embedding generation, vector store management).

### 5. Scraping (`scraping/`)

- **api.py**: Endpoints to:
  - Submit scraping jobs with flexible configurations.
  - Check job status.
  - Retrieve paginated results of scraped items.
- **schemas.py**: Pydantic models defining scraping job configurations, statuses, and result schemas.
- **tasks/html_scraper.py**, **parser.py**, **pdf_scraper.py**, **robots_handler.py**: Planned modules for performing HTTP fetches, parsing content, PDF OCR, and obeying robots.txt rules.

### 6. Training Workflows (`training/`)

- **api.py**: Defines endpoints for initiating and monitoring machine learning training workflows.
- **helpers.py**: Provides data preprocessing and utility functions for preparing training inputs.
- **schemas.py**: Models for training job configurations, status updates, and result metrics.
- **tasks/**: Placeholder for training-specific task implementations (e.g., model evaluation, metric logging).

### 7. Utilities (`utils/`)

- **common_helpers.py**: Collection of general-purpose helper functions shared across modules.
- **error_handlers.py**: Custom FastAPI exception handlers for consistent error responses and logging.
- **logging_setup.py**: Configures structured logging using Loguru with standardized formats and log levels.

### 8. Entry Points

- **main.py**: The application entry point. Sets up the FastAPI app with CORS, exception handlers, module routers under `/api/v1`, and startup/shutdown events.
- **Api_Orchestrator.py**: Aggregates all module routers under a common prefix and defines a health check endpoint at `/health`.
- **Fonctionnality_Orchestrator.py**: Blueprint for high-level orchestration of multi-module workflows (e.g., end-to-end pipelines).
- **cli_app.py**: Intended CLI entry point for command-line interactions (to be implemented with Typer or Click).

## Architectural Highlights

- **Modularity**: Each domain (dataset, RAG, scraping, training) is fully encapsulated with its own router, service layer, schemas, and tasks.
- **Validation & Safety**: Pydantic models enforce strict typing and validation on all incoming and outgoing API payloads.
- **Extensibility**: `tasks` subpackages isolate I/O-bound and processing logic, facilitating future feature additions without affecting API layer.
- **Configuration by Design**: Central `AppSettings` ensures environment-based configuration, directory management, and consistent defaults.
- **Separation of Concerns**: Clear division between HTTP interface (routers), business logic (services), and data validation (schemas).

---

*Documentation generated for the WhytCard project backend. For questions or updates, please refer to the module-specific documentation files in the `backend/` directory.* 