# Extradime.com - Complete Implementation Checklist

> **Granular task checklist based on docs/improved_enhanced_tickets.md**
> **Approach:** Test-Driven Development (TDD)
> **Format:** Each task has unique ID (TICKET-ID.TASK-ID)
> **Coverage:** All 3 Phases (39 tickets, 1,398 tasks)
> **Phases:** Phase 1 (Weeks 1-8), Phase 2 (Weeks 9-16), Phase 3 (Weeks 17-24)

---

## Progress Tracking

**Total Tasks:** 1,398 (All Phases)
**Completed:** 0
**In Progress:** 0
**Remaining:** 1,398

### By Phase:
- **Phase 1 (Core Platform):** 855 tasks (EXT-001 to EXT-029)
- **Phase 2 (User & Community):** 331 tasks (EXT-030 to EXT-036)
- **Phase 3 (Advanced Features):** 212 tasks (EXT-037 to EXT-039)

### By Epic:
- **Epic 1.1 (Foundation):** 233 tasks (EXT-001 to EXT-009)
- **Epic 1.2 (Scraping):** 248 tasks (EXT-010 to EXT-017)
- **Epic 1.3 (Content):** 193 tasks (EXT-018 to EXT-021)
- **Epic 1.4 (AI Generation):** 181 tasks (EXT-022 to EXT-029)
- **Epic 2.1 (User Management):** 98 tasks (EXT-030 to EXT-031)
- **Epic 2.2 (Forum Integration):** 81 tasks (EXT-032 to EXT-033)
- **Epic 2.3 (Content Moderation):** 152 tasks (EXT-034 to EXT-036)
- **Epic 3.1 (Newsletter System):** 212 tasks (EXT-037 to EXT-039)

### By Ticket:
**Phase 1:**
- EXT-001: 28 | EXT-002: 18 | EXT-003: 28 | EXT-004: 29 | EXT-005: 31
- EXT-006: 25 | EXT-007: 26 | EXT-008: 12 | EXT-009: 24
- EXT-010: 42 | EXT-011: 37 | EXT-012: 29 | EXT-013: 29
- EXT-014: 34 | EXT-015: 32 | EXT-016: 30 | EXT-017: 24
- EXT-018: 46 | EXT-019: 45 | EXT-020: 49 | EXT-021: 31
- EXT-022: 26 | EXT-023: 37 | EXT-024: 49 | EXT-025: 32
- EXT-026: 44 | EXT-027: 34 | EXT-028: 45 | EXT-029: 42

**Phase 2:**
- EXT-030: 56 | EXT-031: 42 | EXT-032: 31 | EXT-033: 50
- EXT-034: 36 | EXT-035: 42 | EXT-036: 43

**Phase 3:**
- EXT-037: 64 | EXT-038: 40 | EXT-039: 62

---

# Phase 1: Core Platform (Weeks 1-8)

## Epic 1.1: Project Foundation (Week 1-2)

### EXT-001: Django Project Initial Setup

- [ ] **EXT-001.1**: Create project directory: `mkdir -p /Users/Mark/Extradime/extradime_gemini`
- [ ] **EXT-001.2**: Navigate to project directory: `cd /Users/Mark/Extradime/extradime_gemini`
- [ ] **EXT-001.3**: Create virtual environment: `python -m venv venv`
- [ ] **EXT-001.4**: Activate virtual environment: `source venv/bin/activate`
- [ ] **EXT-001.5**: Install Django: `pip install django==5.0.1`
- [ ] **EXT-001.6**: Install django-environ: `pip install django-environ==0.11.2`
- [ ] **EXT-001.7**: Create Django project: `django-admin startproject extradime .`
- [ ] **EXT-001.8**: Create settings directory: `mkdir -p extradime/settings`
- [ ] **EXT-001.9**: Create `extradime/settings/__init__.py` file
- [ ] **EXT-001.10**: Create `extradime/settings/base.py` with base configuration
- [ ] **EXT-001.11**: Create `extradime/settings/development.py` with DEBUG=True
- [ ] **EXT-001.12**: Create `extradime/settings/production.py` with DEBUG=False
- [ ] **EXT-001.13**: Create `extradime/settings/test.py` for testing configuration
- [ ] **EXT-001.14**: Create `.env.example` file with all required environment variables
- [ ] **EXT-001.15**: Create `.env` file (copy from .env.example and fill in values)
- [ ] **EXT-001.16**: Create `.gitignore` file (include venv/, .env, *.pyc, __pycache__/)
- [ ] **EXT-001.17**: Create `README.md` with project description and setup instructions
- [ ] **EXT-001.18**: Update `manage.py` to use development settings by default
- [ ] **EXT-001.19**: Configure DATABASES in base.py to read from environment variables
- [ ] **EXT-001.20**: Configure STATIC_URL, STATIC_ROOT, MEDIA_URL, MEDIA_ROOT in base.py
- [ ] **EXT-001.21**: Configure TEMPLATES with proper directories in base.py
- [ ] **EXT-001.22**: Set SECRET_KEY to load from environment variable in base.py
- [ ] **EXT-001.23**: Configure ALLOWED_HOSTS in development.py and production.py
- [ ] **EXT-001.24**: Run Django server: `python manage.py runserver`
- [ ] **EXT-001.25**: Verify server starts without errors at http://localhost:8000/
- [ ] **EXT-001.26**: Verify admin interface loads at http://localhost:8000/admin/
- [ ] **EXT-001.27**: Run `python manage.py diffsettings` and verify settings load correctly
- [ ] **EXT-001.28**: Test with DJANGO_SETTINGS_MODULE=extradime.settings.production

---

### EXT-002: PostgreSQL Database Configuration

- [ ] **EXT-002.1**: Install PostgreSQL (if not already installed)
- [ ] **EXT-002.2**: Install psycopg2-binary: `pip install psycopg2-binary==2.9.9`
- [ ] **EXT-002.3**: Create PostgreSQL database: `createdb extradime_db`
- [ ] **EXT-002.4**: Create PostgreSQL user: `createuser extradime_user -P`
- [ ] **EXT-002.5**: Grant privileges: `psql -c "GRANT ALL PRIVILEGES ON DATABASE extradime_db TO extradime_user;"`
- [ ] **EXT-002.6**: Update `.env` file with database credentials (DB_NAME, DB_USER, DB_PASSWORD, DB_HOST, DB_PORT)
- [ ] **EXT-002.7**: Update `extradime/settings/base.py` with PostgreSQL DATABASES configuration
- [ ] **EXT-002.8**: Test database connection: `python manage.py dbshell`
- [ ] **EXT-002.9**: Exit dbshell and verify connection successful
- [ ] **EXT-002.10**: Run initial migrations: `python manage.py migrate`
- [ ] **EXT-002.11**: Verify migrations applied successfully (check output)
- [ ] **EXT-002.12**: Create superuser: `python manage.py createsuperuser`
- [ ] **EXT-002.13**: Test CRUD operations in Django shell: `python manage.py shell`
- [ ] **EXT-002.14**: In shell, create test user: `from django.contrib.auth.models import User; User.objects.create(username='test')`
- [ ] **EXT-002.15**: In shell, read user: `User.objects.get(username='test')`
- [ ] **EXT-002.16**: In shell, update user: `user.email = 'test@example.com'; user.save()`
- [ ] **EXT-002.17**: In shell, delete user: `user.delete()`
- [ ] **EXT-002.18**: Exit shell and verify database operations work correctly

---

### EXT-003: Celery and Redis Setup

