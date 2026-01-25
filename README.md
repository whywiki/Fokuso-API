# Fokuso API

<div align="center">

[![Django](https://img.shields.io/badge/Django-3.2-092E20?style=for-the-badge&labelColor=black&logo=django&logoColor=092E20)](https://djangoproject.com/)
[![Django REST Framework](https://img.shields.io/badge/DRF-3.12-ff1709?style=for-the-badge&labelColor=black&logo=django&logoColor=ff1709)](https://django-rest-framework.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13-316192?style=for-the-badge&labelColor=black&logo=postgresql&logoColor=316192)](https://postgresql.org/)
[![Docker](https://img.shields.io/badge/Docker-latest-2496ED?style=for-the-badge&labelColor=black&logo=docker&logoColor=2496ED)](https://docker.com/)

<div align="center">
  <img src="https://github.com/lowskydev/Fokuso/blob/main/src/assets/logo.png" alt="Fokuso Logo" width="120" height="120">
</div>

**[Frontend Repository](https://github.com/lowskydev/Fokuso)**

[Features](#-features) • [Quick Start](#-quick-start) • [Tech Stack](#%EF%B8%8F-tech-stack) • [Project Structure](#-project-structure) • [Contributing](#-contributing)

</div>

---

## About

Fokuso API is the robust Django REST backend that powers the [Fokuso productivity platform](https://github.com/lowskydev/Fokuso). Built with modern development practices, it provides a comprehensive suite of APIs for focus management, spaced repetition learning, task organization, and productivity analytics.

The API implements Test Driven Development (TDD) principles and includes comprehensive documentation via Swagger UI, making it easy for developers to integrate and extend the platform's capabilities.

---

## Features

### **Authentication & User Management**

- **Token-based Authentication**: Secure user sessions with tokens
- **User Registration & Login**: Complete auth flow
- **Profile Management**: User data management

### **Spaced Repetition System**

- **Flashcard Management**: CRUD operations for learning cards
- **Deck Organization**: Subject-based card grouping
- **SM-2 Algorithm**: Scientifically-proven spaced repetition
- **Review Statistics**: Comprehensive learning analytics
- **Daily Progress Tracking**: Monitor learning consistency

### **Focus Session Management**

- **Session Logging**: Track focus and break periods
- **Duration Recording**: Precise time measurement
- **Statistics Generation**: Productivity insights and trends
- **Streak Calculation**: Consistency tracking

### **Task Management**

- **Todo CRUD Operations**: Complete task management
- **Priority Levels**: High, medium, low prioritization
- **Category System**: Work, personal, health, education, etc.
- **Tag Management**: Flexible organization system
- **Due Date Tracking**: Deadline management

### **Calendar System**

- **Event Management**: Create, update, delete events
- **Event Types**: Focus, study, meeting, break, other
- **Time Tracking**: Start/end time with duration calculation
- **Date Filtering**: Efficient event querying
- **Grouped Responses**: Events organized by date

### **Analytics & Statistics**

- **Daily Review Stats**: Flashcard performance tracking
- **Focus Statistics**: Session analytics and trends
- **Progress Metrics**: Comprehensive productivity insights
- **Historical Data**: Long-term trend analysis

---

## Quick Start

### Prerequisites

Before you begin, ensure you have the following installed:

- **Docker** and **Docker Compose**
- **Git**

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/lowskydev/Fokuso-API.git
   cd Fokuso-API
   ```

2. **Start the services**

   ```bash
   docker compose up
   ```

3. **Access the application**

   - **API Documentation**: [http://127.0.0.1:8000/api/docs](http://127.0.0.1:8000/api/docs)
   - **Admin Panel**: [http://127.0.0.1:8000/admin](http://127.0.0.1:8000/admin)

4. **Setup the Fokuso Frontend**

   Follow the instructions in the [Frontend Repository](https://github.com/lowskydev/Fokuso) to set up the frontend application.

### Important Commands

#### **Development Commands**

```bash
# Start services
docker compose up

# Start services in background
docker compose up -d

# Stop services
docker compose down

```

#### **Application Management**

```bash
# Run tests
docker compose run --rm app sh -c "python manage.py test"

# Create superuser
docker compose run --rm app sh -c "python manage.py createsuperuser"

# Apply migrations
docker compose run --rm app sh -c "python manage.py migrate"

# Code linting
docker compose run --rm app sh -c "flake8"

# Access Django shell
docker compose run --rm app sh -c "python manage.py shell"

# Create new migrations
docker compose run --rm app sh -c "python manage.py makemigrations"
```

#### **Database Management**

```bash
# Reset database (careful - this deletes all fokuso data)
docker compose down
docker volume rm fokuso-api_dev-db-data
docker compose up

# Backup database
docker compose exec db pg_dump -U devuser devdb > backup.sql

# Restore database
docker compose exec -T db psql -U devuser devdb < backup.sql
```

---

## Tech Stack

### **Backend Framework**

- **Django 3.2** - Robust web framework
- **Django REST Framework 3.12** - Powerful API toolkit
- **drf-spectacular** - OpenAPI 3 schema generation

### **Database**

- **PostgreSQL 13** - Advanced relational database
- **psycopg2** - PostgreSQL adapter for Python

### **Development & Deployment**

- **Docker & Docker Compose** - Containerization
- **flake8** - Code linting and style checking
- **Django Test Framework** - Comprehensive testing suite

### **API Features**

- **Token Authentication** - Secure API access
- **Swagger UI Documentation** - Interactive API docs
- **CORS Headers** - Cross-origin resource sharing
- **Pagination** - Efficient data loading
- **Filtering & Search** - Advanced query capabilities

---

## Project Structure

```
app/
├── 📁 app/                       # Main application configuration
│   ├── 📄 settings.py            # Django settings
│   ├── 📄 urls.py                # URL routing
│   └── 📄 calc.py                # Utility functions
│
├── 📁 core/                      # Core application models
│   ├── 📄 models.py              # Database models
│   ├── 📄 admin.py               # Admin interface
│   └── 📁 management/            # Custom management commands
│
├── 📁 user/                      # User authentication
│   ├── 📄 views.py               # Auth views
│   ├── 📄 serializers.py         # User serializers
│   └── 📄 urls.py                # User URLs
│
├── 📁 flashcards/                # Spaced repetition system
│   ├── 📄 views.py               # Flashcard views
│   ├── 📄 serializers.py         # Card serializers
│   ├── 📄 sm2.py                 # SM-2 algorithm
│   └── 📄 urls.py                # Flashcard URLs
│
├── 📁 calendars/                 # Calendar management
│   ├── 📄 views.py               # Calendar views
│   ├── 📄 serializers.py         # Event serializers
│   └── 📄 urls.py                # Calendar URLs
│
├── 📁 todos/                     # Task management
│   ├── 📄 views.py               # Todo views
│   ├── 📄 serializers.py         # Task serializers
│   └── 📄 urls.py                # Todo URLs
│
├── 📁 stats/                     # Analytics system
│   ├── 📄 views.py               # Statistics views
│   ├── 📄 serializers.py         # Stats serializers
│   └── 📄 urls.py                # Stats URLs
│
└── 📁 notes/                     # Note management
    ├── 📄 views.py               # Notes views
    ├── 📄 serializers.py         # Note serializers
    └── 📄 urls.py                # Notes URLs
```

### **Key Architecture Decisions**

- **Modular App Structure**: Features separated into Django apps
- **RESTful API Design**: Consistent REST principles
- **Token Authentication**: Stateless authentication system
- **Test-Driven Development**: Comprehensive test coverage
- **Docker Containerization**: Consistent development environment

---

## API Endpoints

### **Authentication**

```
POST   /api/user/create/                   # User registration
POST   /api/user/token/                    # Login & token generation
GET    /api/user/me/                       # User profile
PATCH  /api/user/me/                       # Update profile
```

### **Flashcards**

```
GET    /api/flashcards/                    # List flashcards
POST   /api/flashcards/                    # Create flashcard
GET    /api/flashcards/{id}/               # Get flashcard
PATCH  /api/flashcards/{id}/               # Update flashcard
DELETE /api/flashcards/{id}/               # Delete flashcard
POST   /api/flashcards/{id}/review/        # Review flashcard

GET    /api/flashcards/decks/              # List decks
POST   /api/flashcards/decks/              # Create deck
```

### **Calendar**

```
GET    /api/calendars/events/              # List events
POST   /api/calendars/events/              # Create event
GET    /api/calendars/events/{id}/         # Get event
PATCH  /api/calendars/events/{id}/         # Update event
DELETE /api/calendars/events/{id}/         # Delete event

GET    /api/calendars/events/grouped/      # Events grouped by date
GET    /api/calendars/events/today/        # Today's events
```

### **Todos**

```
GET    /api/todos/                         # List todos
POST   /api/todos/                         # Create todo
GET    /api/todos/{id}/                    # Get todo
PATCH  /api/todos/{id}/                    # Update todo
DELETE /api/todos/{id}/                    # Delete todo

GET    /api/todos/tags/                    # List tags
POST   /api/todos/tags/                    # Create tag
```

### **Statistics**

```
POST   /api/stats/session/                 # Log focus session
GET    /api/stats/sessions/                # List sessions
GET    /api/stats/user-stats/              # User statistics
GET    /api/stats/weekly-data/             # Weekly analytics
GET    /api/stats/hourly-data/             # Hourly analytics
```

---

## Testing

Fokuso API follows Test-Driven Development principles with comprehensive test coverage:

```bash
# Run all tests
docker compose run --rm app sh -c "python manage.py test"

# Run specific app tests
docker compose run --rm app sh -c "python manage.py test flashcards"

# Run specific test class
docker compose run --rm app sh -c "python manage.py test flashcards.tests.test_flashcards_api"
```

### **Test Structure**

- **Unit Tests**: Model and utility function testing
- **API Tests**: Comprehensive endpoint testing
- **Integration Tests**: Feature workflow testing
- **Authentication Tests**: Security validation

---

## Contributing

### **How to Contribute**

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **Write tests** for your new feature
4. **Implement your feature** following TDD principles
5. **Run the test suite** to ensure everything passes
6. **Commit your changes** (`git commit -m 'Add amazing feature'`)
7. **Push to the branch** (`git push origin feature/amazing-feature`)
8. **Open a Pull Request**

### **Development Guidelines**

- Follow Django best practices and PEP 8 style guide
- Write comprehensive tests for all new features
- Update API documentation for new endpoints
- Use meaningful commit messages
- Ensure all tests pass before submitting PR

---

## Contributors

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/lowskydev">
        <img src="https://github.com/lowskydev.png" width="100px;" alt="lowskydev"/>
        <br />
        <sub><b><a href="https://github.com/lowskydev">lowskydev</a></b></sub>
      </a>
      <br />
      <sub> Project Leader & Full-Stack Developer</sub>
    </td>
    <td align="center">
      <a href="https://github.com/lyes0000">
        <img src="https://github.com/lyes0000.png" width="100px;" alt="lyes0000"/>
        <br />
        <sub><b><a href="https://github.com/lyes0000">lyes0000</a></b></sub>
      </a>
      <br />
      <sub> Backend Developer</sub>
    </td>
  </tr>
</table>

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## Acknowledgments

- **Django Software Foundation** for the excellent web framework
- **Django REST Framework** for powerful API tools
- **PostgreSQL** for reliable database technology
- **Docker** for consistent development environments

---

<div align="center">

**Made with ❤️ by the Fokuso team**

[⬆ Back to top](#-fokuso-api)

</div>