- [ ] **EXT-003.1**: Install Redis (if not already installed)
- [ ] **EXT-003.2**: Install Celery: `pip install celery==5.3.4`
- [ ] **EXT-003.3**: Install Redis Python client: `pip install redis==5.0.1`
- [ ] **EXT-003.4**: Install django-celery-beat: `pip install django-celery-beat==2.5.0`
- [ ] **EXT-003.5**: Install django-celery-results: `pip install django-celery-results==2.5.1`
- [ ] **EXT-003.6**: Create `extradime/celery.py` file
- [ ] **EXT-003.7**: Implement Celery app configuration in `extradime/celery.py`
- [ ] **EXT-003.8**: Update `extradime/__init__.py` to load Celery app on startup
- [ ] **EXT-003.9**: Add 'django_celery_beat' to INSTALLED_APPS in base.py
- [ ] **EXT-003.10**: Add 'django_celery_results' to INSTALLED_APPS in base.py
- [ ] **EXT-003.11**: Configure CELERY_BROKER_URL in base.py (redis://localhost:6379/0)
- [ ] **EXT-003.12**: Configure CELERY_RESULT_BACKEND in base.py (redis://localhost:6379/0)
- [ ] **EXT-003.13**: Configure CELERY_ACCEPT_CONTENT, CELERY_TASK_SERIALIZER, CELERY_RESULT_SERIALIZER in base.py
- [ ] **EXT-003.14**: Configure CELERY_TIMEZONE = 'UTC' in base.py
- [ ] **EXT-003.15**: Create `apps/core/tasks.py` file
- [ ] **EXT-003.16**: Write test task in `apps/core/tasks.py`: `@shared_task def test_task(): return 'Hello'`
- [ ] **EXT-003.17**: Run migrations for Celery apps: `python manage.py migrate`
- [ ] **EXT-003.18**: Start Redis server: `redis-server` (in separate terminal)
- [ ] **EXT-003.19**: Verify Redis is running: `redis-cli ping` (should return PONG)
- [ ] **EXT-003.20**: Start Celery worker: `celery -A extradime worker -l info` (in separate terminal)
- [ ] **EXT-003.21**: Verify Celery worker starts without errors
- [ ] **EXT-003.22**: Start Celery beat: `celery -A extradime beat -l info` (in separate terminal)
- [ ] **EXT-003.23**: Verify Celery beat starts without errors
- [ ] **EXT-003.24**: Execute test task in Django shell: `from apps.core.tasks import test_task; result = test_task.delay()`
- [ ] **EXT-003.25**: Check task result: `result.get()`
- [ ] **EXT-003.26**: Verify task appears in Redis: `redis-cli KEYS *`
- [ ] **EXT-003.27**: Check task results in database: query django_celery_results_taskresult table
- [ ] **EXT-003.28**: Verify all Celery components working correctly

---

### EXT-004: Core App Setup

- [ ] **EXT-004.1**: Create apps directory: `mkdir -p apps`
- [ ] **EXT-004.2**: Create `apps/__init__.py` file
- [ ] **EXT-004.3**: Create core app: `python manage.py startapp core apps/core`
- [ ] **EXT-004.4**: Create `apps/core/apps.py` with proper app configuration
- [ ] **EXT-004.5**: Add 'apps.core' to INSTALLED_APPS in base.py
- [ ] **EXT-004.6**: Create templates directory: `mkdir -p apps/core/templates/core`
- [ ] **EXT-004.7**: Create static directories: `mkdir -p static/css static/js`
- [ ] **EXT-004.8**: Create `apps/core/templates/core/base.html` with complete Bootstrap 5 template
- [ ] **EXT-004.9**: Create `apps/core/templates/core/home.html` extending base.html
- [ ] **EXT-004.10**: Create `apps/core/templates/core/about.html` extending base.html
- [ ] **EXT-004.11**: Create `static/css/main.css` with custom styles
- [ ] **EXT-004.12**: Create `static/js/main.js` with custom JavaScript
- [ ] **EXT-004.13**: Create `apps/core/views.py` with HomeView (TemplateView)
- [ ] **EXT-004.14**: Create `apps/core/views.py` with AboutView (TemplateView)
- [ ] **EXT-004.15**: Create `apps/core/urls.py` with URL patterns for home and about
- [ ] **EXT-004.16**: Update `extradime/urls.py` to include core.urls
- [ ] **EXT-004.17**: Create `apps/core/utils.py` for shared utility functions
- [ ] **EXT-004.18**: Create `apps/core/middleware.py` for custom middleware (if needed)
- [ ] **EXT-004.19**: Run Django server: `python manage.py runserver`
- [ ] **EXT-004.20**: Access home page: http://localhost:8000/ and verify it renders
- [ ] **EXT-004.21**: Verify Bootstrap 5 CSS loads (check browser console for no 404 errors)
- [ ] **EXT-004.22**: Verify static files load correctly (main.css, main.js)
- [ ] **EXT-004.23**: Test navigation links (Home, Articles, Opportunities, About)
- [ ] **EXT-004.24**: Test responsive design at 320px width (mobile - hamburger menu visible)
- [ ] **EXT-004.25**: Test responsive design at 768px width (tablet - two-column footer)
- [ ] **EXT-004.26**: Test responsive design at 1024px+ width (desktop - full navigation)
- [ ] **EXT-004.27**: Test mobile toggle button functionality (hamburger menu expands/collapses)
- [ ] **EXT-004.28**: Validate HTML: https://validator.w3.org/ (paste source or URL)
- [ ] **EXT-004.29**: Access about page: http://localhost:8000/about/ and verify it renders

---

### EXT-005: Requirements and Dependencies Installation

- [ ] **EXT-005.1**: Create `requirements.txt` file in project root
- [ ] **EXT-005.2**: Add Django==5.0.1 to requirements.txt
- [ ] **EXT-005.3**: Add celery==5.3.4 to requirements.txt
- [ ] **EXT-005.4**: Add redis==5.0.1 to requirements.txt
- [ ] **EXT-005.5**: Add psycopg2-binary==2.9.9 to requirements.txt
- [ ] **EXT-005.6**: Add django-environ==0.11.2 to requirements.txt
- [ ] **EXT-005.7**: Add django-celery-beat==2.5.0 to requirements.txt
- [ ] **EXT-005.8**: Add django-celery-results==2.5.1 to requirements.txt
- [ ] **EXT-005.9**: Add scrapy==2.11.0 to requirements.txt
- [ ] **EXT-005.10**: Add beautifulsoup4==4.12.2 to requirements.txt
- [ ] **EXT-005.11**: Add feedparser==6.0.10 to requirements.txt
- [ ] **EXT-005.12**: Add openai==1.6.1 to requirements.txt
- [ ] **EXT-005.13**: Add anthropic==0.8.1 to requirements.txt
- [ ] **EXT-005.14**: Add langchain==0.1.0 to requirements.txt
- [ ] **EXT-005.15**: Add tenacity==8.2.3 to requirements.txt
- [ ] **EXT-005.16**: Add tiktoken==0.5.2 to requirements.txt
- [ ] **EXT-005.17**: Add reppy==0.4.14 to requirements.txt (for robots.txt checking)
- [ ] **EXT-005.18**: Add pytest==7.4.3 to requirements.txt
- [ ] **EXT-005.19**: Add pytest-django==4.7.0 to requirements.txt
- [ ] **EXT-005.20**: Add factory-boy==3.3.0 to requirements.txt
- [ ] **EXT-005.21**: Add Pillow==10.1.0 to requirements.txt
- [ ] **EXT-005.22**: Add django-ckeditor==6.7.0 to requirements.txt
- [ ] **EXT-005.23**: Create `requirements-dev.txt` for development tools
- [ ] **EXT-005.24**: Add pytest-cov to requirements-dev.txt
- [ ] **EXT-005.25**: Add black to requirements-dev.txt
- [ ] **EXT-005.26**: Add flake8 to requirements-dev.txt
- [ ] **EXT-005.27**: Install all dependencies: `pip install -r requirements.txt`
- [ ] **EXT-005.28**: Verify installation: `pip list`
- [ ] **EXT-005.29**: Test imports in Python shell: `import django, celery, scrapy, openai, anthropic`
- [ ] **EXT-005.30**: Check for security vulnerabilities: `pip check`
- [ ] **EXT-005.31**: Generate frozen requirements: `pip freeze > requirements-frozen.txt`

---

### EXT-006: Environment Configuration

- [ ] **EXT-006.1**: Review `.env.example` file created in EXT-001
- [ ] **EXT-006.2**: Add SECRET_KEY to .env.example (with placeholder value)
- [ ] **EXT-006.3**: Add DEBUG to .env.example (default: True)
- [ ] **EXT-006.4**: Add ALLOWED_HOSTS to .env.example (default: localhost,127.0.0.1)
- [ ] **EXT-006.5**: Add DB_NAME to .env.example (default: extradime_db)
- [ ] **EXT-006.6**: Add DB_USER to .env.example (default: extradime_user)
- [ ] **EXT-006.7**: Add DB_PASSWORD to .env.example (placeholder)
- [ ] **EXT-006.8**: Add DB_HOST to .env.example (default: localhost)
- [ ] **EXT-006.9**: Add DB_PORT to .env.example (default: 5432)
- [ ] **EXT-006.10**: Add CELERY_BROKER_URL to .env.example (default: redis://localhost:6379/0)
- [ ] **EXT-006.11**: Add CELERY_RESULT_BACKEND to .env.example (default: redis://localhost:6379/0)
- [ ] **EXT-006.12**: Add OPENAI_API_KEY to .env.example (placeholder)
- [ ] **EXT-006.13**: Add ANTHROPIC_API_KEY to .env.example (placeholder)
- [ ] **EXT-006.14**: Add OPENAI_MODEL to .env.example (default: gpt-4)
- [ ] **EXT-006.15**: Add ANTHROPIC_MODEL to .env.example (default: claude-3-sonnet-20240229)
- [ ] **EXT-006.16**: Add EMAIL_HOST to .env.example (placeholder)
- [ ] **EXT-006.17**: Add EMAIL_PORT to .env.example (default: 587)
- [ ] **EXT-006.18**: Add EMAIL_HOST_USER to .env.example (placeholder)
- [ ] **EXT-006.19**: Add EMAIL_HOST_PASSWORD to .env.example (placeholder)
- [ ] **EXT-006.20**: Copy .env.example to .env: `cp .env.example .env`
- [ ] **EXT-006.21**: Fill in actual values in .env file (SECRET_KEY, DB_PASSWORD, API keys)
- [ ] **EXT-006.22**: Generate SECRET_KEY: `python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"`
- [ ] **EXT-006.23**: Update SECRET_KEY in .env with generated value
- [ ] **EXT-006.24**: Verify .env is in .gitignore
- [ ] **EXT-006.25**: Test environment variables load: `python manage.py shell` and check `settings.SECRET_KEY`

---

### EXT-007: Logging Configuration

- [ ] **EXT-007.1**: Create logs directory: `mkdir -p logs`
- [ ] **EXT-007.2**: Create `logs/.gitkeep` file to track empty directory
- [ ] **EXT-007.3**: Update `.gitignore` to add `logs/*.log`
- [ ] **EXT-007.4**: Open `extradime/settings/base.py` for editing
- [ ] **EXT-007.5**: Add LOGGING configuration dictionary to base.py
- [ ] **EXT-007.6**: Configure 'verbose' formatter with levelname, asctime, module, message
- [ ] **EXT-007.7**: Configure 'file' handler with RotatingFileHandler
- [ ] **EXT-007.8**: Set file handler filename to 'logs/django.log'
- [ ] **EXT-007.9**: Set file handler maxBytes to 15MB (1024*1024*15)
- [ ] **EXT-007.10**: Set file handler backupCount to 10
- [ ] **EXT-007.11**: Configure 'console' handler with StreamHandler
- [ ] **EXT-007.12**: Add 'django' logger with file and console handlers
- [ ] **EXT-007.13**: Add 'celery' logger with separate log file 'logs/celery.log'
- [ ] **EXT-007.14**: Add 'scrapy' logger with separate log file 'logs/scrapy.log'
- [ ] **EXT-007.15**: Add 'apps' logger for application-specific logging
- [ ] **EXT-007.16**: Update `extradime/settings/development.py` to set log level to DEBUG
- [ ] **EXT-007.17**: Update `extradime/settings/production.py` to set log level to INFO
- [ ] **EXT-007.18**: Run Django server: `python manage.py runserver`
- [ ] **EXT-007.19**: Verify logs/django.log file created
- [ ] **EXT-007.20**: Check log file contains formatted log entries
- [ ] **EXT-007.21**: Verify console output shows DEBUG level in development
- [ ] **EXT-007.22**: Test log rotation by creating large log file (optional)
- [ ] **EXT-007.23**: Trigger an error and verify it's logged properly
- [ ] **EXT-007.24**: Check log format is readable and contains all required fields
- [ ] **EXT-007.25**: Git add and commit: `git add extradime/settings logs/.gitkeep .gitignore && git commit -m "Add logging configuration"`
- [ ] **EXT-007.26**: Git push: `git push origin master`

---

### EXT-009: Git Repository Initialization

- [ ] **EXT-009.1**: Initialize Git repository: `git init`
- [ ] **EXT-009.2**: Verify .gitignore exists and includes: venv/, .env, *.pyc, __pycache__/, db.sqlite3
- [ ] **EXT-009.3**: Add *.log to .gitignore (if not already added in EXT-007)
- [ ] **EXT-009.4**: Add .DS_Store to .gitignore (for macOS)
- [ ] **EXT-009.5**: Add media/ to .gitignore
- [ ] **EXT-009.6**: Add staticfiles/ to .gitignore
- [ ] **EXT-009.7**: Stage all files: `git add .`
- [ ] **EXT-009.8**: Create initial commit: `git commit -m "Initial Django project setup"`
- [ ] **EXT-009.9**: Create GitHub repository (if using GitHub)
- [ ] **EXT-009.10**: Add remote: `git remote add origin <repository-url>`
- [ ] **EXT-009.11**: Push to remote: `git push -u origin master`
- [ ] **EXT-009.12**: Verify repository on GitHub/remote

---

### EXT-010: Docker Configuration (Optional)

- [ ] **EXT-010.1**: Create `Dockerfile` in project root
- [ ] **EXT-010.2**: Write Dockerfile with Python 3.11 base image
- [ ] **EXT-010.3**: Add WORKDIR /app to Dockerfile
- [ ] **EXT-010.4**: Add COPY requirements.txt to Dockerfile
- [ ] **EXT-010.5**: Add RUN pip install to Dockerfile
- [ ] **EXT-010.6**: Add COPY . /app to Dockerfile
- [ ] **EXT-010.7**: Add EXPOSE 8000 to Dockerfile
- [ ] **EXT-010.8**: Add CMD to Dockerfile
- [ ] **EXT-010.9**: Create `docker-compose.yml` in project root
- [ ] **EXT-010.10**: Configure web service in docker-compose.yml
- [ ] **EXT-010.11**: Configure db service (PostgreSQL) in docker-compose.yml
- [ ] **EXT-010.12**: Configure redis service in docker-compose.yml
- [ ] **EXT-010.13**: Configure celery_worker service in docker-compose.yml
- [ ] **EXT-010.14**: Configure celery_beat service in docker-compose.yml
- [ ] **EXT-010.15**: Configure volumes for code and database in docker-compose.yml
- [ ] **EXT-010.16**: Configure networks in docker-compose.yml
- [ ] **EXT-010.17**: Add health checks for services in docker-compose.yml
- [ ] **EXT-010.18**: Build Docker image: `docker-compose build`
- [ ] **EXT-010.19**: Start services: `docker-compose up`
- [ ] **EXT-010.20**: Verify all services healthy: `docker-compose ps`
- [ ] **EXT-010.21**: Access Django in Docker: http://localhost:8000/
- [ ] **EXT-010.22**: Check logs: `docker-compose logs`
- [ ] **EXT-010.23**: Stop services: `docker-compose down`
- [ ] **EXT-010.24**: Test database persistence: restart and verify data remains

---

## Epic 1.2: Scraping Infrastructure (Week 3-4)

### EXT-010: Scraping App Models

- [ ] **EXT-010.1**: Create test directory: `mkdir -p apps/scraping/tests && touch apps/scraping/tests/__init__.py`
- [ ] **EXT-010.2**: Create `apps/scraping/tests/test_models.py` file
- [ ] **EXT-010.3**: Write unit test for DataSource model creation
- [ ] **EXT-010.4**: Write unit test for DataSource.needs_check property
- [ ] **EXT-010.5**: Write unit test for DataSource.mark_checked() method
- [ ] **EXT-010.6**: Write unit test for DataSource.record_error() method
- [ ] **EXT-010.7**: Write unit test for DataSource.increment_opportunities_found() method
- [ ] **EXT-010.8**: Write unit test for DataSource auto-deactivation after 5 errors
- [ ] **EXT-010.9**: Write unit test for ScrapedOpportunity model creation
- [ ] **EXT-010.10**: Write unit test for ScrapedOpportunity.mark_processed() method
- [ ] **EXT-010.11**: Write unit test for ScrapedOpportunity.mark_rejected() method
- [ ] **EXT-010.12**: Write unit test for ScrapedOpportunity.mark_used_in_content() method
- [ ] **EXT-010.13**: Write unit test for ScrapedOpportunity.is_new property
- [ ] **EXT-010.14**: Write unit test for ScrapedOpportunity.age_in_days property
- [ ] **EXT-010.15**: Create scraping app: `python manage.py startapp scraping apps/scraping`
- [ ] **EXT-010.16**: Add 'apps.scraping' to INSTALLED_APPS in base.py
- [ ] **EXT-010.17**: Create `apps/scraping/models.py` file
- [ ] **EXT-010.18**: Implement DataSource model with all fields (name, url, feed_url, source_type, etc.)
- [ ] **EXT-010.19**: Implement DataSource Meta class with ordering and indexes
- [ ] **EXT-010.20**: Implement DataSource.__str__() method
- [ ] **EXT-010.21**: Implement DataSource.needs_check property
- [ ] **EXT-010.22**: Implement DataSource.mark_checked() method
- [ ] **EXT-010.23**: Implement DataSource.record_error() method with auto-deactivation logic
- [ ] **EXT-010.24**: Implement DataSource.increment_opportunities_found() method
- [ ] **EXT-010.25**: Implement ScrapedOpportunity model with all fields (title, description, url, etc.)
- [ ] **EXT-010.26**: Implement ScrapedOpportunity Meta class with ordering and indexes
- [ ] **EXT-010.27**: Implement ScrapedOpportunity.__str__() method
- [ ] **EXT-010.28**: Implement ScrapedOpportunity.mark_processed() method
- [ ] **EXT-010.29**: Implement ScrapedOpportunity.mark_rejected() method
- [ ] **EXT-010.30**: Implement ScrapedOpportunity.mark_used_in_content() method
- [ ] **EXT-010.31**: Implement ScrapedOpportunity.is_new property
- [ ] **EXT-010.32**: Implement ScrapedOpportunity.age_in_days property
- [ ] **EXT-010.33**: Create migrations: `python manage.py makemigrations scraping`
- [ ] **EXT-010.34**: Review migration file for correctness
- [ ] **EXT-010.35**: Apply migrations: `python manage.py migrate`
- [ ] **EXT-010.36**: Run tests: `pytest apps/scraping/tests/test_models.py -v`
- [ ] **EXT-010.37**: Fix any failing tests (debug and re-run until all pass)
- [ ] **EXT-010.38**: Test model creation in Django shell: create DataSource instance
- [ ] **EXT-010.39**: Test model creation in Django shell: create ScrapedOpportunity instance
- [ ] **EXT-010.40**: Test relationships: verify ScrapedOpportunity.source ForeignKey works
- [ ] **EXT-010.41**: Git add and commit: `git add apps/scraping && git commit -m "Add scraping models with tests"`
- [ ] **EXT-010.42**: Git push: `git push origin master`

---

### EXT-011: Scraping Admin Interface

- [ ] **EXT-011.1**: Create `apps/scraping/admin.py` file
- [ ] **EXT-011.2**: Import DataSource and ScrapedOpportunity models
- [ ] **EXT-011.3**: Create DataSourceAdmin class
- [ ] **EXT-011.4**: Configure DataSourceAdmin.list_display (name, source_type, is_active, last_checked, total_opportunities_found, error_count)
- [ ] **EXT-011.5**: Configure DataSourceAdmin.list_filter (source_type, is_active)
- [ ] **EXT-011.6**: Configure DataSourceAdmin.search_fields (name, url)
- [ ] **EXT-011.7**: Configure DataSourceAdmin.readonly_fields (last_checked, total_opportunities_found, error_count, created_at, updated_at)
- [ ] **EXT-011.8**: Implement activate_sources admin action
- [ ] **EXT-011.9**: Implement deactivate_sources admin action
- [ ] **EXT-011.10**: Implement run_spider_now admin action (placeholder for now)
- [ ] **EXT-011.11**: Add actions to DataSourceAdmin
- [ ] **EXT-011.12**: Register DataSourceAdmin with admin site
- [ ] **EXT-011.13**: Create ScrapedOpportunityAdmin class
- [ ] **EXT-011.14**: Configure ScrapedOpportunityAdmin.list_display (title, source, status, date_discovered, quality_score)
- [ ] **EXT-011.15**: Configure ScrapedOpportunityAdmin.list_filter (status, source, date_discovered)
- [ ] **EXT-011.16**: Configure ScrapedOpportunityAdmin.search_fields (title, description, url)
- [ ] **EXT-011.17**: Configure ScrapedOpportunityAdmin.readonly_fields (date_discovered, processed_at, raw_data)
- [ ] **EXT-011.18**: Implement mark_as_processed admin action
- [ ] **EXT-011.19**: Implement mark_as_rejected admin action
- [ ] **EXT-011.20**: Implement mark_as_used admin action
- [ ] **EXT-011.21**: Add actions to ScrapedOpportunityAdmin
- [ ] **EXT-011.22**: Register ScrapedOpportunityAdmin with admin site
- [ ] **EXT-011.23**: Run Django server: `python manage.py runserver`
- [ ] **EXT-011.24**: Access admin: http://localhost:8000/admin/scraping/
- [ ] **EXT-011.25**: Verify DataSource admin displays correctly
- [ ] **EXT-011.26**: Verify ScrapedOpportunity admin displays correctly
- [ ] **EXT-011.27**: Test all filters (source_type, is_active, status, date ranges)
- [ ] **EXT-011.28**: Test search functionality (search for DataSource by name, ScrapedOpportunity by title)
- [ ] **EXT-011.29**: Create test DataSource via admin and verify display
- [ ] **EXT-011.30**: Create test ScrapedOpportunity via admin and verify display
- [ ] **EXT-011.31**: Test custom actions (activate, deactivate, mark as processed)
- [ ] **EXT-011.32**: Verify statistics display correctly (total_opportunities_found, error_count, last_checked)
- [ ] **EXT-011.33**: Test inline editing (change is_active, check_frequency_hours)
- [ ] **EXT-011.34**: Verify all CRUD operations accessible within 2 clicks
- [ ] **EXT-011.35**: Verify clear field labels and helpful error messages
- [ ] **EXT-011.36**: Git add and commit: `git add apps/scraping/admin.py && git commit -m "Add scraping admin interface"`
- [ ] **EXT-011.37**: Git push: `git push origin master`

---

### EXT-012: Scrapy Project Setup

- [ ] **EXT-012.1**: Create `apps/scraping/scrapy.cfg` file
- [ ] **EXT-012.2**: Configure scrapy.cfg with project settings
- [ ] **EXT-012.3**: Create `apps/scraping/settings.py` for Scrapy settings
- [ ] **EXT-012.4**: Configure BOT_NAME = 'extradime_scraper' in Scrapy settings
- [ ] **EXT-012.5**: Configure ROBOTSTXT_OBEY = True in Scrapy settings
- [ ] **EXT-012.6**: Configure DOWNLOAD_DELAY = 2 in Scrapy settings
- [ ] **EXT-012.7**: Configure CONCURRENT_REQUESTS = 8 in Scrapy settings
- [ ] **EXT-012.8**: Configure USER_AGENT from environment variable in Scrapy settings
- [ ] **EXT-012.9**: Create `apps/scraping/items.py` file
- [ ] **EXT-012.10**: Define OpportunityItem class with fields matching ScrapedOpportunity model
- [ ] **EXT-012.11**: Create `apps/scraping/pipelines.py` file
- [ ] **EXT-012.12**: Implement DjangoOrmPipeline class
- [ ] **EXT-012.13**: Implement DjangoOrmPipeline.process_item() to save to database
- [ ] **EXT-012.14**: Implement duplicate checking in pipeline (check by URL)
- [ ] **EXT-012.15**: Implement DataSource statistics update in pipeline
- [ ] **EXT-012.16**: Implement error logging in pipeline
- [ ] **EXT-012.17**: Enable pipeline in Scrapy settings
- [ ] **EXT-012.18**: Create `apps/scraping/middlewares.py` file
- [ ] **EXT-012.19**: Implement error handling middleware (if needed)
- [ ] **EXT-012.20**: Create `apps/scraping/spiders/__init__.py` file
- [ ] **EXT-012.21**: Update `extradime/settings/base.py` to add Django-Scrapy integration
- [ ] **EXT-012.22**: Add Django setup code to Scrapy settings (os.environ, django.setup())
- [ ] **EXT-012.23**: Verify Scrapy settings load correctly: `scrapy settings --get BOT_NAME`
- [ ] **EXT-012.24**: Test pipeline with mock data in Django shell
- [ ] **EXT-012.25**: Verify Django models accessible from Scrapy context
- [ ] **EXT-012.26**: Test duplicate handling (create duplicate opportunity and verify it's skipped)
- [ ] **EXT-012.27**: Run `scrapy list` (should show no spiders yet, but command should work)
- [ ] **EXT-012.28**: Git add and commit: `git add apps/scraping && git commit -m "Add Scrapy project setup"`
- [ ] **EXT-012.29**: Git push: `git push origin master`

---

### EXT-013: Base Spider Implementation

- [ ] **EXT-013.1**: Create test file: `apps/scraping/tests/test_spiders.py`
- [ ] **EXT-013.2**: Write unit test for BaseSpider.check_robots_txt() with allowed URL
- [ ] **EXT-013.3**: Write unit test for BaseSpider.check_robots_txt() with blocked URL
- [ ] **EXT-013.4**: Write unit test for BaseSpider.check_robots_txt() with unavailable robots.txt
- [ ] **EXT-013.5**: Write unit test for BaseSpider.handle_error() with TimeoutError
- [ ] **EXT-013.6**: Write unit test for BaseSpider.handle_error() with ConnectionRefusedError
- [ ] **EXT-013.7**: Write unit test for BaseSpider.handle_error() with DNSLookupError
- [ ] **EXT-013.8**: Write unit test for BaseSpider.extract_text() with valid XPath
- [ ] **EXT-013.9**: Write unit test for BaseSpider.extract_text() with invalid XPath
- [ ] **EXT-013.10**: Write unit test for BaseSpider.extract_url() with absolute URL
- [ ] **EXT-013.11**: Write unit test for BaseSpider.extract_url() with relative URL
- [ ] **EXT-013.12**: Create `apps/scraping/spiders/base_spider.py` file
- [ ] **EXT-013.13**: Import required modules (scrapy, logging, reppy, twisted.internet.error)
- [ ] **EXT-013.14**: Create BaseSpider class inheriting from scrapy.Spider
- [ ] **EXT-013.15**: Configure custom_settings in BaseSpider (DOWNLOAD_DELAY, CONCURRENT_REQUESTS_PER_DOMAIN, etc.)
- [ ] **EXT-013.16**: Implement BaseSpider.__init__() with robots_cache
- [ ] **EXT-013.17**: Implement BaseSpider.check_robots_txt() method (complete implementation from ticket)
- [ ] **EXT-013.18**: Implement BaseSpider.handle_error() method (complete implementation from ticket)
- [ ] **EXT-013.19**: Implement BaseSpider.extract_text() method (complete implementation from ticket)
- [ ] **EXT-013.20**: Implement BaseSpider.extract_url() method (complete implementation from ticket)
- [ ] **EXT-013.21**: Implement BaseSpider.parse_common() method (raises NotImplementedError)
- [ ] **EXT-013.22**: Create `apps/scraping/robots_checker.py` file (if additional utilities needed)
- [ ] **EXT-013.23**: Run tests: `pytest apps/scraping/tests/test_spiders.py -v`
- [ ] **EXT-013.24**: Fix any failing tests (debug and re-run until all pass)
- [ ] **EXT-013.25**: Test robots.txt checking with real URL in Django shell
- [ ] **EXT-013.26**: Test error handling with mock failures
- [ ] **EXT-013.27**: Test text/URL extraction methods with mock selectors
- [ ] **EXT-013.28**: Git add and commit: `git add apps/scraping/spiders && git commit -m "Add BaseSpider with complete implementations"`
- [ ] **EXT-013.29**: Git push: `git push origin master`

---

### EXT-014: RSS Feed Spider

- [ ] **EXT-014.1**: Create test file: `apps/scraping/tests/test_rss_spider.py`
- [ ] **EXT-014.2**: Create test fixture directory: `mkdir -p apps/scraping/tests/fixtures`
- [ ] **EXT-014.3**: Create test fixture: `apps/scraping/tests/fixtures/sample_rss.xml`
- [ ] **EXT-014.4**: Write sample RSS 2.0 feed in fixture file (with 3-5 items)
- [ ] **EXT-014.5**: Write unit test for RSSSpider parsing RSS 2.0 feed
- [ ] **EXT-014.6**: Write unit test for RSSSpider parsing Atom feed
- [ ] **EXT-014.7**: Write unit test for RSSSpider handling missing fields gracefully
- [ ] **EXT-014.8**: Write unit test for RSSSpider handling malformed feed
- [ ] **EXT-014.9**: Write integration test with real feed (Reddit RSS)
- [ ] **EXT-014.10**: Create `apps/scraping/spiders/rss_spider.py` file
- [ ] **EXT-014.11**: Import BaseSpider and feedparser
- [ ] **EXT-014.12**: Create RSSSpider class inheriting from BaseSpider
- [ ] **EXT-014.13**: Set spider name = 'rss'
- [ ] **EXT-014.14**: Implement __init__() to accept feed_url and source_id arguments
- [ ] **EXT-014.15**: Implement start_requests() to yield Request for feed_url
- [ ] **EXT-014.16**: Implement parse() method to parse feed with feedparser
- [ ] **EXT-014.17**: Extract title from entry.title
- [ ] **EXT-014.18**: Extract description from entry.summary or entry.description
- [ ] **EXT-014.19**: Extract url from entry.link
- [ ] **EXT-014.20**: Store entire entry as raw_data (JSON)
- [ ] **EXT-014.21**: Create OpportunityItem for each entry
- [ ] **EXT-014.22**: Handle different feed formats (RSS 2.0, Atom, RSS 1.0)
- [ ] **EXT-014.23**: Handle malformed feeds gracefully (try/except)
- [ ] **EXT-014.24**: Log parsing errors
- [ ] **EXT-014.25**: Update DataSource.last_checked timestamp
- [ ] **EXT-014.26**: Run tests: `pytest apps/scraping/tests/test_rss_spider.py -v`
- [ ] **EXT-014.27**: Fix any failing tests
- [ ] **EXT-014.28**: Test with sample RSS feed fixture
- [ ] **EXT-014.29**: Test with malformed feed
- [ ] **EXT-014.30**: Integration test with real feed: `scrapy crawl rss -a feed_url=https://www.reddit.com/r/beermoney/.rss -a source_id=1`
- [ ] **EXT-014.31**: Verify data saved to database (check ScrapedOpportunity table)
- [ ] **EXT-014.32**: Verify DataSource statistics updated
- [ ] **EXT-014.33**: Git add and commit: `git add apps/scraping/spiders/rss_spider.py apps/scraping/tests && git commit -m "Add RSS feed spider"`
- [ ] **EXT-014.34**: Git push: `git push origin master`

---

### EXT-015: Website Spider Template

- [ ] **EXT-015.1**: Create test file: `apps/scraping/tests/test_website_spider.py`
- [ ] **EXT-015.2**: Create test fixture: `apps/scraping/tests/fixtures/sample_html.html`
- [ ] **EXT-015.3**: Write sample HTML page in fixture file (with structured data)
- [ ] **EXT-015.4**: Write unit test for WebsiteSpider parsing HTML with CSS selectors
- [ ] **EXT-015.5**: Write unit test for WebsiteSpider parsing HTML with XPath selectors
- [ ] **EXT-015.6**: Write unit test for WebsiteSpider handling pagination
- [ ] **EXT-015.7**: Write unit test for WebsiteSpider handling missing elements
- [ ] **EXT-015.8**: Write unit test for WebsiteSpider respecting robots.txt
- [ ] **EXT-015.9**: Create `apps/scraping/spiders/website_spider.py` file
- [ ] **EXT-015.10**: Import BaseSpider and required modules
- [ ] **EXT-015.11**: Create WebsiteSpider class inheriting from BaseSpider
- [ ] **EXT-015.12**: Set spider name = 'website'
- [ ] **EXT-015.13**: Implement __init__() to accept url, source_id, and custom_settings
- [ ] **EXT-015.14**: Load custom_settings from DataSource (CSS/XPath selectors)
- [ ] **EXT-015.15**: Implement start_requests() to yield Request for start URL
- [ ] **EXT-015.16**: Implement parse() method to extract data using selectors
- [ ] **EXT-015.17**: Extract title using configurable selector
- [ ] **EXT-015.18**: Extract description using configurable selector
- [ ] **EXT-015.19**: Extract URL using configurable selector
- [ ] **EXT-015.20**: Handle pagination (extract next page URL and follow)
- [ ] **EXT-015.21**: Create OpportunityItem for each extracted opportunity
- [ ] **EXT-015.22**: Handle missing elements gracefully (use default values)
- [ ] **EXT-015.23**: Respect robots.txt (call check_robots_txt())
- [ ] **EXT-015.24**: Implement rate limiting (use DOWNLOAD_DELAY)
- [ ] **EXT-015.25**: Add error handling for missing selectors
- [ ] **EXT-015.26**: Run tests: `pytest apps/scraping/tests/test_website_spider.py -v`
- [ ] **EXT-015.27**: Fix any failing tests
- [ ] **EXT-015.28**: Test with sample HTML fixture
- [ ] **EXT-015.29**: Test pagination handling
- [ ] **EXT-015.30**: Test with real website (if available)
- [ ] **EXT-015.31**: Git add and commit: `git add apps/scraping/spiders/website_spider.py apps/scraping/tests && git commit -m "Add website spider template"`
- [ ] **EXT-015.32**: Git push: `git push origin master`

---

### EXT-016: Scraping Task Scheduler

- [ ] **EXT-016.1**: Create test file: `apps/scraping/tests/test_tasks.py`
- [ ] **EXT-016.2**: Write unit test for run_spider_task() with RSS spider
- [ ] **EXT-016.3**: Write unit test for run_spider_task() with website spider
- [ ] **EXT-016.4**: Write unit test for run_spider_task() error handling
- [ ] **EXT-016.5**: Write unit test for schedule_all_active_sources()
- [ ] **EXT-016.6**: Write unit test for check_sources_needing_scrape()
- [ ] **EXT-016.7**: Create `apps/scraping/tasks.py` file
- [ ] **EXT-016.8**: Import Celery, Scrapy, and required modules
- [ ] **EXT-016.9**: Implement run_spider_task(source_id, spider_name) as @shared_task
- [ ] **EXT-016.10**: In run_spider_task, get DataSource by ID
- [ ] **EXT-016.11**: In run_spider_task, configure spider based on source_type
- [ ] **EXT-016.12**: In run_spider_task, run spider using CrawlerProcess
- [ ] **EXT-016.13**: In run_spider_task, handle spider errors and update DataSource
- [ ] **EXT-016.14**: In run_spider_task, call DataSource.mark_checked() on success
- [ ] **EXT-016.15**: In run_spider_task, call DataSource.record_error() on failure
- [ ] **EXT-016.16**: Implement schedule_all_active_sources() as @shared_task
- [ ] **EXT-016.17**: In schedule_all_active_sources, query all active DataSources
- [ ] **EXT-016.18**: In schedule_all_active_sources, queue run_spider_task for each source
- [ ] **EXT-016.19**: Implement check_sources_needing_scrape() as @shared_task
- [ ] **EXT-016.20**: In check_sources_needing_scrape, query sources where needs_check=True
- [ ] **EXT-016.21**: In check_sources_needing_scrape, queue run_spider_task for each
- [ ] **EXT-016.22**: Configure Celery Beat schedule in settings/base.py
- [ ] **EXT-016.23**: Add periodic task: check_sources_needing_scrape every 1 hour
- [ ] **EXT-016.24**: Run tests: `pytest apps/scraping/tests/test_tasks.py -v`
- [ ] **EXT-016.25**: Fix any failing tests
- [ ] **EXT-016.26**: Test run_spider_task manually in Django shell
- [ ] **EXT-016.27**: Verify Celery Beat schedule: `celery -A extradime beat -l info`
- [ ] **EXT-016.28**: Verify periodic task executes (check logs)
- [ ] **EXT-016.29**: Git add and commit: `git add apps/scraping/tasks.py extradime/settings/base.py && git commit -m "Add scraping task scheduler"`
- [ ] **EXT-016.30**: Git push: `git push origin master`

---

### EXT-017: Error Handling and Logging

- [ ] **EXT-017.1**: Create `apps/scraping/logging_config.py` file
- [ ] **EXT-017.2**: Configure logging for scraping module (file and console handlers)
- [ ] **EXT-017.3**: Set log level to INFO for production, DEBUG for development
- [ ] **EXT-017.4**: Create log directory: `mkdir -p logs`
- [ ] **EXT-017.5**: Configure rotating file handler (max 10MB, 5 backups)
- [ ] **EXT-017.6**: Add logs/ to .gitignore
- [ ] **EXT-017.7**: Update `apps/scraping/spiders/base_spider.py` to use configured logger
- [ ] **EXT-017.8**: Update `apps/scraping/tasks.py` to use configured logger
- [ ] **EXT-017.9**: Update `apps/scraping/pipelines.py` to use configured logger
- [ ] **EXT-017.10**: Add error logging for spider failures
- [ ] **EXT-017.11**: Add error logging for pipeline failures
- [ ] **EXT-017.12**: Add error logging for task failures
- [ ] **EXT-017.13**: Create `apps/scraping/exceptions.py` for custom exceptions
- [ ] **EXT-017.14**: Define SpiderConfigurationError exception
- [ ] **EXT-017.15**: Define DataSourceInactiveError exception
- [ ] **EXT-017.16**: Define RobotsTxtBlockedError exception
- [ ] **EXT-017.17**: Update spiders to raise custom exceptions
- [ ] **EXT-017.18**: Update tasks to catch and handle custom exceptions
- [ ] **EXT-017.19**: Test error logging by triggering various errors
- [ ] **EXT-017.20**: Verify logs written to logs/scraping.log
- [ ] **EXT-017.21**: Verify log rotation works (create large log file)
- [ ] **EXT-017.22**: Verify error emails sent for critical errors (if configured)
- [ ] **EXT-017.23**: Git add and commit: `git add apps/scraping && git commit -m "Add error handling and logging"`
- [ ] **EXT-017.24**: Git push: `git push origin master`

---

## Epic 1.3: Content Management (Week 5-6)

### EXT-018: Content App Models

- [ ] **EXT-018.1**: Create test directory: `mkdir -p apps/content/tests && touch apps/content/tests/__init__.py`
- [ ] **EXT-018.2**: Create `apps/content/tests/test_models.py` file
- [ ] **EXT-018.3**: Write unit test for Topic model creation
- [ ] **EXT-018.4**: Write unit test for Topic slug auto-generation
- [ ] **EXT-018.5**: Write unit test for Article model creation
- [ ] **EXT-018.6**: Write unit test for Article.save() with slug generation
- [ ] **EXT-018.7**: Write unit test for Article.create_revision() method
- [ ] **EXT-018.8**: Write unit test for Article.get_latest_revision() method
- [ ] **EXT-018.9**: Write unit test for Article with multiple topics (ManyToMany)
- [ ] **EXT-018.10**: Write unit test for Article with source_opportunities (ManyToMany)
- [ ] **EXT-018.11**: Write unit test for PromptLog model creation
- [ ] **EXT-018.12**: Write unit test for ContentRevision model creation
- [ ] **EXT-018.13**: Write unit test for ContentRevision ordering (most recent first)
- [ ] **EXT-018.14**: Create content app: `python manage.py startapp content apps/content`
- [ ] **EXT-018.15**: Add 'apps.content' to INSTALLED_APPS in base.py
- [ ] **EXT-018.16**: Create `apps/content/models.py` file
- [ ] **EXT-018.17**: Implement Topic model with fields (name, slug, description, created_at, updated_at)
- [ ] **EXT-018.18**: Implement Topic Meta class with ordering and unique constraint on slug
- [ ] **EXT-018.19**: Implement Topic.__str__() method
- [ ] **EXT-018.20**: Implement Topic.save() with slug auto-generation from name
- [ ] **EXT-018.21**: Implement Article model with all fields (title, slug, body, status, author, etc.)
- [ ] **EXT-018.22**: Add Article.topics ManyToManyField to Topic
- [ ] **EXT-018.23**: Add Article.source_opportunities ManyToManyField to ScrapedOpportunity
- [ ] **EXT-018.24**: Implement Article Meta class with ordering and indexes
- [ ] **EXT-018.25**: Implement Article.__str__() method
- [ ] **EXT-018.26**: Implement Article.save() with slug auto-generation from title
- [ ] **EXT-018.27**: Implement Article.create_revision() method
- [ ] **EXT-018.28**: Implement Article.get_latest_revision() method
- [ ] **EXT-018.29**: Implement PromptLog model with fields (prompt_text, response_text, llm_used, metadata, created_at)
- [ ] **EXT-018.30**: Implement PromptLog Meta class with ordering
- [ ] **EXT-018.31**: Implement PromptLog.__str__() method
- [ ] **EXT-018.32**: Implement ContentRevision model with fields (article, content, revision_number, created_by, created_at)
- [ ] **EXT-018.33**: Implement ContentRevision Meta class with ordering and unique_together
- [ ] **EXT-018.34**: Implement ContentRevision.__str__() method
- [ ] **EXT-018.35**: Create migrations: `python manage.py makemigrations content`
- [ ] **EXT-018.36**: Review migration file for correctness
- [ ] **EXT-018.37**: Apply migrations: `python manage.py migrate`
- [ ] **EXT-018.38**: Run tests: `pytest apps/content/tests/test_models.py -v`
- [ ] **EXT-018.39**: Fix any failing tests
- [ ] **EXT-018.40**: Test Topic creation in Django shell
- [ ] **EXT-018.41**: Test Article creation in Django shell
- [ ] **EXT-018.42**: Test Article with topics relationship
- [ ] **EXT-018.43**: Test Article with source_opportunities relationship
- [ ] **EXT-018.44**: Test revision creation and retrieval
- [ ] **EXT-018.45**: Git add and commit: `git add apps/content && git commit -m "Add content models with tests"`
- [ ] **EXT-018.46**: Git push: `git push origin master`

---

### EXT-019: Content Admin Interface

- [ ] **EXT-019.1**: Install django-ckeditor: `pip install django-ckeditor==6.7.0 django-ckeditor-5`
- [ ] **EXT-019.2**: Add 'ckeditor' to INSTALLED_APPS in base.py
- [ ] **EXT-019.3**: Add 'ckeditor_uploader' to INSTALLED_APPS in base.py
- [ ] **EXT-019.4**: Configure CKEDITOR_UPLOAD_PATH in base.py
- [ ] **EXT-019.5**: Configure CKEDITOR_CONFIGS in base.py (toolbar, height, width)
- [ ] **EXT-019.6**: Run migrations for CKEditor: `python manage.py migrate`
- [ ] **EXT-019.7**: Create `apps/content/admin.py` file
- [ ] **EXT-019.8**: Import all content models and CKEditorWidget
- [ ] **EXT-019.9**: Create TopicAdmin class
- [ ] **EXT-019.10**: Configure TopicAdmin.list_display (name, slug, created_at)
- [ ] **EXT-019.11**: Configure TopicAdmin.prepopulated_fields for slug
- [ ] **EXT-019.12**: Register TopicAdmin with admin site
- [ ] **EXT-019.13**: Create ContentRevisionInline class (TabularInline)
- [ ] **EXT-019.14**: Configure ContentRevisionInline fields and readonly_fields
- [ ] **EXT-019.15**: Create ArticleAdminForm with CKEditorWidget for body field
- [ ] **EXT-019.16**: Create ArticleAdmin class
- [ ] **EXT-019.17**: Configure ArticleAdmin.form = ArticleAdminForm
- [ ] **EXT-019.18**: Configure ArticleAdmin.list_display (title, status, author, ai_generated, publish_date, created_at)
- [ ] **EXT-019.19**: Configure ArticleAdmin.list_filter (status, ai_generated, topics, publish_date)
- [ ] **EXT-019.20**: Configure ArticleAdmin.search_fields (title, body)
- [ ] **EXT-019.21**: Configure ArticleAdmin.readonly_fields (created_at, updated_at, generation_metadata)
- [ ] **EXT-019.22**: Configure ArticleAdmin.filter_horizontal for topics and source_opportunities
- [ ] **EXT-019.23**: Add ContentRevisionInline to ArticleAdmin.inlines
- [ ] **EXT-019.24**: Implement publish_articles admin action
- [ ] **EXT-019.25**: Implement send_to_review admin action
- [ ] **EXT-019.26**: Implement generate_draft admin action (placeholder)
- [ ] **EXT-019.27**: Add actions to ArticleAdmin
- [ ] **EXT-019.28**: Register ArticleAdmin with admin site
- [ ] **EXT-019.29**: Create PromptLogAdmin class (read-only)
- [ ] **EXT-019.30**: Configure PromptLogAdmin.list_display (llm_used, created_at, truncated_prompt)
- [ ] **EXT-019.31**: Configure PromptLogAdmin.list_filter (llm_used, created_at)
- [ ] **EXT-019.32**: Configure PromptLogAdmin.readonly_fields (all fields)
- [ ] **EXT-019.33**: Implement truncated_prompt method for display
- [ ] **EXT-019.34**: Register PromptLogAdmin with admin site
- [ ] **EXT-019.35**: Run Django server: `python manage.py runserver`
- [ ] **EXT-019.36**: Access admin: http://localhost:8000/admin/content/
- [ ] **EXT-019.37**: Verify Topic admin displays correctly
- [ ] **EXT-019.38**: Verify Article admin displays with CKEditor
- [ ] **EXT-019.39**: Test CKEditor functionality (formatting, images)
- [ ] **EXT-019.40**: Test review queue filter (status='review')
- [ ] **EXT-019.41**: Test custom actions (publish, send to review)
- [ ] **EXT-019.42**: Create test article and verify revision history visible
- [ ] **EXT-019.43**: Verify all CRUD operations accessible within 2 clicks
- [ ] **EXT-019.44**: Git add and commit: `git add apps/content/admin.py extradime/settings/base.py requirements.txt && git commit -m "Add content admin with CKEditor"`
- [ ] **EXT-019.45**: Git push: `git push origin master`

---

### EXT-020: Content Views and Templates

- [ ] **EXT-020.1**: Create `apps/content/views.py` file
- [ ] **EXT-020.2**: Import required Django views (ListView, DetailView)
- [ ] **EXT-020.3**: Implement ArticleListView (ListView)
- [ ] **EXT-020.4**: Configure ArticleListView queryset (published articles, ordered by publish_date)
- [ ] **EXT-020.5**: Configure ArticleListView pagination (10 per page)
- [ ] **EXT-020.6**: Implement ArticleDetailView (DetailView)
- [ ] **EXT-020.7**: Configure ArticleDetailView queryset (published articles only)
- [ ] **EXT-020.8**: Add get_context_data to ArticleDetailView (related articles, source opportunities)
- [ ] **EXT-020.9**: Implement OpportunityListView (ListView)
- [ ] **EXT-020.10**: Configure OpportunityListView queryset (processed opportunities, ordered by date_discovered)
- [ ] **EXT-020.11**: Configure OpportunityListView pagination (20 per page)
- [ ] **EXT-020.12**: Implement OpportunityDetailView (DetailView)
- [ ] **EXT-020.13**: Implement TopicListView (ListView)
- [ ] **EXT-020.14**: Implement TopicArticleListView (ListView filtered by topic)
- [ ] **EXT-020.15**: Configure TopicArticleListView to get topic from URL slug
- [ ] **EXT-020.16**: Create `apps/content/urls.py` file
- [ ] **EXT-020.17**: Add URL pattern for article_list
- [ ] **EXT-020.18**: Add URL pattern for article_detail (with slug)
- [ ] **EXT-020.19**: Add URL pattern for opportunity_list
- [ ] **EXT-020.20**: Add URL pattern for opportunity_detail (with pk)
- [ ] **EXT-020.21**: Add URL pattern for topic_list
- [ ] **EXT-020.22**: Add URL pattern for topic_articles (with slug)
- [ ] **EXT-020.23**: Update `extradime/urls.py` to include content.urls
- [ ] **EXT-020.24**: Create templates directory: `mkdir -p apps/content/templates/content`
- [ ] **EXT-020.25**: Create `apps/content/templates/content/article_list.html`
- [ ] **EXT-020.26**: Implement article_list.html extending base.html (with pagination)
- [ ] **EXT-020.27**: Create `apps/content/templates/content/article_detail.html`
- [ ] **EXT-020.28**: Implement article_detail.html with SEO meta tags
- [ ] **EXT-020.29**: Add related articles section to article_detail.html
- [ ] **EXT-020.30**: Add source opportunities section to article_detail.html
- [ ] **EXT-020.31**: Create `apps/content/templates/content/opportunity_list.html`
- [ ] **EXT-020.32**: Implement opportunity_list.html with pagination
- [ ] **EXT-020.33**: Create `apps/content/templates/content/opportunity_detail.html`
- [ ] **EXT-020.34**: Implement opportunity_detail.html with all opportunity details
- [ ] **EXT-020.35**: Create `apps/content/templates/content/topic_list.html`
- [ ] **EXT-020.36**: Implement topic_list.html with all topics
- [ ] **EXT-020.37**: Update `apps/core/templates/core/base.html` navigation links
- [ ] **EXT-020.38**: Add "Articles" link to navigation ({% url 'content:article_list' %})
- [ ] **EXT-020.39**: Add "Opportunities" link to navigation ({% url 'content:opportunity_list' %})
- [ ] **EXT-020.40**: Run Django server: `python manage.py runserver`
- [ ] **EXT-020.41**: Access article list: http://localhost:8000/articles/
- [ ] **EXT-020.42**: Create test article via admin and verify it displays
- [ ] **EXT-020.43**: Access article detail page and verify it renders
- [ ] **EXT-020.44**: Test pagination (create 15+ articles)
- [ ] **EXT-020.45**: Access opportunity list: http://localhost:8000/opportunities/
- [ ] **EXT-020.46**: Test responsive design on all pages (320px, 768px, 1024px+)
- [ ] **EXT-020.47**: Verify SEO meta tags in article detail page source
- [ ] **EXT-020.48**: Git add and commit: `git add apps/content && git commit -m "Add content views and templates"`
- [ ] **EXT-020.49**: Git push: `git push origin master`

---

### EXT-021: RSS Feeds

- [ ] **EXT-021.1**: Create `apps/content/feeds.py` file
- [ ] **EXT-021.2**: Import Feed and Atom1Feed from django.contrib.syndication
- [ ] **EXT-021.3**: Create ArticlesFeed class inheriting from Feed
- [ ] **EXT-021.4**: Configure ArticlesFeed.title, link, description
- [ ] **EXT-021.5**: Implement ArticlesFeed.items() to return latest 20 published articles
- [ ] **EXT-021.6**: Implement ArticlesFeed.item_title()
- [ ] **EXT-021.7**: Implement ArticlesFeed.item_description()
- [ ] **EXT-021.8**: Implement ArticlesFeed.item_link()
- [ ] **EXT-021.9**: Implement ArticlesFeed.item_pubdate()
- [ ] **EXT-021.10**: Implement ArticlesFeed.item_author_name()
- [ ] **EXT-021.11**: Create TopicFeed class inheriting from Feed
- [ ] **EXT-021.12**: Implement TopicFeed.get_object() to get topic by slug
- [ ] **EXT-021.13**: Implement TopicFeed.title() using topic name
- [ ] **EXT-021.14**: Implement TopicFeed.link() using topic slug
- [ ] **EXT-021.15**: Implement TopicFeed.description() using topic description
- [ ] **EXT-021.16**: Implement TopicFeed.items() to return articles for topic
- [ ] **EXT-021.17**: Update `apps/content/urls.py` to add feed URLs
- [ ] **EXT-021.18**: Add URL pattern for articles feed: /feeds/articles/
- [ ] **EXT-021.19**: Add URL pattern for topic feed: /feeds/topics/<slug>/
- [ ] **EXT-021.20**: Update `apps/core/templates/core/base.html` with feed autodiscovery
- [ ] **EXT-021.21**: Add <link rel="alternate" type="application/rss+xml"> to base.html head
- [ ] **EXT-021.22**: Run Django server: `python manage.py runserver`
- [ ] **EXT-021.23**: Access articles feed: http://localhost:8000/feeds/articles/
- [ ] **EXT-021.24**: Verify feed displays in browser (XML format)
- [ ] **EXT-021.25**: Validate feed: https://validator.w3.org/feed/ (paste feed URL)
- [ ] **EXT-021.26**: Test feed in feed reader (Feedly, RSS reader extension)
- [ ] **EXT-021.27**: Verify all fields present (title, description, link, pubDate, author)
- [ ] **EXT-021.28**: Test topic-specific feed with a topic slug
- [ ] **EXT-021.29**: Check feed autodiscovery in browser (view page source)
- [ ] **EXT-021.30**: Git add and commit: `git add apps/content && git commit -m "Add RSS feeds for articles and topics"`
- [ ] **EXT-021.31**: Git push: `git push origin master`

---

## Epic 1.4: AI Content Generation (Week 7-8)

### EXT-022: Prompt Templates Implementation

- [ ] **EXT-022.1**: Create `apps/content/prompts.py` file
- [ ] **EXT-022.2**: Define ARTICLE_GENERATION_PROMPT template
- [ ] **EXT-022.3**: Add placeholders: {opportunities}, {topic}, {tone}, {word_count}
- [ ] **EXT-022.4**: Add instructions for structure (intro, body, conclusion)
- [ ] **EXT-022.5**: Add instructions for SEO optimization
- [ ] **EXT-022.6**: Define TITLE_GENERATION_PROMPT template
- [ ] **EXT-022.7**: Add placeholders: {content}
- [ ] **EXT-022.8**: Add instructions for SEO-friendly titles (under 60 chars)
- [ ] **EXT-022.9**: Define META_DESCRIPTION_PROMPT template
- [ ] **EXT-022.10**: Add placeholders: {title}, {content}
- [ ] **EXT-022.11**: Add instructions for meta descriptions (under 160 chars)
- [ ] **EXT-022.12**: Define CONTENT_ENHANCEMENT_PROMPT template
- [ ] **EXT-022.13**: Add placeholders: {content}, {enhancement_type}
- [ ] **EXT-022.14**: Add instructions for improving readability, SEO, engagement
- [ ] **EXT-022.15**: Define MODERATION_PROMPT template
- [ ] **EXT-022.16**: Add placeholders: {content}
- [ ] **EXT-022.17**: Add instructions for checking quality, accuracy, appropriateness
- [ ] **EXT-022.18**: Define PERSONA_PROMPTS dictionary with different writing styles
- [ ] **EXT-022.19**: Add 'professional' persona prompt
- [ ] **EXT-022.20**: Add 'casual' persona prompt
- [ ] **EXT-022.21**: Add 'enthusiastic' persona prompt
- [ ] **EXT-022.22**: Add 'analytical' persona prompt
- [ ] **EXT-022.23**: Create documentation comment explaining each prompt's purpose
- [ ] **EXT-022.24**: Add examples of expected output for each prompt
- [ ] **EXT-022.25**: Git add and commit: `git add apps/content/prompts.py && git commit -m "Add AI prompt templates"`
- [ ] **EXT-022.26**: Git push: `git push origin master`

---

### EXT-023: AI Utility Functions

- [ ] **EXT-023.1**: Create test file: `apps/content/tests/test_ai_utils.py`
- [ ] **EXT-023.2**: Write unit test for call_openai_api() with mock response
- [ ] **EXT-023.3**: Write unit test for call_anthropic_api() with mock response
- [ ] **EXT-023.4**: Write unit test for retry logic on API failures
- [ ] **EXT-023.5**: Write unit test for token counting
- [ ] **EXT-023.6**: Write unit test for prompt logging
- [ ] **EXT-023.7**: Create `apps/content/ai_utils.py` file
- [ ] **EXT-023.8**: Import openai, anthropic, tenacity, tiktoken
- [ ] **EXT-023.9**: Implement count_tokens(text, model) function using tiktoken
- [ ] **EXT-023.10**: Implement log_prompt(prompt, response, llm_used, metadata) function
- [ ] **EXT-023.11**: In log_prompt, create PromptLog instance and save to database
- [ ] **EXT-023.12**: Implement call_openai_api(prompt, model, max_tokens, temperature) function
- [ ] **EXT-023.13**: Add @retry decorator with exponential backoff (3 attempts, 2s wait)
- [ ] **EXT-023.14**: In call_openai_api, initialize OpenAI client with API key from settings
- [ ] **EXT-023.15**: In call_openai_api, call client.chat.completions.create()
- [ ] **EXT-023.16**: In call_openai_api, extract response content
- [ ] **EXT-023.17**: In call_openai_api, log prompt and response
- [ ] **EXT-023.18**: In call_openai_api, return dict with content, tokens_used, model
- [ ] **EXT-023.19**: In call_openai_api, handle API errors (rate limit, invalid key, etc.)
- [ ] **EXT-023.20**: Implement call_anthropic_api(prompt, model, max_tokens, temperature) function
- [ ] **EXT-023.21**: Add @retry decorator with exponential backoff
- [ ] **EXT-023.22**: In call_anthropic_api, initialize Anthropic client with API key
- [ ] **EXT-023.23**: In call_anthropic_api, call client.messages.create()
- [ ] **EXT-023.24**: In call_anthropic_api, extract response content
- [ ] **EXT-023.25**: In call_anthropic_api, log prompt and response
- [ ] **EXT-023.26**: In call_anthropic_api, return dict with content, tokens_used, model
- [ ] **EXT-023.27**: In call_anthropic_api, handle API errors
- [ ] **EXT-023.28**: Implement choose_llm() function to select between OpenAI and Anthropic
- [ ] **EXT-023.29**: In choose_llm, check settings.DEFAULT_LLM or use fallback logic
- [ ] **EXT-023.30**: Run tests: `pytest apps/content/tests/test_ai_utils.py -v`
- [ ] **EXT-023.31**: Fix any failing tests
- [ ] **EXT-023.32**: Test call_openai_api manually in Django shell (with real API key)
- [ ] **EXT-023.33**: Test call_anthropic_api manually in Django shell (with real API key)
- [ ] **EXT-023.34**: Verify PromptLog entries created in database
- [ ] **EXT-023.35**: Test retry logic by temporarily using invalid API key
- [ ] **EXT-023.36**: Git add and commit: `git add apps/content/ai_utils.py apps/content/tests && git commit -m "Add AI utility functions with retry logic"`
- [ ] **EXT-023.37**: Git push: `git push origin master`

---

### EXT-024: Article Generation Tasks

- [ ] **EXT-024.1**: Create test file: `apps/content/tests/test_generation_tasks.py`
- [ ] **EXT-024.2**: Write unit test for generate_article_from_opportunities() with mocked LLM
- [ ] **EXT-024.3**: Write unit test for generate_title_from_content() with mocked LLM
- [ ] **EXT-024.4**: Write unit test for generate_meta_description() with mocked LLM
- [ ] **EXT-024.5**: Write unit test for enhance_article_content() with mocked LLM
- [ ] **EXT-024.6**: Write unit test for moderate_article_content() with mocked LLM
- [ ] **EXT-024.7**: Create `apps/content/tasks.py` file
- [ ] **EXT-024.8**: Import Celery, AI utils, prompts, and models
- [ ] **EXT-024.9**: Implement generate_article_from_opportunities(opportunity_ids, topic_id, persona) as @shared_task
- [ ] **EXT-024.10**: In generate_article_from_opportunities, fetch opportunities by IDs
- [ ] **EXT-024.11**: In generate_article_from_opportunities, fetch topic by ID
- [ ] **EXT-024.12**: In generate_article_from_opportunities, format opportunities into prompt context
- [ ] **EXT-024.13**: In generate_article_from_opportunities, get persona prompt from PERSONA_PROMPTS
- [ ] **EXT-024.14**: In generate_article_from_opportunities, format ARTICLE_GENERATION_PROMPT
- [ ] **EXT-024.15**: In generate_article_from_opportunities, call LLM API (OpenAI or Anthropic)
- [ ] **EXT-024.16**: In generate_article_from_opportunities, create Article instance with status='draft'
- [ ] **EXT-024.17**: In generate_article_from_opportunities, set ai_generated=True
- [ ] **EXT-024.18**: In generate_article_from_opportunities, add source_opportunities relationship
- [ ] **EXT-024.19**: In generate_article_from_opportunities, add topic relationship
- [ ] **EXT-024.20**: In generate_article_from_opportunities, save generation_metadata (prompt, model, tokens)
- [ ] **EXT-024.21**: In generate_article_from_opportunities, mark opportunities as used
- [ ] **EXT-024.22**: In generate_article_from_opportunities, return article ID
- [ ] **EXT-024.23**: Implement generate_title_from_content(content) function (complete implementation from ticket)
- [ ] **EXT-024.24**: Implement generate_meta_description(content, title) function (complete implementation from ticket)
- [ ] **EXT-024.25**: Implement enhance_article_content(article_id, enhancement_type) as @shared_task
- [ ] **EXT-024.26**: In enhance_article_content, fetch article by ID
- [ ] **EXT-024.27**: In enhance_article_content, format CONTENT_ENHANCEMENT_PROMPT
- [ ] **EXT-024.28**: In enhance_article_content, call LLM API
- [ ] **EXT-024.29**: In enhance_article_content, update article body with enhanced content
- [ ] **EXT-024.30**: In enhance_article_content, create revision
- [ ] **EXT-024.31**: In enhance_article_content, save and return article ID
- [ ] **EXT-024.32**: Implement moderate_article_content(article_id) as @shared_task
- [ ] **EXT-024.33**: In moderate_article_content, fetch article by ID
- [ ] **EXT-024.34**: In moderate_article_content, format MODERATION_PROMPT
- [ ] **EXT-024.35**: In moderate_article_content, call LLM API
- [ ] **EXT-024.36**: In moderate_article_content, parse moderation response (quality score, issues)
- [ ] **EXT-024.37**: In moderate_article_content, update article metadata with moderation results
- [ ] **EXT-024.38**: In moderate_article_content, return moderation results
- [ ] **EXT-024.39**: Run tests: `pytest apps/content/tests/test_generation_tasks.py -v`
- [ ] **EXT-024.40**: Fix any failing tests
- [ ] **EXT-024.41**: Test generate_article_from_opportunities manually in Django shell
- [ ] **EXT-024.42**: Verify article created with correct fields
- [ ] **EXT-024.43**: Test generate_title_from_content with sample content
- [ ] **EXT-024.44**: Test generate_meta_description with sample content
- [ ] **EXT-024.45**: Test enhance_article_content with existing article
- [ ] **EXT-024.46**: Test moderate_article_content with existing article
- [ ] **EXT-024.47**: Verify all tasks can be queued with Celery: `task.delay()`
- [ ] **EXT-024.48**: Git add and commit: `git add apps/content/tasks.py apps/content/tests && git commit -m "Add article generation tasks"`
- [ ] **EXT-024.49**: Git push: `git push origin master`

---

### EXT-025: Content Generation Admin Actions

- [ ] **EXT-025.1**: Update `apps/content/admin.py` to import generation tasks
- [ ] **EXT-025.2**: Implement generate_article_from_selected admin action for ScrapedOpportunityAdmin
- [ ] **EXT-025.3**: In generate_article_from_selected, get selected opportunity IDs
- [ ] **EXT-025.4**: In generate_article_from_selected, show form to select topic and persona
- [ ] **EXT-025.5**: In generate_article_from_selected, queue generate_article_from_opportunities task
- [ ] **EXT-025.6**: In generate_article_from_selected, show success message with task ID
- [ ] **EXT-025.7**: Add generate_article_from_selected to ScrapedOpportunityAdmin.actions
- [ ] **EXT-025.8**: Implement enhance_selected_articles admin action for ArticleAdmin
- [ ] **EXT-025.9**: In enhance_selected_articles, get selected article IDs
- [ ] **EXT-025.10**: In enhance_selected_articles, show form to select enhancement type
- [ ] **EXT-025.11**: In enhance_selected_articles, queue enhance_article_content task for each
- [ ] **EXT-025.12**: In enhance_selected_articles, show success message
- [ ] **EXT-025.13**: Add enhance_selected_articles to ArticleAdmin.actions
- [ ] **EXT-025.14**: Implement moderate_selected_articles admin action for ArticleAdmin
- [ ] **EXT-025.15**: In moderate_selected_articles, get selected article IDs
- [ ] **EXT-025.16**: In moderate_selected_articles, queue moderate_article_content task for each
- [ ] **EXT-025.17**: In moderate_selected_articles, show success message
- [ ] **EXT-025.18**: Add moderate_selected_articles to ArticleAdmin.actions
- [ ] **EXT-025.19**: Update generate_draft action (from EXT-018) to use generate_article_from_opportunities
- [ ] **EXT-025.20**: Run Django server: `python manage.py runserver`
- [ ] **EXT-025.21**: Access admin: http://localhost:8000/admin/scraping/scrapedopportunity/
- [ ] **EXT-025.22**: Select 3-5 opportunities and test "Generate article from selected" action
- [ ] **EXT-025.23**: Verify task queued (check Celery worker logs)
- [ ] **EXT-025.24**: Wait for task completion and verify article created
- [ ] **EXT-025.25**: Access admin: http://localhost:8000/admin/content/article/
- [ ] **EXT-025.26**: Select article and test "Enhance selected articles" action
- [ ] **EXT-025.27**: Verify enhancement task queued
- [ ] **EXT-025.28**: Select article and test "Moderate selected articles" action
- [ ] **EXT-025.29**: Verify moderation task queued
- [ ] **EXT-025.30**: Check article metadata for moderation results
- [ ] **EXT-025.31**: Git add and commit: `git add apps/content/admin.py && git commit -m "Add content generation admin actions"`
- [ ] **EXT-025.32**: Git push: `git push origin master`

---

### EXT-026: Review Queue Dashboard

- [ ] **EXT-026.1**: Create `apps/content/views.py` addition for ReviewQueueView
- [ ] **EXT-026.2**: Import PermissionRequiredMixin and ListView
- [ ] **EXT-026.3**: Create ReviewQueueView class inheriting from PermissionRequiredMixin, ListView
- [ ] **EXT-026.4**: Set model = Article
- [ ] **EXT-026.5**: Set template_name = 'content/review_queue.html'
- [ ] **EXT-026.6**: Set permission_required = 'content.change_article'
- [ ] **EXT-026.7**: Set paginate_by = 20
- [ ] **EXT-026.8**: Implement get_queryset() method
- [ ] **EXT-026.9**: In get_queryset, filter articles with status='review'
- [ ] **EXT-026.10**: In get_queryset, add select_related('prompt_ref')
- [ ] **EXT-026.11**: In get_queryset, add prefetch_related('topics', 'source_opportunities')
- [ ] **EXT-026.12**: In get_queryset, apply topic filter from request.GET
- [ ] **EXT-026.13**: In get_queryset, apply LLM filter from request.GET
- [ ] **EXT-026.14**: In get_queryset, apply sorting from request.GET (default: '-created_at')
- [ ] **EXT-026.15**: Implement get_context_data() method
- [ ] **EXT-026.16**: In get_context_data, add pending_count (articles with status='review')
- [ ] **EXT-026.17**: In get_context_data, add topics list
- [ ] **EXT-026.18**: Update `apps/content/urls.py` to add review queue URL
- [ ] **EXT-026.19**: Add URL pattern: path('review-queue/', ReviewQueueView.as_view(), name='review_queue')
- [ ] **EXT-026.20**: Create `apps/content/templates/content/review_queue.html`
- [ ] **EXT-026.21**: Extend base.html in review_queue.html
- [ ] **EXT-026.22**: Add page title and header
- [ ] **EXT-026.23**: Add statistics panel (pending count, avg review time)
- [ ] **EXT-026.24**: Add filter form (topic dropdown, LLM dropdown, date range)
- [ ] **EXT-026.25**: Add sort options (date, quality score)
- [ ] **EXT-026.26**: Add article cards with preview (title, excerpt, metadata)
- [ ] **EXT-026.27**: Add quick action buttons (Approve, Edit, Reject) for each article
- [ ] **EXT-026.28**: Add pagination controls
- [ ] **EXT-026.29**: Style with Bootstrap 5 classes
- [ ] **EXT-026.30**: Update `apps/core/templates/core/base.html` navigation
- [ ] **EXT-026.31**: Add "Review Queue" link to navigation (only visible to editors)
- [ ] **EXT-026.32**: Run Django server: `python manage.py runserver`
- [ ] **EXT-026.33**: Access review queue as editor: http://localhost:8000/review-queue/
- [ ] **EXT-026.34**: Verify page displays articles with status='review'
- [ ] **EXT-026.35**: Test topic filter (select topic and verify filtering)
- [ ] **EXT-026.36**: Test LLM filter (select LLM and verify filtering)
- [ ] **EXT-026.37**: Test sorting (by date, by quality score)
- [ ] **EXT-026.38**: Test quick actions (Approve, Edit, Reject buttons work)
- [ ] **EXT-026.39**: Test pagination (create 25+ review articles)
- [ ] **EXT-026.40**: Verify statistics display correctly
- [ ] **EXT-026.41**: Test permissions (non-editors cannot access)
- [ ] **EXT-026.42**: Test responsive design (320px, 768px, 1024px+)
- [ ] **EXT-026.43**: Git add and commit: `git add apps/content && git commit -m "Add review queue dashboard"`
- [ ] **EXT-026.44**: Git push: `git push origin master`

---

### EXT-027: Testing Infrastructure Setup

- [ ] **EXT-027.1**: Install testing dependencies: `pip install pytest==7.4.3 pytest-django==4.7.0 pytest-cov factory-boy==3.3.0`
- [ ] **EXT-027.2**: Update requirements.txt with testing dependencies
- [ ] **EXT-027.3**: Create `pytest.ini` file in project root
- [ ] **EXT-027.4**: Configure pytest.ini with DJANGO_SETTINGS_MODULE = extradime.settings.test
- [ ] **EXT-027.5**: Add python_files = tests.py test_*.py *_tests.py to pytest.ini
- [ ] **EXT-027.6**: Add addopts = --cov=apps --cov-report=html --cov-report=term-missing to pytest.ini
- [ ] **EXT-027.7**: Update `extradime/settings/test.py` for testing
- [ ] **EXT-027.8**: In test.py, use in-memory SQLite database
- [ ] **EXT-027.9**: In test.py, set DEBUG = False
- [ ] **EXT-027.10**: In test.py, use fast password hasher (PASSWORD_HASHERS with MD5PasswordHasher)
- [ ] **EXT-027.11**: In test.py, set CELERY_TASK_ALWAYS_EAGER = True
- [ ] **EXT-027.12**: In test.py, disable migrations (use --reuse-db flag)
- [ ] **EXT-027.13**: Create `conftest.py` in project root
- [ ] **EXT-027.14**: In conftest.py, add pytest fixtures for common test data
- [ ] **EXT-027.15**: Create `apps/scraping/tests/factories.py`
- [ ] **EXT-027.16**: Import factory and factory.django
- [ ] **EXT-027.17**: Create DataSourceFactory with Faker for name, url
- [ ] **EXT-027.18**: Set DataSourceFactory defaults (source_type='rss', is_active=True)
- [ ] **EXT-027.19**: Create ScrapedOpportunityFactory with Faker for title, description, url
- [ ] **EXT-027.20**: Set ScrapedOpportunityFactory.source = SubFactory(DataSourceFactory)
- [ ] **EXT-027.21**: Create `apps/content/tests/factories.py`
- [ ] **EXT-027.22**: Create TopicFactory with Faker for name
- [ ] **EXT-027.23**: Create ArticleFactory with Faker for title, body
- [ ] **EXT-027.24**: Set ArticleFactory defaults (status='draft', ai_generated=False)
- [ ] **EXT-027.25**: Create PromptLogFactory with Faker for prompt_text, response_text
- [ ] **EXT-027.26**: Create `apps/core/tests/test_base.py` with base test classes
- [ ] **EXT-027.27**: Create BaseTestCase class with common setup/teardown
- [ ] **EXT-027.28**: Run all tests: `pytest`
- [ ] **EXT-027.29**: Verify tests run successfully
- [ ] **EXT-027.30**: Generate coverage report: `pytest --cov=apps --cov-report=html`
- [ ] **EXT-027.31**: Open coverage report: `open htmlcov/index.html`
- [ ] **EXT-027.32**: Verify coverage > 80% (or note current coverage)
- [ ] **EXT-027.33**: Git add and commit: `git add pytest.ini conftest.py apps/*/tests/factories.py && git commit -m "Add testing infrastructure"`
- [ ] **EXT-027.34**: Git push: `git push origin master`

---

### EXT-028: Phase 1 Integration Testing

- [ ] **EXT-028.1**: Create `apps/scraping/tests/test_integration.py`
- [ ] **EXT-028.2**: Import pytest, patch, factories, models
- [ ] **EXT-028.3**: Write test_scraping_workflow() function
- [ ] **EXT-028.4**: In test_scraping_workflow, create DataSource with factory
- [ ] **EXT-028.5**: In test_scraping_workflow, mock run_spider task
- [ ] **EXT-028.6**: In test_scraping_workflow, call run_spider_task
- [ ] **EXT-028.7**: In test_scraping_workflow, verify opportunities created
- [ ] **EXT-028.8**: In test_scraping_workflow, verify DataSource.last_checked updated
- [ ] **EXT-028.9**: In test_scraping_workflow, verify DataSource.total_opportunities_found updated
- [ ] **EXT-028.10**: Write test_rss_spider_integration() function
- [ ] **EXT-028.11**: In test_rss_spider_integration, create test RSS feed fixture
- [ ] **EXT-028.12**: In test_rss_spider_integration, run RSS spider with fixture
- [ ] **EXT-028.13**: In test_rss_spider_integration, verify opportunities scraped
- [ ] **EXT-028.14**: Create `apps/content/tests/test_integration.py`
- [ ] **EXT-028.15**: Write test_content_generation_workflow() function
- [ ] **EXT-028.16**: In test_content_generation_workflow, create opportunity with factory
- [ ] **EXT-028.17**: In test_content_generation_workflow, mock call_openai_api
- [ ] **EXT-028.18**: In test_content_generation_workflow, call generate_article_from_opportunities
- [ ] **EXT-028.19**: In test_content_generation_workflow, verify article created
- [ ] **EXT-028.20**: In test_content_generation_workflow, verify article.status == 'review'
- [ ] **EXT-028.21**: In test_content_generation_workflow, verify article.ai_generated == True
- [ ] **EXT-028.22**: In test_content_generation_workflow, verify source_opportunities relationship
- [ ] **EXT-028.23**: In test_content_generation_workflow, verify PromptLog created
- [ ] **EXT-028.24**: In test_content_generation_workflow, verify opportunity.status == 'USED_IN_CONTENT'
- [ ] **EXT-028.25**: Create `tests/test_e2e.py` in project root
- [ ] **EXT-028.26**: Write test_end_to_end_article_creation() function
- [ ] **EXT-028.27**: Mark with @pytest.mark.integration decorator
- [ ] **EXT-028.28**: In test_e2e, create DataSource and scrape opportunities (mocked)
- [ ] **EXT-028.29**: In test_e2e, generate article from opportunity (mocked LLM)
- [ ] **EXT-028.30**: In test_e2e, verify article in review status
- [ ] **EXT-028.31**: In test_e2e, publish article (set status='published', publish_date=now)
- [ ] **EXT-028.32**: In test_e2e, verify article accessible on frontend (GET /articles/{slug}/)
- [ ] **EXT-028.33**: In test_e2e, verify article in RSS feed (GET /feeds/articles/)
- [ ] **EXT-028.34**: Write test_admin_interface_integration() function
- [ ] **EXT-028.35**: In test_admin_interface, test DataSource admin CRUD operations
- [ ] **EXT-028.36**: In test_admin_interface, test Article admin CRUD operations
- [ ] **EXT-028.37**: In test_admin_interface, test admin actions (publish, generate, etc.)
- [ ] **EXT-028.38**: Run integration tests: `pytest -m integration -v`
- [ ] **EXT-028.39**: Fix any failing integration tests
- [ ] **EXT-028.40**: Run all tests: `pytest -v`
- [ ] **EXT-028.41**: Verify all tests passing
- [ ] **EXT-028.42**: Check test coverage: `pytest --cov=apps --cov-report=term-missing`
- [ ] **EXT-028.43**: Verify coverage > 80%
- [ ] **EXT-028.44**: Git add and commit: `git add apps/*/tests/test_integration.py tests/test_e2e.py && git commit -m "Add Phase 1 integration tests"`
- [ ] **EXT-028.45**: Git push: `git push origin master`

---

### EXT-029: Documentation and README

- [ ] **EXT-029.1**: Update `README.md` with project overview
- [ ] **EXT-029.2**: Add project description to README
- [ ] **EXT-029.3**: Add features list to README (scraping, AI generation, content management)
- [ ] **EXT-029.4**: Add tech stack to README (Django, PostgreSQL, Celery, Scrapy, OpenAI, etc.)
- [ ] **EXT-029.5**: Add quick start section to README
- [ ] **EXT-029.6**: Add links to detailed documentation
- [ ] **EXT-029.7**: Add license information to README
- [ ] **EXT-029.8**: Add contact/support information to README
- [ ] **EXT-029.9**: Create `docs/SETUP.md` file
- [ ] **EXT-029.10**: Add prerequisites section to SETUP.md (Python 3.11+, PostgreSQL, Redis)
- [ ] **EXT-029.11**: Add installation steps to SETUP.md (clone, venv, pip install)
- [ ] **EXT-029.12**: Add database setup steps to SETUP.md (createdb, createuser, migrate)
- [ ] **EXT-029.13**: Add environment configuration to SETUP.md (copy .env.example, fill values)
- [ ] **EXT-029.14**: Add running the application to SETUP.md (runserver, celery worker, celery beat)
- [ ] **EXT-029.15**: Add running tests to SETUP.md (pytest commands)
- [ ] **EXT-029.16**: Create `docs/DEVELOPER_GUIDE.md` file
- [ ] **EXT-029.17**: Add project structure section to DEVELOPER_GUIDE.md
- [ ] **EXT-029.18**: Add code style guidelines to DEVELOPER_GUIDE.md (PEP 8, Black, flake8)
- [ ] **EXT-029.19**: Add testing guidelines to DEVELOPER_GUIDE.md (TDD, coverage requirements)
- [ ] **EXT-029.20**: Add Git workflow to DEVELOPER_GUIDE.md (branching, commits, PRs)
- [ ] **EXT-029.21**: Add how to add new features to DEVELOPER_GUIDE.md
- [ ] **EXT-029.22**: Document all environment variables in DEVELOPER_GUIDE.md
- [ ] **EXT-029.23**: Create `docs/ADMIN_GUIDE.md` file
- [ ] **EXT-029.24**: Document DataSource admin in ADMIN_GUIDE.md (how to add sources, run spiders)
- [ ] **EXT-029.25**: Document Article admin in ADMIN_GUIDE.md (how to review, publish, generate)
- [ ] **EXT-029.26**: Document admin actions in ADMIN_GUIDE.md (all custom actions)
- [ ] **EXT-029.27**: Document review queue workflow in ADMIN_GUIDE.md
- [ ] **EXT-029.28**: Create `docs/TROUBLESHOOTING.md` file
- [ ] **EXT-029.29**: Add common issues to TROUBLESHOOTING.md (database connection, Celery, Redis)
- [ ] **EXT-029.30**: Add solutions to TROUBLESHOOTING.md
- [ ] **EXT-029.31**: Add debugging tips to TROUBLESHOOTING.md
- [ ] **EXT-029.32**: Create `CONTRIBUTING.md` file
- [ ] **EXT-029.33**: Add how to contribute to CONTRIBUTING.md
- [ ] **EXT-029.34**: Add code of conduct to CONTRIBUTING.md
- [ ] **EXT-029.35**: Add pull request process to CONTRIBUTING.md
- [ ] **EXT-029.36**: Test setup guide on fresh machine (or VM)
- [ ] **EXT-029.37**: Verify all commands work as documented
- [ ] **EXT-029.38**: Check all links in documentation
- [ ] **EXT-029.39**: Proofread all documentation
- [ ] **EXT-029.40**: Add screenshots to documentation (optional but helpful)
- [ ] **EXT-029.41**: Git add and commit: `git add README.md docs/ CONTRIBUTING.md && git commit -m "Add comprehensive documentation"`
- [ ] **EXT-029.42**: Git push: `git push origin master`

---

# Phase 2: User & Community Features (Weeks 9-16)

## Epic 2.1: User Management (Week 9-10)

### EXT-030: User Models and Authentication

- [ ] **EXT-030.1**: Create `apps/users/__init__.py` directory
- [ ] **EXT-030.2**: Create test file: `apps/users/tests/test_models.py`
- [ ] **EXT-030.3**: Write unit test for CustomUser model creation
- [ ] **EXT-030.4**: Write unit test for UserProfile model creation
- [ ] **EXT-030.5**: Write unit test for user registration
- [ ] **EXT-030.6**: Write unit test for email verification
- [ ] **EXT-030.7**: Create `apps/users/models.py`
- [ ] **EXT-030.8**: Import AbstractUser from django.contrib.auth.models
- [ ] **EXT-030.9**: Create CustomUser model extending AbstractUser
- [ ] **EXT-030.10**: Add email_verified field to CustomUser (BooleanField, default=False)
- [ ] **EXT-030.11**: Add verification_token field to CustomUser (CharField, max_length=100, blank=True)
- [ ] **EXT-030.12**: Implement CustomUser.__str__() method
- [ ] **EXT-030.13**: Create UserProfile model with OneToOneField to CustomUser
- [ ] **EXT-030.14**: Add bio field to UserProfile (TextField, blank=True)
- [ ] **EXT-030.15**: Add avatar field to UserProfile (ImageField, upload_to='avatars/', blank=True)
- [ ] **EXT-030.16**: Add location field to UserProfile (CharField, max_length=100, blank=True)
- [ ] **EXT-030.17**: Add website field to UserProfile (URLField, blank=True)
- [ ] **EXT-030.18**: Add social_links field to UserProfile (JSONField, default=dict)
- [ ] **EXT-030.19**: Add email_preferences field to UserProfile (JSONField, default=dict)
- [ ] **EXT-030.20**: Implement UserProfile.__str__() method
- [ ] **EXT-030.21**: Update `extradime/settings/base.py` to set AUTH_USER_MODEL = 'users.CustomUser'
- [ ] **EXT-030.22**: Create migrations: `python manage.py makemigrations users`
- [ ] **EXT-030.23**: Apply migrations: `python manage.py migrate`
- [ ] **EXT-030.24**: Create `apps/users/forms.py`
- [ ] **EXT-030.25**: Create RegistrationForm with email, password1, password2 fields
- [ ] **EXT-030.26**: Add email validation to RegistrationForm
- [ ] **EXT-030.27**: Create LoginForm with email and password fields
- [ ] **EXT-030.28**: Create PasswordResetForm
- [ ] **EXT-030.29**: Create `apps/users/views.py`
- [ ] **EXT-030.30**: Implement RegisterView (CreateView)
- [ ] **EXT-030.31**: In RegisterView, generate verification token
- [ ] **EXT-030.32**: In RegisterView, send verification email
- [ ] **EXT-030.33**: Implement VerifyEmailView to handle token verification
- [ ] **EXT-030.34**: Implement LoginView using Django's LoginView
- [ ] **EXT-030.35**: Implement LogoutView using Django's LogoutView
- [ ] **EXT-030.36**: Implement PasswordResetView
- [ ] **EXT-030.37**: Create `apps/users/urls.py`
- [ ] **EXT-030.38**: Add URL patterns for register, login, logout, verify-email, password-reset
- [ ] **EXT-030.39**: Update `extradime/urls.py` to include users URLs
- [ ] **EXT-030.40**: Create templates: `apps/users/templates/users/register.html`
- [ ] **EXT-030.41**: Create templates: `apps/users/templates/users/login.html`
- [ ] **EXT-030.42**: Create templates: `apps/users/templates/users/verify_email.html`
- [ ] **EXT-030.43**: Create templates: `apps/users/templates/users/password_reset.html`
- [ ] **EXT-030.44**: Create `apps/users/admin.py`
- [ ] **EXT-030.45**: Register CustomUser with admin
- [ ] **EXT-030.46**: Register UserProfile with admin
- [ ] **EXT-030.47**: Configure UserAdmin with list_display, search_fields
- [ ] **EXT-030.48**: Run tests: `pytest apps/users/tests/test_models.py -v`
- [ ] **EXT-030.49**: Fix any failing tests
- [ ] **EXT-030.50**: Test registration flow in browser
- [ ] **EXT-030.51**: Test email verification (check console for email)
- [ ] **EXT-030.52**: Test login/logout functionality
- [ ] **EXT-030.53**: Test password reset flow
- [ ] **EXT-030.54**: Verify user permissions work correctly
- [ ] **EXT-030.55**: Git add and commit: `git add apps/users && git commit -m "Add user authentication system"`
- [ ] **EXT-030.56**: Git push: `git push origin master`

---

### EXT-031: User Profile Pages

- [ ] **EXT-031.1**: Create test file: `apps/users/tests/test_views.py`
- [ ] **EXT-031.2**: Write unit test for ProfileView (GET request)
- [ ] **EXT-031.3**: Write unit test for ProfileEditView (GET and POST)
- [ ] **EXT-031.4**: Write unit test for avatar upload
- [ ] **EXT-031.5**: Write unit test for privacy settings
- [ ] **EXT-031.6**: Update `apps/users/views.py`
- [ ] **EXT-031.7**: Implement ProfileView (DetailView)
- [ ] **EXT-031.8**: In ProfileView.get_context_data, add user's articles
- [ ] **EXT-031.9**: In ProfileView.get_context_data, add user statistics (join date, posts count)
- [ ] **EXT-031.10**: In ProfileView.get_context_data, add activity history
- [ ] **EXT-031.11**: Implement ProfileEditView (UpdateView)
- [ ] **EXT-031.12**: Add LoginRequiredMixin to ProfileEditView
- [ ] **EXT-031.13**: In ProfileEditView, restrict to profile owner only
- [ ] **EXT-031.14**: Create ProfileEditForm with bio, location, website, social_links fields
- [ ] **EXT-031.15**: Add avatar upload handling with Pillow (resize to 200x200)
- [ ] **EXT-031.16**: Add privacy_settings field to UserProfile model
- [ ] **EXT-031.17**: Create migration for privacy_settings field
- [ ] **EXT-031.18**: Apply migration: `python manage.py migrate`
- [ ] **EXT-031.19**: Update `apps/users/urls.py`
- [ ] **EXT-031.20**: Add URL pattern: path('profile/<int:pk>/', ProfileView, name='profile')
- [ ] **EXT-031.21**: Add URL pattern: path('profile/edit/', ProfileEditView, name='profile_edit')
- [ ] **EXT-031.22**: Create `apps/users/templates/users/profile.html`
- [ ] **EXT-031.23**: Display user avatar, bio, location, website in profile.html
- [ ] **EXT-031.24**: Display user statistics (join date, articles count) in profile.html
- [ ] **EXT-031.25**: Display recent activity (recent articles, comments) in profile.html
- [ ] **EXT-031.26**: Add "Edit Profile" button (only visible to profile owner)
- [ ] **EXT-031.27**: Create `apps/users/templates/users/profile_edit.html`
- [ ] **EXT-031.28**: Add form fields for bio, location, website, social_links
- [ ] **EXT-031.29**: Add avatar upload field with preview
- [ ] **EXT-031.30**: Add privacy settings checkboxes
- [ ] **EXT-031.31**: Style with Bootstrap 5 classes
- [ ] **EXT-031.32**: Install Pillow: `pip install Pillow==10.1.0`
- [ ] **EXT-031.33**: Update requirements.txt
- [ ] **EXT-031.34**: Run tests: `pytest apps/users/tests/test_views.py -v`
- [ ] **EXT-031.35**: Fix any failing tests
- [ ] **EXT-031.36**: Test profile view in browser
- [ ] **EXT-031.37**: Test profile edit functionality
- [ ] **EXT-031.38**: Test avatar upload (upload image and verify resize)
- [ ] **EXT-031.39**: Test privacy settings (public/private profile)
- [ ] **EXT-031.40**: Test responsive design (mobile, tablet, desktop)
- [ ] **EXT-031.41**: Git add and commit: `git add apps/users requirements.txt && git commit -m "Add user profile pages"`
- [ ] **EXT-031.42**: Git push: `git push origin master`

---

## Epic 2.2: Forum Integration (Week 11-12)

### EXT-032: Forum Package Evaluation and Installation

- [ ] **EXT-032.1**: Research django-machina package (read documentation)
- [ ] **EXT-032.2**: Research alternative: custom forum build (pros/cons)
- [ ] **EXT-032.3**: Evaluate features: categories, topics, posts, permissions, search
- [ ] **EXT-032.4**: Evaluate maintenance: last update, community support, issues
- [ ] **EXT-032.5**: Evaluate customization: template override, model extension
- [ ] **EXT-032.6**: Evaluate performance: query optimization, caching
- [ ] **EXT-032.7**: Make decision: django-machina vs custom (document reasoning)
- [ ] **EXT-032.8**: Install django-machina: `pip install django-machina==1.3.0`
- [ ] **EXT-032.9**: Update requirements.txt
- [ ] **EXT-032.10**: Add machina apps to INSTALLED_APPS in settings/base.py
- [ ] **EXT-032.11**: Add machina middleware to MIDDLEWARE in settings/base.py
- [ ] **EXT-032.12**: Update `extradime/urls.py` to include machina URLs
- [ ] **EXT-032.13**: Run machina migrations: `python manage.py migrate`
- [ ] **EXT-032.14**: Create initial forum structure using admin or management command
- [ ] **EXT-032.15**: Create category: "General Discussion"
- [ ] **EXT-032.16**: Create forum: "Getting Started" under General Discussion
- [ ] **EXT-032.17**: Create forum: "Success Stories" under General Discussion
- [ ] **EXT-032.18**: Create category: "Side Hustles"
- [ ] **EXT-032.19**: Create forum: "Freelancing" under Side Hustles
- [ ] **EXT-032.20**: Create forum: "Online Business" under Side Hustles
- [ ] **EXT-032.21**: Configure forum permissions (who can view, post, moderate)
- [ ] **EXT-032.22**: Integrate with CustomUser model
- [ ] **EXT-032.23**: Customize machina templates (copy to project templates directory)
- [ ] **EXT-032.24**: Update base template to match site design
- [ ] **EXT-032.25**: Test forum creation in admin
- [ ] **EXT-032.26**: Test topic creation (create test topic)
- [ ] **EXT-032.27**: Test posting (create test post and reply)
- [ ] **EXT-032.28**: Test permissions (verify non-logged-in users can't post)
- [ ] **EXT-032.29**: Test forum navigation and breadcrumbs
- [ ] **EXT-032.30**: Git add and commit: `git add . && git commit -m "Add forum integration with django-machina"`
- [ ] **EXT-032.31**: Git push: `git push origin master`

---

### EXT-033: AI Avatar Models and Personas

- [ ] **EXT-033.1**: Create `apps/community/__init__.py` directory
- [ ] **EXT-033.2**: Create test file: `apps/community/tests/test_models.py`
- [ ] **EXT-033.3**: Write unit test for AIAvatarProfile model creation
- [ ] **EXT-033.4**: Write unit test for persona prompt formatting
- [ ] **EXT-033.5**: Write unit test for AI response generation
- [ ] **EXT-033.6**: Create `apps/community/models.py`
- [ ] **EXT-033.7**: Import User model and required modules
- [ ] **EXT-033.8**: Create AIAvatarProfile model with OneToOneField to User
- [ ] **EXT-033.9**: Add name field to AIAvatarProfile (CharField, max_length=100)
- [ ] **EXT-033.10**: Add bio field to AIAvatarProfile (TextField)
- [ ] **EXT-033.11**: Add avatar_image field to AIAvatarProfile (ImageField)
- [ ] **EXT-033.12**: Add persona_prompt field to AIAvatarProfile (TextField)
- [ ] **EXT-033.13**: Add expertise_areas field to AIAvatarProfile (JSONField, default=list)
- [ ] **EXT-033.14**: Add personality_traits field to AIAvatarProfile (JSONField, default=list)
- [ ] **EXT-033.15**: Add is_active field to AIAvatarProfile (BooleanField, default=True)
- [ ] **EXT-033.16**: Add response_frequency field to AIAvatarProfile (CharField with choices)
- [ ] **EXT-033.17**: Implement AIAvatarProfile.__str__() method
- [ ] **EXT-033.18**: Add AIAvatarProfile to INSTALLED_APPS
- [ ] **EXT-033.19**: Create migrations: `python manage.py makemigrations community`
- [ ] **EXT-033.20**: Apply migrations: `python manage.py migrate`
- [ ] **EXT-033.21**: Create `apps/community/avatar_prompts.py`
- [ ] **EXT-033.22**: Define PERSONA_PROMPTS dictionary
- [ ] **EXT-033.23**: Add "Freelance Expert" persona prompt (professional, experienced)
- [ ] **EXT-033.24**: Add "Side Hustle Enthusiast" persona prompt (energetic, motivational)
- [ ] **EXT-033.25**: Add "Passive Income Strategist" persona prompt (analytical, data-driven)
- [ ] **EXT-033.26**: Create `apps/community/tasks.py`
- [ ] **EXT-033.27**: Import Celery shared_task decorator
- [ ] **EXT-033.28**: Implement generate_ai_avatar_response(avatar_id, post_id) task
- [ ] **EXT-033.29**: In generate_ai_avatar_response, fetch AIAvatarProfile by ID
- [ ] **EXT-033.30**: In generate_ai_avatar_response, fetch forum post by ID
- [ ] **EXT-033.31**: In generate_ai_avatar_response, format prompt with persona and post content
- [ ] **EXT-033.32**: In generate_ai_avatar_response, call LLM API (reuse from apps/content/ai_utils.py)
- [ ] **EXT-033.33**: In generate_ai_avatar_response, create forum reply with AI-generated content
- [ ] **EXT-033.34**: In generate_ai_avatar_response, mark reply as AI-generated
- [ ] **EXT-033.35**: Create `apps/community/admin.py`
- [ ] **EXT-033.36**: Register AIAvatarProfile with admin
- [ ] **EXT-033.37**: Configure AIAvatarProfileAdmin with list_display, list_filter
- [ ] **EXT-033.38**: Create management command: `apps/community/management/commands/create_ai_avatars.py`
- [ ] **EXT-033.39**: In create_ai_avatars command, create User for each persona
- [ ] **EXT-033.40**: In create_ai_avatars command, create AIAvatarProfile for each persona
- [ ] **EXT-033.41**: Run command: `python manage.py create_ai_avatars`
- [ ] **EXT-033.42**: Verify AI avatars created in admin
- [ ] **EXT-033.43**: Run tests: `pytest apps/community/tests/test_models.py -v`
- [ ] **EXT-033.44**: Fix any failing tests
- [ ] **EXT-033.45**: Test AI avatar response generation manually
- [ ] **EXT-033.46**: Create test forum post and trigger AI response
- [ ] **EXT-033.47**: Verify AI response stays in character
- [ ] **EXT-033.48**: Verify AI posts are clearly marked with badge/indicator
- [ ] **EXT-033.49**: Git add and commit: `git add apps/community && git commit -m "Add AI avatar personas"`
- [ ] **EXT-033.50**: Git push: `git push origin master`

---

## Epic 2.3: Content Moderation (Week 13-14)

### EXT-034: Moderation Configuration and Models

- [ ] **EXT-034.1**: Update `apps/community/models.py`
- [ ] **EXT-034.2**: Create ModerationLog model
- [ ] **EXT-034.3**: Add content_type field to ModerationLog (ForeignKey to ContentType)
- [ ] **EXT-034.4**: Add object_id field to ModerationLog (PositiveIntegerField)
- [ ] **EXT-034.5**: Add content_object field to ModerationLog (GenericForeignKey)
- [ ] **EXT-034.6**: Add moderator field to ModerationLog (ForeignKey to User, null=True)
- [ ] **EXT-034.7**: Add action field to ModerationLog (CharField with choices: approve, reject, flag, ban)
- [ ] **EXT-034.8**: Add reason field to ModerationLog (TextField, blank=True)
- [ ] **EXT-034.9**: Add timestamp field to ModerationLog (DateTimeField, auto_now_add=True)
- [ ] **EXT-034.10**: Add scores field to ModerationLog (JSONField for Perspective API scores)
- [ ] **EXT-034.11**: Implement ModerationLog.__str__() method
- [ ] **EXT-034.12**: Create migrations: `python manage.py makemigrations community`
- [ ] **EXT-034.13**: Apply migrations: `python manage.py migrate`
- [ ] **EXT-034.14**: Create `apps/community/moderation_config.py`
- [ ] **EXT-034.15**: Define MODERATION_THRESHOLDS dictionary
- [ ] **EXT-034.16**: Set TOXICITY threshold: auto_flag=0.7, auto_reject=0.9
- [ ] **EXT-034.17**: Set SEVERE_TOXICITY threshold: auto_flag=0.6, auto_reject=0.8
- [ ] **EXT-034.18**: Set IDENTITY_ATTACK threshold: auto_flag=0.7, auto_reject=0.9
- [ ] **EXT-034.19**: Set INSULT threshold: auto_flag=0.7, auto_reject=0.9
- [ ] **EXT-034.20**: Set PROFANITY threshold: auto_flag=0.6, auto_reject=0.8
- [ ] **EXT-034.21**: Set THREAT threshold: auto_flag=0.7, auto_reject=0.9
- [ ] **EXT-034.22**: Create `apps/community/moderation.py`
- [ ] **EXT-034.23**: Implement approve_content(content_object, moderator) function
- [ ] **EXT-034.24**: Implement reject_content(content_object, moderator, reason) function
- [ ] **EXT-034.25**: Implement flag_content(content_object, reason, scores) function
- [ ] **EXT-034.26**: Implement ban_user(user, moderator, reason) function
- [ ] **EXT-034.27**: Each function should create ModerationLog entry
- [ ] **EXT-034.28**: Update `apps/community/admin.py`
- [ ] **EXT-034.29**: Register ModerationLog with admin
- [ ] **EXT-034.30**: Configure ModerationLogAdmin with list_display, list_filter, search_fields
- [ ] **EXT-034.31**: Test moderation functions in Django shell
- [ ] **EXT-034.32**: Create test content and flag it
- [ ] **EXT-034.33**: Verify ModerationLog created correctly
- [ ] **EXT-034.34**: Test approve/reject actions
- [ ] **EXT-034.35**: Git add and commit: `git add apps/community && git commit -m "Add moderation configuration and models"`
- [ ] **EXT-034.36**: Git push: `git push origin master`

---

### EXT-035: Perspective API Integration

- [ ] **EXT-035.1**: Sign up for Google Perspective API (get API key)
- [ ] **EXT-035.2**: Add PERSPECTIVE_API_KEY to .env.example
- [ ] **EXT-035.3**: Add PERSPECTIVE_API_KEY to .env file
- [ ] **EXT-035.4**: Install google-api-python-client: `pip install google-api-python-client==2.108.0`
- [ ] **EXT-035.5**: Update requirements.txt
- [ ] **EXT-035.6**: Create test file: `apps/community/tests/test_perspective.py`
- [ ] **EXT-035.7**: Write unit test for analyze_text() with mocked API
- [ ] **EXT-035.8**: Write unit test for should_flag() with various scores
- [ ] **EXT-035.9**: Write unit test for moderate_content() workflow
- [ ] **EXT-035.10**: Create `apps/community/perspective_api.py`
- [ ] **EXT-035.11**: Import googleapiclient.discovery
- [ ] **EXT-035.12**: Import settings for API key
- [ ] **EXT-035.13**: Implement analyze_text(text) function
- [ ] **EXT-035.14**: In analyze_text, build Perspective API client
- [ ] **EXT-035.15**: In analyze_text, create analyze_request with text and attributes
- [ ] **EXT-035.16**: In analyze_text, request scores for: TOXICITY, SEVERE_TOXICITY, IDENTITY_ATTACK, INSULT, PROFANITY, THREAT
- [ ] **EXT-035.17**: In analyze_text, call API and handle response
- [ ] **EXT-035.18**: In analyze_text, extract scores from response
- [ ] **EXT-035.19**: In analyze_text, return scores dictionary
- [ ] **EXT-035.20**: In analyze_text, add error handling for API errors
- [ ] **EXT-035.21**: In analyze_text, add rate limit handling (retry with backoff)
- [ ] **EXT-035.22**: Implement should_flag(scores, thresholds) function
- [ ] **EXT-035.23**: In should_flag, compare each score to threshold
- [ ] **EXT-035.24**: In should_flag, return True if any auto_flag threshold exceeded
- [ ] **EXT-035.25**: In should_flag, return 'reject' if any auto_reject threshold exceeded
- [ ] **EXT-035.26**: Implement moderate_content(content_object) function
- [ ] **EXT-035.27**: In moderate_content, extract text from content_object
- [ ] **EXT-035.28**: In moderate_content, call analyze_text()
- [ ] **EXT-035.29**: In moderate_content, call should_flag() with scores
- [ ] **EXT-035.30**: In moderate_content, if should reject, call reject_content()
- [ ] **EXT-035.31**: In moderate_content, if should flag, call flag_content()
- [ ] **EXT-035.32**: In moderate_content, return scores and action taken
- [ ] **EXT-035.33**: Add caching to avoid duplicate API calls (use Django cache)
- [ ] **EXT-035.34**: Run tests: `pytest apps/community/tests/test_perspective.py -v`
- [ ] **EXT-035.35**: Fix any failing tests
- [ ] **EXT-035.36**: Test with real API (optional, use test content)
- [ ] **EXT-035.37**: Test with appropriate content (should pass)
- [ ] **EXT-035.38**: Test with toxic content (should flag/reject)
- [ ] **EXT-035.39**: Verify error handling works (test with invalid API key)
- [ ] **EXT-035.40**: Verify rate limiting works
- [ ] **EXT-035.41**: Git add and commit: `git add apps/community requirements.txt .env.example && git commit -m "Add Perspective API integration"`
- [ ] **EXT-035.42**: Git push: `git push origin master`

---

### EXT-036: Automated Moderation Workflow

- [ ] **EXT-036.1**: Create `apps/community/signals.py`
- [ ] **EXT-036.2**: Import post_save signal and receiver decorator
- [ ] **EXT-036.3**: Import ForumPost model (from machina or custom)
- [ ] **EXT-036.4**: Create post_save receiver for ForumPost
- [ ] **EXT-036.5**: In receiver, check if instance is newly created
- [ ] **EXT-036.6**: In receiver, trigger moderate_content_task.delay(post_id, 'forumpost')
- [ ] **EXT-036.7**: Update `apps/community/tasks.py`
- [ ] **EXT-036.8**: Implement moderate_content_task(object_id, content_type_str) as @shared_task
- [ ] **EXT-036.9**: In moderate_content_task, get content object by ID and type
- [ ] **EXT-036.10**: In moderate_content_task, call moderate_content() from perspective_api.py
- [ ] **EXT-036.11**: In moderate_content_task, handle moderation result
- [ ] **EXT-036.12**: In moderate_content_task, create ModerationLog if flagged
- [ ] **EXT-036.13**: In moderate_content_task, send notification to moderators if flagged
- [ ] **EXT-036.14**: In moderate_content_task, return moderation result
- [ ] **EXT-036.15**: Update `apps/community/__init__.py` to import signals
- [ ] **EXT-036.16**: Add default_app_config to ensure signals are loaded
- [ ] **EXT-036.17**: Create `apps/community/views.py`
- [ ] **EXT-036.18**: Implement ModerationQueueView (ListView)
- [ ] **EXT-036.19**: Add PermissionRequiredMixin to ModerationQueueView (permission: 'community.moderate_content')
- [ ] **EXT-036.20**: In ModerationQueueView.get_queryset, filter ModerationLog for flagged content
- [ ] **EXT-036.21**: In ModerationQueueView.get_queryset, exclude already moderated items
- [ ] **EXT-036.22**: In ModerationQueueView.get_context_data, add statistics (pending count, etc.)
- [ ] **EXT-036.23**: Create `apps/community/urls.py`
- [ ] **EXT-036.24**: Add URL pattern for moderation queue
- [ ] **EXT-036.25**: Update `extradime/urls.py` to include community URLs
- [ ] **EXT-036.26**: Create `apps/community/templates/community/moderation_queue.html`
- [ ] **EXT-036.27**: Display list of flagged content with scores
- [ ] **EXT-036.28**: Add action buttons (Approve, Reject) for each item
- [ ] **EXT-036.29**: Display Perspective API scores for each item
- [ ] **EXT-036.30**: Add filtering by content type, score threshold
- [ ] **EXT-036.31**: Style with Bootstrap 5 classes
- [ ] **EXT-036.32**: Implement approve/reject actions in views
- [ ] **EXT-036.33**: Add CSRF protection to action forms
- [ ] **EXT-036.34**: Test signal triggers (create forum post and verify moderation task runs)
- [ ] **EXT-036.35**: Test moderation task with appropriate content
- [ ] **EXT-036.36**: Test moderation task with toxic content (should flag)
- [ ] **EXT-036.37**: Test auto-rejection (very toxic content)
- [ ] **EXT-036.38**: Test moderation queue view (access as moderator)
- [ ] **EXT-036.39**: Test approve action (approve flagged content)
- [ ] **EXT-036.40**: Test reject action (reject flagged content)
- [ ] **EXT-036.41**: Verify moderator notifications work
- [ ] **EXT-036.42**: Git add and commit: `git add apps/community && git commit -m "Add automated moderation workflow"`
- [ ] **EXT-036.43**: Git push: `git push origin master`

---

# Phase 3: Advanced Features (Weeks 17-24)

## Epic 3.1: Newsletter System (Week 17-18)

### EXT-037: Newsletter Models and Subscription

- [ ] **EXT-037.1**: Create `apps/newsletter/__init__.py` directory
- [ ] **EXT-037.2**: Create test file: `apps/newsletter/tests/test_models.py`
- [ ] **EXT-037.3**: Write unit test for Subscription model creation
- [ ] **EXT-037.4**: Write unit test for NewsletterIssue model creation
- [ ] **EXT-037.5**: Write unit test for subscription verification
- [ ] **EXT-037.6**: Write unit test for unsubscribe functionality
- [ ] **EXT-037.7**: Create `apps/newsletter/models.py`
- [ ] **EXT-037.8**: Import User model and required modules
- [ ] **EXT-037.9**: Create Subscription model
- [ ] **EXT-037.10**: Add email field to Subscription (EmailField, unique=True)
- [ ] **EXT-037.11**: Add user field to Subscription (ForeignKey to User, null=True, blank=True)
- [ ] **EXT-037.12**: Add is_active field to Subscription (BooleanField, default=False)
- [ ] **EXT-037.13**: Add subscribed_at field to Subscription (DateTimeField, auto_now_add=True)
- [ ] **EXT-037.14**: Add preferences field to Subscription (JSONField: topics, frequency)
- [ ] **EXT-037.15**: Add verification_token field to Subscription (CharField, max_length=100)
- [ ] **EXT-037.16**: Add verified_at field to Subscription (DateTimeField, null=True, blank=True)
- [ ] **EXT-037.17**: Add unsubscribe_token field to Subscription (CharField, max_length=100, unique=True)
- [ ] **EXT-037.18**: Implement Subscription.__str__() method
- [ ] **EXT-037.19**: Implement Subscription.generate_tokens() method
- [ ] **EXT-037.20**: Create NewsletterIssue model
- [ ] **EXT-037.21**: Add title field to NewsletterIssue (CharField, max_length=200)
- [ ] **EXT-037.22**: Add content field to NewsletterIssue (TextField)
- [ ] **EXT-037.23**: Add html_content field to NewsletterIssue (TextField)
- [ ] **EXT-037.24**: Add sent_at field to NewsletterIssue (DateTimeField, null=True, blank=True)
- [ ] **EXT-037.25**: Add recipient_count field to NewsletterIssue (IntegerField, default=0)
- [ ] **EXT-037.26**: Add featured_articles field to NewsletterIssue (ManyToManyField to Article)
- [ ] **EXT-037.27**: Add created_at field to NewsletterIssue (DateTimeField, auto_now_add=True)
- [ ] **EXT-037.28**: Implement NewsletterIssue.__str__() method
- [ ] **EXT-037.29**: Add newsletter to INSTALLED_APPS
- [ ] **EXT-037.30**: Create migrations: `python manage.py makemigrations newsletter`
- [ ] **EXT-037.31**: Apply migrations: `python manage.py migrate`
- [ ] **EXT-037.32**: Create `apps/newsletter/forms.py`
- [ ] **EXT-037.33**: Create SubscriptionForm with email field
- [ ] **EXT-037.34**: Add email validation to SubscriptionForm
- [ ] **EXT-037.35**: Create PreferenceForm with topics and frequency fields
- [ ] **EXT-037.36**: Create `apps/newsletter/views.py`
- [ ] **EXT-037.37**: Implement SubscribeView (CreateView)
- [ ] **EXT-037.38**: In SubscribeView, generate verification token
- [ ] **EXT-037.39**: In SubscribeView, send verification email
- [ ] **EXT-037.40**: Implement VerifySubscriptionView to handle token verification
- [ ] **EXT-037.41**: In VerifySubscriptionView, set is_active=True and verified_at=now
- [ ] **EXT-037.42**: Implement UnsubscribeView to handle unsubscribe token
- [ ] **EXT-037.43**: In UnsubscribeView, set is_active=False
- [ ] **EXT-037.44**: Implement PreferenceView (UpdateView) for managing preferences
- [ ] **EXT-037.45**: Create `apps/newsletter/urls.py`
- [ ] **EXT-037.46**: Add URL patterns for subscribe, verify, unsubscribe, preferences
- [ ] **EXT-037.47**: Update `extradime/urls.py` to include newsletter URLs
- [ ] **EXT-037.48**: Create templates: `apps/newsletter/templates/newsletter/subscribe.html`
- [ ] **EXT-037.49**: Create templates: `apps/newsletter/templates/newsletter/verify.html`
- [ ] **EXT-037.50**: Create templates: `apps/newsletter/templates/newsletter/unsubscribe.html`
- [ ] **EXT-037.51**: Create templates: `apps/newsletter/templates/newsletter/preferences.html`
- [ ] **EXT-037.52**: Create `apps/newsletter/admin.py`
- [ ] **EXT-037.53**: Register Subscription with admin
- [ ] **EXT-037.54**: Register NewsletterIssue with admin
- [ ] **EXT-037.55**: Configure SubscriptionAdmin with list_display, list_filter, search_fields
- [ ] **EXT-037.56**: Run tests: `pytest apps/newsletter/tests/test_models.py -v`
- [ ] **EXT-037.57**: Fix any failing tests
- [ ] **EXT-037.58**: Test subscription flow in browser
- [ ] **EXT-037.59**: Test email verification (check console for email)
- [ ] **EXT-037.60**: Test preference management
- [ ] **EXT-037.61**: Test unsubscribe functionality
- [ ] **EXT-037.62**: Verify double opt-in works correctly
- [ ] **EXT-037.63**: Git add and commit: `git add apps/newsletter && git commit -m "Add newsletter subscription system"`
- [ ] **EXT-037.64**: Git push: `git push origin master`

---

### EXT-038: Newsletter Content Curation

- [ ] **EXT-038.1**: Create test file: `apps/newsletter/tests/test_curation.py`
- [ ] **EXT-038.2**: Write unit test for select_featured_articles()
- [ ] **EXT-038.3**: Write unit test for identify_trending_topics()
- [ ] **EXT-038.4**: Write unit test for generate_newsletter_content() with mocked LLM
- [ ] **EXT-038.5**: Create `apps/newsletter/curation.py`
- [ ] **EXT-038.6**: Import Article, ScrapedOpportunity, Topic models
- [ ] **EXT-038.7**: Import datetime and timedelta
- [ ] **EXT-038.8**: Implement select_featured_articles(since_date, limit=5) function
- [ ] **EXT-038.9**: In select_featured_articles, query articles published since date
- [ ] **EXT-038.10**: In select_featured_articles, filter by status='published'
- [ ] **EXT-038.11**: In select_featured_articles, order by views (if tracking), created_at
- [ ] **EXT-038.12**: In select_featured_articles, return top N articles
- [ ] **EXT-038.13**: Implement identify_trending_topics(since_date) function
- [ ] **EXT-038.14**: In identify_trending_topics, query recent articles and opportunities
- [ ] **EXT-038.15**: In identify_trending_topics, count topic mentions
- [ ] **EXT-038.16**: In identify_trending_topics, return top trending topics
- [ ] **EXT-038.17**: Implement generate_newsletter_content(articles, opportunities, topics) function
- [ ] **EXT-038.18**: In generate_newsletter_content, format newsletter prompt
- [ ] **EXT-038.19**: In generate_newsletter_content, include article summaries
- [ ] **EXT-038.20**: In generate_newsletter_content, include trending topics
- [ ] **EXT-038.21**: In generate_newsletter_content, include recent opportunities
- [ ] **EXT-038.22**: In generate_newsletter_content, call LLM API (reuse from apps/content/ai_utils.py)
- [ ] **EXT-038.23**: In generate_newsletter_content, return formatted newsletter content
- [ ] **EXT-038.24**: Create `apps/newsletter/tasks.py`
- [ ] **EXT-038.25**: Import Celery shared_task decorator
- [ ] **EXT-038.26**: Implement curate_newsletter_content() as @shared_task
- [ ] **EXT-038.27**: In curate_newsletter_content, calculate since_date (last 7 days)
- [ ] **EXT-038.28**: In curate_newsletter_content, call select_featured_articles()
- [ ] **EXT-038.29**: In curate_newsletter_content, call identify_trending_topics()
- [ ] **EXT-038.30**: In curate_newsletter_content, call generate_newsletter_content()
- [ ] **EXT-038.31**: In curate_newsletter_content, return curated content
- [ ] **EXT-038.32**: Run tests: `pytest apps/newsletter/tests/test_curation.py -v`
- [ ] **EXT-038.33**: Fix any failing tests
- [ ] **EXT-038.34**: Test select_featured_articles with sample data
- [ ] **EXT-038.35**: Test identify_trending_topics with sample data
- [ ] **EXT-038.36**: Test generate_newsletter_content with mocked LLM
- [ ] **EXT-038.37**: Test curate_newsletter_content task end-to-end
- [ ] **EXT-038.38**: Verify content quality and relevance
- [ ] **EXT-038.39**: Git add and commit: `git add apps/newsletter && git commit -m "Add newsletter content curation"`
- [ ] **EXT-038.40**: Git push: `git push origin master`

---

### EXT-039: Newsletter Generation and Sending

- [ ] **EXT-039.1**: Install django-anymail: `pip install django-anymail[mailgun]==10.2`
- [ ] **EXT-039.2**: Update requirements.txt
- [ ] **EXT-039.3**: Add EMAIL_BACKEND to settings/base.py (use anymail)
- [ ] **EXT-039.4**: Add ANYMAIL settings to settings/base.py
- [ ] **EXT-039.5**: Add email service credentials to .env.example (MAILGUN_API_KEY, MAILGUN_DOMAIN)
- [ ] **EXT-039.6**: Add email service credentials to .env file
- [ ] **EXT-039.7**: Create test file: `apps/newsletter/tests/test_sending.py`
- [ ] **EXT-039.8**: Write unit test for generate_newsletter_task()
- [ ] **EXT-039.9**: Write unit test for send_newsletter_task()
- [ ] **EXT-039.10**: Write unit test for send_newsletter_email()
- [ ] **EXT-039.11**: Update `apps/newsletter/tasks.py`
- [ ] **EXT-039.12**: Implement generate_newsletter_task() as @shared_task
- [ ] **EXT-039.13**: In generate_newsletter_task, call curate_newsletter_content()
- [ ] **EXT-039.14**: In generate_newsletter_task, create NewsletterIssue with curated content
- [ ] **EXT-039.15**: In generate_newsletter_task, add featured_articles to issue
- [ ] **EXT-039.16**: In generate_newsletter_task, queue send_newsletter_task
- [ ] **EXT-039.17**: In generate_newsletter_task, return issue ID
- [ ] **EXT-039.18**: Implement send_newsletter_task(issue_id) as @shared_task
- [ ] **EXT-039.19**: In send_newsletter_task, fetch NewsletterIssue by ID
- [ ] **EXT-039.20**: In send_newsletter_task, query active verified subscribers
- [ ] **EXT-039.21**: In send_newsletter_task, loop through subscribers
- [ ] **EXT-039.22**: In send_newsletter_task, queue send_newsletter_email for each subscriber
- [ ] **EXT-039.23**: In send_newsletter_task, update issue.sent_at and recipient_count
- [ ] **EXT-039.24**: Implement send_newsletter_email(issue_id, subscriber_id) as @shared_task
- [ ] **EXT-039.25**: In send_newsletter_email, fetch issue and subscriber
- [ ] **EXT-039.26**: In send_newsletter_email, personalize content (use subscriber name if available)
- [ ] **EXT-039.27**: In send_newsletter_email, render HTML email template
- [ ] **EXT-039.28**: In send_newsletter_email, add unsubscribe link with token
- [ ] **EXT-039.29**: In send_newsletter_email, send email using Django's send_mail
- [ ] **EXT-039.30**: In send_newsletter_email, handle sending errors
- [ ] **EXT-039.31**: In send_newsletter_email, track sending status
- [ ] **EXT-039.32**: Create `apps/newsletter/templates/newsletter/email_base.html`
- [ ] **EXT-039.33**: Design email base template with header, footer, unsubscribe link
- [ ] **EXT-039.34**: Use inline CSS for email compatibility
- [ ] **EXT-039.35**: Create `apps/newsletter/templates/newsletter/weekly_digest.html`
- [ ] **EXT-039.36**: Extend email_base.html in weekly_digest.html
- [ ] **EXT-039.37**: Add featured articles section with images and summaries
- [ ] **EXT-039.38**: Add trending topics section
- [ ] **EXT-039.39**: Add call-to-action buttons
- [ ] **EXT-039.40**: Test email rendering (use Mailtrap or similar)
- [ ] **EXT-039.41**: Configure Celery Beat for scheduled sending
- [ ] **EXT-039.42**: Add periodic task to celery beat schedule (weekly on Monday 9am)
- [ ] **EXT-039.43**: Update `extradime/settings/base.py` with CELERY_BEAT_SCHEDULE
- [ ] **EXT-039.44**: Add generate_newsletter_task to beat schedule
- [ ] **EXT-039.45**: Implement webhook handler for bounces (if using Mailgun/SendGrid)
- [ ] **EXT-039.46**: Create view to handle bounce webhooks
- [ ] **EXT-039.47**: In bounce handler, mark subscription as bounced
- [ ] **EXT-039.48**: Implement webhook handler for complaints
- [ ] **EXT-039.49**: In complaint handler, unsubscribe user
- [ ] **EXT-039.50**: Add analytics tracking (open rate, click rate) - optional
- [ ] **EXT-039.51**: Run tests: `pytest apps/newsletter/tests/test_sending.py -v`
- [ ] **EXT-039.52**: Fix any failing tests
- [ ] **EXT-039.53**: Test newsletter generation manually
- [ ] **EXT-039.54**: Test email sending to test address (use Mailtrap)
- [ ] **EXT-039.55**: Verify email renders correctly in various clients
- [ ] **EXT-039.56**: Test personalization (subscriber name, preferences)
- [ ] **EXT-039.57**: Test unsubscribe link works
- [ ] **EXT-039.58**: Test scheduled sending with Celery Beat
- [ ] **EXT-039.59**: Test bounce handling (simulate bounce)
- [ ] **EXT-039.60**: Verify analytics tracking (if implemented)
- [ ] **EXT-039.61**: Git add and commit: `git add apps/newsletter requirements.txt extradime/settings && git commit -m "Add newsletter generation and sending"`
- [ ] **EXT-039.62**: Git push: `git push origin master`

---

# Complete Project Summary

## Total Statistics

**All Phases Complete:** 39 tickets broken down into granular tasks
**Total Tasks:** 1,398
**Average Tasks per Ticket:** 35.8
**Estimated Time:** ~233 hours (at 10 minutes per task average)

### By Phase:
- **Phase 1 (Core Platform):** 29 tickets, 855 tasks, ~142 hours
- **Phase 2 (User & Community):** 7 tickets, 331 tasks, ~55 hours
- **Phase 3 (Advanced Features):** 3 tickets, 212 tasks, ~35 hours

---

## Implementation Approach

### Test-Driven Development (TDD)
Every functional ticket follows this pattern:
1. **Create test file** → Write unit tests → **Create implementation file** → Implement functionality
2. **Run tests** → Fix failures → **Manual verification** → Git commit and push

### Task Granularity
- **Setup tasks:** 5-10 minutes (file creation, configuration)
- **Test writing:** 10-15 minutes (write unit tests)
- **Implementation:** 10-20 minutes (implement methods, classes)
- **Verification:** 5-10 minutes (run tests, manual checks)
- **Git tasks:** 2-5 minutes (commit, push)

---

## Key Features

✅ **Unique Task IDs:** Every task has format `TICKET-ID.TASK-ID` (e.g., EXT-001.1)
✅ **Specific Commands:** Exact commands to run (no ambiguity)
✅ **TDD Approach:** Tests written before implementation
✅ **Verification Steps:** Browser testing, shell testing, pytest
✅ **Git Integration:** Commit and push after each ticket
✅ **Complete Coverage:** All 28 Phase 1 tickets included

---

## Usage Instructions

### For AI Coding Agents:
1. Start with `EXT-001.1` and work sequentially
2. Check off each task as completed: `- [x]`
3. Follow TDD pattern: Write tests before implementation
4. Run tests after each implementation task
5. Verify manually using provided commands
6. Commit after each ticket completion

### For Human Developers:
1. Use as detailed roadmap for implementation
2. Adjust task order if needed (maintain TDD approach)
3. Skip optional tasks (e.g., EXT-008 Docker if not needed)
4. Add custom tasks for your specific environment
5. Track progress by checking off completed tasks

---

## Epic Breakdown

### Epic 1.1: Project Foundation (195 tasks)
**Focus:** Django setup, database, Celery, core app, dependencies
**Duration:** Week 1-2
**Key Deliverables:** Working Django project with PostgreSQL, Celery, Redis, Bootstrap 5 UI

### Epic 1.2: Scraping Infrastructure (248 tasks)
**Focus:** Scraping models, admin, Scrapy spiders, task scheduler
**Duration:** Week 3-4
**Key Deliverables:** RSS and website spiders, automated scraping, error handling

### Epic 1.3: Content Management (193 tasks)
**Focus:** Content models, admin with CKEditor, views, templates, RSS feeds
**Duration:** Week 5-6
**Key Deliverables:** Article and topic management, public-facing pages, RSS feeds

### Epic 1.4: AI Content Generation (187 tasks)
**Focus:** Prompt templates, AI utilities, article generation, moderation, analytics
**Duration:** Week 7-8
**Key Deliverables:** Automated article generation, content enhancement, moderation, dashboard

---

## Technology Stack

**Backend:**
- Django 5.0.1
- PostgreSQL 15+
- Celery 5.3.4 + Redis
- Scrapy 2.11.0

**AI/ML:**
- OpenAI GPT-4
- Anthropic Claude 3
- LangChain 0.1.0
- Tenacity (retry logic)

**Frontend:**
- Bootstrap 5
- CKEditor 6.7.0
- Chart.js (for analytics)

**Testing:**
- pytest 7.4.3
- pytest-django 4.7.0
- factory-boy 3.3.0

---

## Next Steps After Phase 1

Once all 823 tasks are completed:

1. **Phase 2: Advanced Features**
   - User authentication and profiles
   - Advanced search and filtering
   - Email notifications
   - Social media integration

2. **Phase 3: Optimization**
   - Performance optimization
   - Caching strategy
   - Database indexing
   - CDN integration

3. **Phase 4: Deployment**
   - Production server setup
   - CI/CD pipeline
   - Monitoring and logging
   - Backup strategy

---

## Success Criteria

Phase 1 is complete when:
- ✅ All 823 tasks checked off
- ✅ All tests passing (pytest)
- ✅ All features working in browser
- ✅ All code committed and pushed to Git
- ✅ Documentation updated
- ✅ No critical bugs remaining

---

## Support and Resources

**Documentation:**
- `docs/improved_enhanced_tickets.md` - Detailed ticket specifications
- `docs/TICKETS_EVALUATION.md` - Quality evaluation
- `docs/CHECKLIST_SUMMARY.md` - Overview and statistics

**Getting Help:**
- Review ticket acceptance criteria
- Check implementation notes in tickets
- Refer to code examples in tickets
- Test frequently to catch issues early

---

**Document Created:** 2025-10-01
**Last Updated:** 2025-10-01
**Status:** ✅ Complete - Ready for Implementation

