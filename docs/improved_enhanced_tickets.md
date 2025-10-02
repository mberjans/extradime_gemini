# Extradime.com - Development Tickets (Improved Version)

> **Comprehensive ticket list for implementing the Extradime.com platform**
>
> **Format:** Jira-like tickets organized by Phase and Epic
> **Reference:** Based on docs/IMPLEMENTATION_GUIDE.md and docs/implementation_specs.md
>
> **⭐ IMPROVED VERSION:** This document incorporates Priority 1 and Priority 2 recommendations from `docs/TICKETS_EVALUATION.md` to address identified gaps and raise overall ticket quality from 8/10 to 9/10.
>
> **Key Improvements Applied:**
> - EXT-004: Complete base.html template code with Bootstrap 5
> - EXT-009: Inline complete DataSource model code
> - EXT-010: Specific acceptance criteria for statistics and usability
> - EXT-012: Complete method implementations for BaseSpider
> - EXT-018: CKEditor specified explicitly with rationale
> - EXT-023: Complete implementations for placeholder functions

---

## Table of Contents

- [Phase 1: Core Platform (Weeks 1-8)](#phase-1-core-platform-weeks-1-8)
  - [Epic 1.1: Project Foundation](#epic-11-project-foundation-week-1-2)
  - [Epic 1.2: Scraping Infrastructure](#epic-12-scraping-infrastructure-week-3-4)
  - [Epic 1.3: Content Management](#epic-13-content-management-week-5-6)
  - [Epic 1.4: AI Content Generation](#epic-14-ai-content-generation-week-7-8)
- [Phase 2: User & Community Features (Weeks 9-16)](#phase-2-user--community-features-weeks-9-16)
- [Phase 3: Advanced Features (Weeks 17-24)](#phase-3-advanced-features-weeks-17-24)

---

# Phase 1: Core Platform (Weeks 1-8)

## Epic 1.1: Project Foundation (Week 1-2)

### EXT-001: Django Project Initial Setup
**Type:** Task  
**Priority:** Critical  
**Estimated Time:** 8 hours  
**Dependencies:** None  
**Phase:** Phase 1 - Week 1

**Description:**
Set up the initial Django project structure with proper settings organization (base, development, production). Create the main project directory, configure settings modules, and establish the basic project structure that will serve as the foundation for all future development.

**Acceptance Criteria:**
- [ ] Django project runs without errors on `python manage.py runserver`
- [ ] Settings properly split into base.py, development.py, and production.py
- [ ] Environment variables loading correctly from .env file
- [ ] Admin interface accessible at /admin/
- [ ] Static files configuration working
- [ ] Template directories configured
- [ ] ALLOWED_HOSTS configured properly
- [ ] SECRET_KEY loaded from environment variable

**Files to Create:**
- `extradime/__init__.py`
- `extradime/settings/__init__.py`
- `extradime/settings/base.py`
- `extradime/settings/development.py`
- `extradime/settings/production.py`
- `extradime/settings/test.py`
- `extradime/urls.py`
- `extradime/wsgi.py`
- `extradime/asgi.py`
- `manage.py`
- `.env.example`
- `.gitignore`
- `README.md`

**Implementation Notes:**
- Reference: docs/implementation_specs.md Section 11 for .env.example content
- Use django-environ or python-decouple for environment variable management
- Set DEBUG=True in development.py, DEBUG=False in production.py
- Configure DATABASES in base.py to read from environment variables
- Set up STATIC_URL, STATIC_ROOT, MEDIA_URL, MEDIA_ROOT in base.py
- Configure TEMPLATES with proper directories
- Add 'django.contrib.admin', 'django.contrib.auth', etc. to INSTALLED_APPS

**Testing Requirements:**
- Verify Django server starts successfully: `python manage.py runserver`
- Verify admin interface loads: http://localhost:8000/admin/
- Verify settings load correctly: `python manage.py diffsettings`
- Test with different DJANGO_SETTINGS_MODULE values

---

### EXT-002: PostgreSQL Database Configuration
**Type:** Task  
**Priority:** Critical  
**Estimated Time:** 4 hours  
**Dependencies:** EXT-001  
**Phase:** Phase 1 - Week 1

**Description:**
Configure PostgreSQL database connection, create database and user, set up connection parameters in Django settings, and verify database connectivity. Ensure proper permissions and test CRUD operations.

**Acceptance Criteria:**
- [ ] PostgreSQL database created (extradime_db)
- [ ] PostgreSQL user created with proper permissions (extradime_user)
- [ ] Database connection configured in settings
- [ ] Can connect to PostgreSQL from Django
- [ ] Initial migrations run successfully
- [ ] Can create/read/update/delete test records via Django ORM
- [ ] Database connection pooling configured (if using pgbouncer)

**Files to Create/Modify:**
- `extradime/settings/base.py` (update DATABASES configuration)
- `.env` (add database credentials)

**Implementation Notes:**
- Use psycopg2-binary for PostgreSQL adapter
- Database configuration in base.py:
  ```python
  DATABASES = {
      'default': {
          'ENGINE': 'django.db.backends.postgresql',
          'NAME': env('DB_NAME'),
          'USER': env('DB_USER'),
          'PASSWORD': env('DB_PASSWORD'),
          'HOST': env('DB_HOST', default='localhost'),
          'PORT': env('DB_PORT', default='5432'),
      }
  }
  ```
- Create database: `createdb extradime_db`
- Create user: `createuser extradime_user -P`
- Grant privileges: `GRANT ALL PRIVILEGES ON DATABASE extradime_db TO extradime_user;`

**Testing Requirements:**
- Test connection: `python manage.py dbshell`
- Run migrations: `python manage.py migrate`
- Create test model and verify CRUD operations
- Check connection in Django shell: `python manage.py shell`

---

### EXT-003: Celery and Redis Setup
**Type:** Task  
**Priority:** Critical  
**Estimated Time:** 6 hours  
**Dependencies:** EXT-001  
**Phase:** Phase 1 - Week 1

**Description:**
Set up Celery for asynchronous task processing with Redis as the message broker. Configure Celery Beat for scheduled tasks, create the Celery app configuration, and verify that tasks can be executed successfully.

**Acceptance Criteria:**
- [ ] Redis installed and running
- [ ] Celery worker starts without errors
- [ ] Celery beat scheduler runs successfully
- [ ] Can execute test task successfully
- [ ] Tasks appear in Redis
- [ ] Task results stored correctly
- [ ] Celery monitoring accessible (Flower optional)
- [ ] Scheduled tasks configured in Celery Beat

**Files to Create:**
- `extradime/celery.py`
- `extradime/__init__.py` (update to load Celery)
- `apps/core/tasks.py` (test task)

**Files to Modify:**
- `extradime/settings/base.py` (add Celery configuration)
- `requirements.txt` (add celery, redis, django-celery-beat, django-celery-results)

**Implementation Notes:**
- Reference: docs/implementation_specs.md Section 12 for dependencies
- Celery configuration in base.py:
  ```python
  CELERY_BROKER_URL = env('CELERY_BROKER_URL', default='redis://localhost:6379/0')
  CELERY_RESULT_BACKEND = env('CELERY_RESULT_BACKEND', default='redis://localhost:6379/0')
  CELERY_ACCEPT_CONTENT = ['json']
  CELERY_TASK_SERIALIZER = 'json'
  CELERY_RESULT_SERIALIZER = 'json'
  CELERY_TIMEZONE = 'UTC'
  ```
- Create test task to verify setup
- Add 'django_celery_beat', 'django_celery_results' to INSTALLED_APPS
- Run migrations for celery apps

**Testing Requirements:**
- Start Redis: `redis-server`
- Start Celery worker: `celery -A extradime worker -l info`
- Start Celery beat: `celery -A extradime beat -l info`
- Execute test task and verify completion
- Check task in Redis: `redis-cli KEYS *`
- Verify task results in database

---

### EXT-004: Core App Setup
**Type:** Task
**Priority:** High
**Estimated Time:** 4 hours
**Dependencies:** EXT-001
**Phase:** Phase 1 - Week 1

**Description:**
Create the core Django app that will contain shared functionality, base templates, homepage, and common utilities. Set up the base template structure with navigation, footer, and CSS/JS includes using Bootstrap 5.

**Acceptance Criteria:**
- [ ] Core app created and added to INSTALLED_APPS
- [ ] Home page renders correctly at /
- [ ] Base template includes Bootstrap 5 CSS/JS
- [ ] Navigation structure in place with logo, main menu, and mobile toggle
- [ ] Footer with links present (About, Contact, Privacy Policy, Terms)
- [ ] Static files loading correctly (verified in browser console, no 404 errors)
- [ ] Responsive design implemented: works on mobile (320px), tablet (768px), desktop (1024px+)
- [ ] About page created and accessible at /about/

**Files to Create:**
- `apps/__init__.py`
- `apps/core/__init__.py`
- `apps/core/apps.py`
- `apps/core/models.py`
- `apps/core/views.py`
- `apps/core/urls.py`
- `apps/core/utils.py`
- `apps/core/middleware.py`
- `apps/core/templates/core/base.html`
- `apps/core/templates/core/home.html`
- `apps/core/templates/core/about.html`
- `static/css/main.css`
- `static/js/main.js`

**Files to Modify:**
- `extradime/settings/base.py` (add 'apps.core' to INSTALLED_APPS)
- `extradime/urls.py` (include core.urls)

**Implementation Notes:**
- Use Django's startapp command: `python manage.py startapp core apps/core`
- **CSS Framework Choice: Bootstrap 5**
  - Rationale: Extensive component library, excellent documentation, rapid development, strong community support
  - Alternative considered: Tailwind CSS (more customizable but steeper learning curve)
- **Complete base.html template:**
  ```html
  {% load static %}
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta name="description" content="{% block meta_description %}Discover legitimate ways to earn extra income online. Reviews, guides, and opportunities for side hustles and freelancing.{% endblock %}">
      <meta name="keywords" content="{% block meta_keywords %}extra income, side hustle, freelancing, online earning{% endblock %}">
      <title>{% block title %}Extradime.com - Earn Extra Income Online{% endblock %}</title>

      <!-- Bootstrap 5 CSS -->
      <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

      <!-- Custom CSS -->
      <link rel="stylesheet" href="{% static 'css/main.css' %}">

      {% block extra_css %}{% endblock %}
  </head>
  <body>
      <!-- Navigation -->
      <nav class="navbar navbar-expand-lg navbar-light bg-light shadow-sm">
          <div class="container">
              <a class="navbar-brand fw-bold" href="{% url 'core:home' %}">
                  <span class="text-primary">Extra</span><span class="text-success">dime</span>.com
              </a>
              <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                  <span class="navbar-toggler-icon"></span>
              </button>
              <div class="collapse navbar-collapse" id="navbarNav">
                  <ul class="navbar-nav ms-auto">
                      <li class="nav-item">
                          <a class="nav-link" href="{% url 'core:home' %}">Home</a>
                      </li>
                      <li class="nav-item">
                          <a class="nav-link" href="{% url 'content:article_list' %}">Articles</a>
                      </li>
                      <li class="nav-item">
                          <a class="nav-link" href="{% url 'content:opportunity_list' %}">Opportunities</a>
                      </li>
                      <li class="nav-item">
                          <a class="nav-link" href="{% url 'core:about' %}">About</a>
                      </li>
                  </ul>
              </div>
          </div>
      </nav>

      <!-- Main Content -->
      <main class="container my-4">
          {% block content %}{% endblock %}
      </main>

      <!-- Footer -->
      <footer class="bg-dark text-white mt-5 py-4">
          <div class="container">
              <div class="row">
                  <div class="col-md-4 mb-3">
                      <h5>Extradime.com</h5>
                      <p class="small">Your trusted source for legitimate online earning opportunities.</p>
                  </div>
                  <div class="col-md-4 mb-3">
                      <h6>Quick Links</h6>
                      <ul class="list-unstyled">
                          <li><a href="{% url 'core:about' %}" class="text-white-50">About Us</a></li>
                          <li><a href="#" class="text-white-50">Contact</a></li>
                          <li><a href="#" class="text-white-50">Privacy Policy</a></li>
                          <li><a href="#" class="text-white-50">Terms of Service</a></li>
                      </ul>
                  </div>
                  <div class="col-md-4 mb-3">
                      <h6>Follow Us</h6>
                      <p class="small">Stay updated with the latest opportunities</p>
                      <!-- Social media links can be added here -->
                  </div>
              </div>
              <hr class="bg-white">
              <div class="text-center small">
                  <p>&copy; {% now "Y" %} Extradime.com. All rights reserved.</p>
              </div>
          </div>
      </footer>

      <!-- Bootstrap 5 JS Bundle (includes Popper) -->
      <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>

      <!-- Custom JS -->
      <script src="{% static 'js/main.js' %}"></script>

      {% block extra_js %}{% endblock %}
  </body>
  </html>
  ```
- Home view should be a simple TemplateView
- Set up URL routing in extradime/urls.py
- **Responsive Breakpoints:**
  - Mobile: 320px - 767px (single column layout)
  - Tablet: 768px - 1023px (two column layout)
  - Desktop: 1024px+ (full multi-column layout)

**Testing Requirements:**
- Access home page: http://localhost:8000/
- Verify static files load (check browser console for no 404 errors)
- Test navigation links (all should be clickable)
- Verify responsive design:
  - Mobile (320px): Navigation collapses to hamburger menu
  - Tablet (768px): Two-column footer layout
  - Desktop (1024px+): Full navigation bar, three-column footer
- Check HTML validation: https://validator.w3.org/
- Test mobile toggle button functionality

---

### EXT-005: Requirements and Dependencies Installation
**Type:** Task  
**Priority:** Critical  
**Estimated Time:** 2 hours  
**Dependencies:** None  
**Phase:** Phase 1 - Week 1

**Description:**
Create comprehensive requirements.txt file with all necessary dependencies for the project, including Django, Celery, Scrapy, AI libraries, and development tools. Set up virtual environment and install all dependencies.

**Acceptance Criteria:**
- [ ] requirements.txt created with all dependencies
- [ ] requirements-dev.txt created for development tools
- [ ] Virtual environment created
- [ ] All dependencies install without errors
- [ ] No version conflicts
- [ ] Dependencies pinned to specific versions
- [ ] Can import all major libraries in Python shell

**Files to Create:**
- `requirements.txt`
- `requirements-dev.txt`
- `setup.cfg` (optional, for project metadata)

**Implementation Notes:**
- Reference: docs/implementation_specs.md Section 12.1 for complete requirements.txt
- Key dependencies:
  - Django==5.0.1
  - celery==5.3.4
  - scrapy==2.11.0
  - openai==1.6.1
  - anthropic==0.8.1
  - langchain==0.1.0
  - psycopg2-binary==2.9.9
  - redis==5.0.1
  - beautifulsoup4==4.12.2
  - pytest==7.4.3
  - (see full list in implementation_specs.md)
- Create virtual environment: `python -m venv venv`
- Activate: `source venv/bin/activate`
- Install: `pip install -r requirements.txt`

**Testing Requirements:**
- Verify installation: `pip list`
- Test imports in Python shell:
  ```python
  import django
  import celery
  import scrapy
  import openai
  import anthropic
  ```
- Check for security vulnerabilities: `pip check`
- Generate requirements: `pip freeze > requirements-frozen.txt`

---

### EXT-008: Docker Configuration (Optional)
**Type:** Task
**Priority:** Low
**Estimated Time:** 4 hours
**Dependencies:** EXT-001, EXT-002, EXT-003
**Phase:** Phase 1 - Week 2

**Description:**
Create Docker and docker-compose configuration for containerized development and deployment. Set up containers for Django, PostgreSQL, Redis, and Celery workers.

**Acceptance Criteria:**
- [ ] Dockerfile created for Django app
- [ ] docker-compose.yml created with all services
- [ ] All services start with docker-compose up
- [ ] Database persists data with volumes
- [ ] Can access Django app from host
- [ ] Celery workers running in containers
- [ ] Environment variables passed to containers
- [ ] Development and production configurations

**Files to Create:**
- `Dockerfile`
- `docker-compose.yml`
- `docker-compose.prod.yml`
- `.dockerignore`
- `scripts/docker-entrypoint.sh`

**Implementation Notes:**
- Reference: docs/implementation_specs.md Section 10 for file structure
- Use official Python image as base
- Configure services: web, db, redis, celery_worker, celery_beat
- Mount code as volume for development
- Use named volumes for database persistence
- Configure health checks for services
- Set up proper networking between containers

**Testing Requirements:**
- Build image: `docker-compose build`
- Start services: `docker-compose up`
- Verify all services healthy: `docker-compose ps`
- Access Django: http://localhost:8000/
- Check logs: `docker-compose logs`
- Test database persistence after restart

---

## Epic 1.2: Scraping Infrastructure (Week 3-4)

### EXT-009: Scraping App Models
**Type:** Task
**Priority:** Critical
**Estimated Time:** 6 hours
**Dependencies:** EXT-002
**Phase:** Phase 1 - Week 3

**Description:**
Create Django models for the scraping app: DataSource and ScrapedOpportunity. Implement all fields, methods, properties, and Meta classes as specified in the implementation specs. Create and run migrations.

**Acceptance Criteria:**
- [ ] DataSource model created with all fields
- [ ] ScrapedOpportunity model created with all fields
- [ ] All model methods implemented (mark_checked, record_error, etc.)
- [ ] All properties implemented (needs_check, is_new)
- [ ] Migrations created and applied successfully
- [ ] Can create DataSource via Django admin
- [ ] Can create ScrapedOpportunity via Django admin
- [ ] All model methods work correctly
- [ ] Unit tests written and passing

**Files to Create:**
- `apps/scraping/__init__.py`
- `apps/scraping/apps.py`
- `apps/scraping/models.py`
- `apps/scraping/tests/__init__.py`
- `apps/scraping/tests/test_models.py`
- `apps/scraping/migrations/0001_initial.py` (auto-generated)

**Files to Modify:**
- `extradime/settings/base.py` (add 'apps.scraping' to INSTALLED_APPS)

**Implementation Notes:**
- **Complete DataSource Model:**
  ```python
  from django.db import models
  from django.utils import timezone

  class DataSource(models.Model):
      """Source for scraping opportunities (RSS feeds, websites, APIs)."""

      SOURCE_TYPES = [
          ('rss', 'RSS Feed'),
          ('website', 'Website'),
          ('api', 'API'),
      ]

      # Basic Information
      name = models.CharField(
          max_length=200,
          help_text="Human-readable name for this data source"
      )
      url = models.URLField(
          max_length=500,
          help_text="Main URL of the source"
      )
      feed_url = models.URLField(
          max_length=500,
          blank=True,
          null=True,
          help_text="RSS feed URL (if applicable)"
      )
      source_type = models.CharField(
          max_length=20,
          choices=SOURCE_TYPES,
          default='rss',
          help_text="Type of data source"
      )

      # Status and Configuration
      is_active = models.BooleanField(
          default=True,
          help_text="Whether this source is currently being scraped"
      )
      check_frequency_hours = models.IntegerField(
          default=24,
          help_text="How often to check this source (in hours)"
      )
      custom_settings = models.JSONField(
          default=dict,
          blank=True,
          help_text="Custom scraping settings (selectors, filters, etc.)"
      )

      # Statistics and Tracking
      last_checked = models.DateTimeField(
          null=True,
          blank=True,
          help_text="Last time this source was checked"
      )
      total_opportunities_found = models.IntegerField(
          default=0,
          help_text="Total number of opportunities found from this source"
      )
      last_error = models.TextField(
          blank=True,
          null=True,
          help_text="Last error message encountered"
      )
      error_count = models.IntegerField(
          default=0,
          help_text="Number of consecutive errors"
      )

      # Timestamps
      created_at = models.DateTimeField(auto_now_add=True)
      updated_at = models.DateTimeField(auto_now=True)

      class Meta:
          ordering = ['-created_at']
          indexes = [
              models.Index(fields=['is_active', 'last_checked']),
              models.Index(fields=['source_type']),
          ]

      def __str__(self):
          return f"{self.name} ({self.get_source_type_display()})"

      @property
      def needs_check(self):
          """Check if source needs to be scraped based on frequency."""
          if not self.is_active:
              return False
          if not self.last_checked:
              return True
          time_since_check = timezone.now() - self.last_checked
          return time_since_check.total_seconds() / 3600 >= self.check_frequency_hours

      def mark_checked(self):
          """Mark source as checked and reset error count."""
          self.last_checked = timezone.now()
          self.error_count = 0
          self.last_error = None
          self.save(update_fields=['last_checked', 'error_count', 'last_error'])

      def record_error(self, error_message):
          """Record an error for this source."""
          self.error_count += 1
          self.last_error = str(error_message)[:500]  # Truncate long errors
          self.last_checked = timezone.now()
          self.save(update_fields=['error_count', 'last_error', 'last_checked'])

          # Deactivate if too many consecutive errors
          if self.error_count >= 5:
              self.is_active = False
              self.save(update_fields=['is_active'])

      def increment_opportunities_found(self, count=1):
          """Increment the total opportunities found counter."""
          self.total_opportunities_found += count
          self.save(update_fields=['total_opportunities_found'])
  ```

- **ScrapedOpportunity Model** (see docs/implementation_specs.md Section 13.1 for complete code):
  - Key fields: title, description, url, source (ForeignKey to DataSource)
  - Status choices: NEW, PROCESSED, REJECTED, USED_IN_CONTENT
  - Tracking: date_discovered, processed_at, quality_score
  - Data: raw_data (JSONField), potential_earnings_text, requirements_text, location
  - Methods: mark_processed(), mark_rejected(), mark_used_in_content()
  - Properties: is_new, age_in_days

- Add indexes for performance on frequently queried fields
- Implement __str__ methods for admin display
- Add help_text for all fields for better admin UX

**Testing Requirements:**
- Run migrations: `python manage.py makemigrations scraping`
- Apply migrations: `python manage.py migrate`
- Unit tests for all model methods
- Test model creation in Django shell
- Test relationships between models
- Run tests: `pytest apps/scraping/tests/test_models.py`

---

### EXT-010: Scraping Admin Interface
**Type:** Task
**Priority:** High
**Estimated Time:** 4 hours
**Dependencies:** EXT-009
**Phase:** Phase 1 - Week 3

**Description:**
Create customized Django admin interface for DataSource and ScrapedOpportunity models. Add custom list displays, filters, search fields, and admin actions for managing scraped data.

**Acceptance Criteria:**
- [ ] DataSource admin registered with custom configuration
- [ ] ScrapedOpportunity admin registered with custom configuration
- [ ] List displays show key fields (name, source_type, is_active, last_checked for DataSource)
- [ ] Filters work correctly (status, source_type, date ranges)
- [ ] Search functionality works (searches name, url for DataSource; title, description for ScrapedOpportunity)
- [ ] Custom admin actions implemented (Run Spider Now, Mark as Processed)
- [ ] Statistics displayed correctly: shows total_opportunities_found, error_count, last_checked with accurate values from database
- [ ] Inline editing works where appropriate (is_active, check_frequency_hours can be edited inline)
- [ ] Admin interface is user-friendly: all CRUD operations accessible within 2 clicks, clear field labels, helpful error messages, readonly fields clearly marked

**Files to Create:**
- `apps/scraping/admin.py`

**Implementation Notes:**
- DataSource admin:
  - list_display: name, source_type, is_active, last_checked, total_opportunities_found, error_count
  - list_filter: source_type, is_active
  - search_fields: name, url
  - actions: activate_sources, deactivate_sources, run_spider_now
  - readonly_fields: last_checked, total_opportunities_found, error_count, created_at, updated_at
- ScrapedOpportunity admin:
  - list_display: title, source, status, date_discovered, quality_score
  - list_filter: status, source, date_discovered
  - search_fields: title, description, url
  - actions: mark_as_processed, mark_as_rejected, mark_as_used
  - readonly_fields: date_discovered, processed_at, raw_data
- Add custom CSS for admin if needed

**Testing Requirements:**
- Access admin: http://localhost:8000/admin/scraping/
- Test all filters and search
- Test custom actions
- Create test DataSource and verify display
- Create test ScrapedOpportunity and verify display
- Test inline editing

---

### EXT-011: Scrapy Project Setup
**Type:** Task
**Priority:** Critical
**Estimated Time:** 4 hours
**Dependencies:** EXT-009
**Phase:** Phase 1 - Week 3

**Description:**
Set up Scrapy project structure within the Django app, configure Scrapy settings, create items and pipelines for saving data to Django database. Integrate Scrapy with Django ORM.

**Acceptance Criteria:**
- [ ] Scrapy project structure created
- [ ] Scrapy settings configured
- [ ] Items defined for scraped data
- [ ] Pipeline created to save to Django database
- [ ] Scrapy can access Django models
- [ ] Settings include user agent, delays, robots.txt obedience
- [ ] Middleware configured for error handling
- [ ] Can run Scrapy spiders from command line

**Files to Create:**
- `apps/scraping/scrapy.cfg`
- `apps/scraping/settings.py` (Scrapy settings)
- `apps/scraping/items.py`
- `apps/scraping/pipelines.py`
- `apps/scraping/middlewares.py`
- `apps/scraping/spiders/__init__.py`

**Files to Modify:**
- `extradime/settings/base.py` (add Scrapy Django integration)

**Implementation Notes:**
- Configure Scrapy settings:
  - BOT_NAME = 'extradime_scraper'
  - ROBOTSTXT_OBEY = True
  - DOWNLOAD_DELAY = 2
  - CONCURRENT_REQUESTS = 8
  - USER_AGENT from environment variable
  - Enable pipelines
- Create OpportunityItem with fields matching ScrapedOpportunity model
- Pipeline should:
  - Connect to Django database
  - Create or update ScrapedOpportunity records
  - Handle duplicates (check by URL)
  - Update DataSource statistics
  - Log errors
- Add Django settings integration:
  ```python
  import os
  import django
  os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'extradime.settings.development')
  django.setup()
  ```

**Testing Requirements:**
- Verify Scrapy settings load correctly
- Test pipeline with mock data
- Verify Django models accessible from Scrapy
- Test duplicate handling
- Run: `scrapy list` (should show no spiders yet)

---

### EXT-012: Base Spider Implementation
**Type:** Task
**Priority:** High
**Estimated Time:** 6 hours
**Dependencies:** EXT-011
**Phase:** Phase 1 - Week 3

**Description:**
Create base spider class with common functionality: robots.txt checking, rate limiting, error handling, logging, and user agent rotation. This will be the parent class for all specific spiders.

**Acceptance Criteria:**
- [ ] BaseSpider class created
- [ ] Robots.txt checking implemented
- [ ] Rate limiting working
- [ ] Error handling implemented
- [ ] Logging configured
- [ ] User agent rotation (if configured)
- [ ] Request/response middleware working
- [ ] Can be subclassed by specific spiders
- [ ] Unit tests passing

**Files to Create:**
- `apps/scraping/spiders/base_spider.py`
- `apps/scraping/robots_checker.py`
- `apps/scraping/tests/test_spiders.py`

**Implementation Notes:**
- BaseSpider should inherit from scrapy.Spider
- **Complete BaseSpider Implementation:**
  ```python
  import scrapy
  import logging
  from reppy.robots import Robots
  from scrapy.exceptions import IgnoreRequest
  from twisted.internet.error import TimeoutError, ConnectionRefusedError, DNSLookupError

  logger = logging.getLogger(__name__)

  class BaseSpider(scrapy.Spider):
      """Base spider with common functionality for all spiders."""

      name = 'base_spider'

      custom_settings = {
          'DOWNLOAD_DELAY': 2,
          'CONCURRENT_REQUESTS_PER_DOMAIN': 8,
          'RETRY_TIMES': 3,
          'RETRY_HTTP_CODES': [500, 502, 503, 504, 408, 429],
          'ROBOTSTXT_OBEY': True,
      }

      def __init__(self, *args, **kwargs):
          super().__init__(*args, **kwargs)
          self.robots_cache = {}

      def check_robots_txt(self, url):
          """
          Verify URL is allowed by robots.txt using reppy library.

          Args:
              url (str): URL to check

          Returns:
              bool: True if allowed, False if blocked
          """
          try:
              # Extract base URL for robots.txt
              from urllib.parse import urlparse
              parsed = urlparse(url)
              base_url = f"{parsed.scheme}://{parsed.netloc}"
              robots_url = f"{base_url}/robots.txt"

              # Check cache first
              if robots_url not in self.robots_cache:
                  try:
                      self.robots_cache[robots_url] = Robots.fetch(robots_url)
                  except Exception as e:
                      logger.warning(f"Could not fetch robots.txt from {robots_url}: {e}")
                      # Fail open - allow if robots.txt unavailable
                      return True

              robots = self.robots_cache[robots_url]
              user_agent = self.settings.get('USER_AGENT', '*')

              if robots.allowed(url, user_agent):
                  return True
              else:
                  logger.warning(f"URL blocked by robots.txt: {url}")
                  return False

          except Exception as e:
              logger.error(f"Error checking robots.txt for {url}: {e}")
              # Fail open on error
              return True

      def handle_error(self, failure):
          """
          Log and handle spider errors with specific error type handling.

          Args:
              failure: Twisted Failure object
          """
          request = failure.request

          # Handle specific error types
          if failure.check(TimeoutError):
              logger.error(f"Timeout error for {request.url}")
              # Could implement retry logic here

          elif failure.check(ConnectionRefusedError):
              logger.error(f"Connection refused for {request.url}")
              # Mark source as potentially down

          elif failure.check(DNSLookupError):
              logger.error(f"DNS lookup failed for {request.url}")
              # Mark source as invalid

          elif failure.check(IgnoreRequest):
              logger.warning(f"Request ignored for {request.url}")

          else:
              # Generic error handling
              logger.error(f"Spider error for {request.url}: {failure.value}")

          # Log full traceback for debugging
          logger.debug(f"Full error traceback: {failure.getTraceback()}")

      def extract_text(self, selector, xpath, default=''):
          """
          Safely extract text from selector using XPath.

          Args:
              selector: Scrapy selector object
              xpath (str): XPath expression
              default (str): Default value if extraction fails

          Returns:
              str: Extracted text or default value
          """
          try:
              result = selector.xpath(xpath).get()
              if result:
                  # Clean whitespace
                  return result.strip()
              return default
          except Exception as e:
              logger.warning(f"Error extracting text with xpath '{xpath}': {e}")
              return default

      def extract_url(self, selector, xpath, response=None, default=''):
          """
          Safely extract and normalize URL from selector using XPath.

          Args:
              selector: Scrapy selector object
              xpath (str): XPath expression
              response: Scrapy response object (for urljoin)
              default (str): Default value if extraction fails

          Returns:
              str: Extracted and normalized URL or default value
          """
          try:
              url = selector.xpath(xpath).get()
              if url:
                  url = url.strip()
                  # Convert relative URLs to absolute
                  if response:
                      url = response.urljoin(url)
                  return url
              return default
          except Exception as e:
              logger.warning(f"Error extracting URL with xpath '{xpath}': {e}")
              return default

      def parse_common(self, response):
          """
          Common parsing logic that can be overridden by subclasses.
          Checks robots.txt and handles errors.
          """
          # Check robots.txt
          if not self.check_robots_txt(response.url):
              logger.warning(f"Skipping {response.url} - blocked by robots.txt")
              return

          # Subclasses should override this method
          raise NotImplementedError("Subclasses must implement parse_common()")
  ```

- **Example Usage:**
  ```python
  class MySpider(BaseSpider):
      name = 'my_spider'

      def parse(self, response):
          # Use inherited methods
          title = self.extract_text(response, '//h1/text()')
          link = self.extract_url(response, '//a/@href', response)

          yield {
              'title': title,
              'link': link,
          }
  ```

- Add custom settings for rate limiting and retry behavior
- Implement comprehensive logging at appropriate levels (debug, info, warning, error)
- Handle common exceptions gracefully with fail-open approach where appropriate

**Testing Requirements:**
- Unit tests for robots.txt checking
- Test error handling with mock failures
- Test rate limiting
- Test text/URL extraction methods
- Mock HTTP responses for testing

---

### EXT-013: RSS Feed Spider
**Type:** Task
**Priority:** High
**Estimated Time:** 8 hours
**Dependencies:** EXT-012
**Phase:** Phase 1 - Week 4

**Description:**
Implement RSS feed spider for parsing RSS/Atom feeds from various sources. Extract opportunity data from feed items, handle different feed formats, and save to database via pipeline.

**Acceptance Criteria:**
- [ ] RSSSpider class created inheriting from BaseSpider
- [ ] Can parse RSS 2.0 feeds
- [ ] Can parse Atom feeds
- [ ] Extracts title, description, link, pubDate
- [ ] Handles missing fields gracefully
- [ ] Saves data to ScrapedOpportunity model
- [ ] Updates DataSource last_checked timestamp
- [ ] Handles feed parsing errors
- [ ] Unit tests passing
- [ ] Integration test with real feed

**Files to Create:**
- `apps/scraping/spiders/rss_spider.py`
- `apps/scraping/tests/test_rss_spider.py`
- `apps/scraping/tests/fixtures/sample_rss.xml`

**Implementation Notes:**
- Use feedparser library for parsing
- Spider should accept feed_url as argument
- Parse feed items and create OpportunityItem for each
- Extract fields:
  - title: entry.title
  - description: entry.summary or entry.description
  - url: entry.link
  - raw_data: entire entry as JSON
- Handle different feed formats (RSS 2.0, Atom, RSS 1.0)
- Handle malformed feeds gracefully
- Log parsing errors
- Example usage:
  ```bash
  scrapy crawl rss -a feed_url=https://example.com/feed.xml -a source_id=1
  ```

**Testing Requirements:**
- Create sample RSS feed fixture
- Test parsing with sample feed
- Test with malformed feed
- Test with missing fields
- Integration test with real feed (e.g., Reddit RSS)
- Verify data saved to database
- Run: `scrapy crawl rss -a feed_url=<test_url> -a source_id=1`

---

### EXT-014: Website Spider Template
**Type:** Task
**Priority:** Medium
**Estimated Time:** 8 hours
**Dependencies:** EXT-012
**Phase:** Phase 1 - Week 4

**Description:**
Create a template spider for scraping regular websites (non-RSS). Implement CSS/XPath selectors for extracting opportunity data, pagination handling, and JavaScript rendering support (if needed).

**Acceptance Criteria:**
- [ ] WebsiteSpider class created
- [ ] CSS/XPath selectors configurable
- [ ] Pagination handling implemented
- [ ] Can extract structured data from HTML
- [ ] Handles JavaScript-rendered content (Selenium integration)
- [ ] Respects robots.txt
- [ ] Rate limiting working
- [ ] Error handling for missing elements
- [ ] Unit tests passing

**Files to Create:**
- `apps/scraping/spiders/website_spider.py`
- `apps/scraping/tests/test_website_spider.py`
- `apps/scraping/tests/fixtures/sample_html.html`

**Implementation Notes:**
- Spider should be configurable via custom_settings in DataSource
- Selectors should be passed as arguments or stored in DataSource.custom_settings
- Example selectors configuration:
  ```json
  {
    "title_selector": "h2.job-title::text",
    "description_selector": "div.job-description::text",
    "url_selector": "a.job-link::attr(href)",
    "pagination_selector": "a.next-page::attr(href)"
  }
  ```
- Implement pagination:
  - Extract next page URL
  - Follow pagination links
  - Stop at max_pages limit
- For JavaScript sites:
  - Use Selenium with headless Chrome
  - Wait for elements to load
  - Extract rendered HTML
- Use BeautifulSoup for complex HTML parsing

**Testing Requirements:**
- Create sample HTML fixture
- Test selector extraction
- Test pagination
- Test with missing elements
- Test JavaScript rendering (if implemented)
- Integration test with real website

---

### EXT-015: Scraping Celery Tasks
**Type:** Task
**Priority:** Critical
**Estimated Time:** 8 hours
**Dependencies:** EXT-013, EXT-014
**Phase:** Phase 1 - Week 4

**Description:**
Create Celery tasks for running spiders asynchronously, scheduling regular scraping jobs, and managing scraping workflows. Implement tasks for checking all sources, running individual spiders, and cleanup.

**Acceptance Criteria:**
- [ ] run_spider_task implemented
- [ ] check_all_sources_task implemented
- [ ] cleanup_old_opportunities_task implemented
- [ ] Tasks can be triggered manually
- [ ] Tasks can be scheduled with Celery Beat
- [ ] Error handling and retry logic implemented
- [ ] Task results logged
- [ ] DataSource statistics updated after scraping
- [ ] Unit tests passing

**Files to Create:**
- `apps/scraping/tasks.py`
- `apps/scraping/tests/test_tasks.py`

**Files to Modify:**
- `extradime/settings/base.py` (add Celery Beat schedule)

**Implementation Notes:**
- Implement tasks:
  ```python
  @shared_task(bind=True, max_retries=3)
  def run_spider_task(self, spider_name, source_id):
      """Run a specific spider for a data source."""
      # Get DataSource
      # Configure spider
      # Run spider using CrawlerProcess or scrapyd
      # Update DataSource statistics
      # Handle errors and retry

  @shared_task
  def check_all_sources():
      """Check all active sources that need updating."""
      # Get sources where needs_check=True
      # Queue run_spider_task for each

  @shared_task
  def cleanup_old_opportunities():
      """Delete old rejected opportunities."""
      # Delete opportunities older than 90 days with status='REJECTED'
  ```
- Configure Celery Beat schedule:
  ```python
  CELERY_BEAT_SCHEDULE = {
      'check-sources-every-hour': {
          'task': 'apps.scraping.tasks.check_all_sources',
          'schedule': crontab(minute=0),  # Every hour
      },
      'cleanup-old-opportunities': {
          'task': 'apps.scraping.tasks.cleanup_old_opportunities',
          'schedule': crontab(hour=2, minute=0),  # Daily at 2 AM
      },
  }
  ```
- Use CrawlerRunner for running spiders from Django
- Log all task executions
- Update DataSource.last_checked after scraping
- Handle spider errors and update DataSource.last_error

**Testing Requirements:**
- Unit tests for each task
- Mock spider execution
- Test error handling and retries
- Test Celery Beat schedule
- Integration test: trigger task and verify execution
- Run: `celery -A extradime worker -l info`
- Trigger task: `python manage.py shell` then `run_spider_task.delay('rss', 1)`

---

### EXT-016: Scraping Utilities and Helpers
**Type:** Task
**Priority:** Medium
**Estimated Time:** 4 hours
**Dependencies:** EXT-009
**Phase:** Phase 1 - Week 4

**Description:**
Create utility functions for scraping operations: URL validation, text cleaning, duplicate detection, quality scoring, and data extraction helpers.

**Acceptance Criteria:**
- [ ] URL validation function implemented
- [ ] Text cleaning function implemented
- [ ] Duplicate detection function implemented
- [ ] Quality scoring function implemented
- [ ] Data extraction helpers implemented
- [ ] All functions have docstrings
- [ ] Unit tests passing
- [ ] Functions used in spiders and pipelines

**Files to Create:**
- `apps/scraping/utils.py`
- `apps/scraping/tests/test_utils.py`

**Implementation Notes:**
- Implement utility functions:
  ```python
  def validate_url(url: str) -> bool:
      """Validate URL format and accessibility."""

  def clean_text(text: str) -> str:
      """Clean and normalize text (remove extra whitespace, HTML entities)."""

  def is_duplicate(url: str) -> bool:
      """Check if opportunity with this URL already exists."""

  def calculate_quality_score(opportunity_data: dict) -> float:
      """Calculate quality score (0-1) based on completeness and content."""

  def extract_earnings(text: str) -> Optional[str]:
      """Extract earnings information from text."""

  def extract_requirements(text: str) -> Optional[str]:
      """Extract requirements from text."""

  def detect_scam_indicators(text: str) -> List[str]:
      """Detect potential scam indicators in text."""
  ```
- Quality scoring criteria:
  - Has title: +0.2
  - Has description (>100 chars): +0.3
  - Has earnings info: +0.2
  - Has requirements: +0.2
  - No scam indicators: +0.1
- Use regex for earnings/requirements extraction
- Scam indicators: "get rich quick", "guaranteed income", "no experience needed + high pay", etc.

**Testing Requirements:**
- Unit tests for each function
- Test edge cases (empty strings, None, malformed data)
- Test quality scoring with various inputs
- Test scam detection with known scam phrases
- Run: `pytest apps/scraping/tests/test_utils.py -v`

---

## Epic 1.3: Content Management (Week 5-6)

### EXT-017: Content App Models
**Type:** Task
**Priority:** Critical
**Estimated Time:** 8 hours
**Dependencies:** EXT-002, EXT-009
**Phase:** Phase 1 - Week 5

**Description:**
Create Django models for content management: Topic, Article, PromptLog, and ContentRevision. Implement all fields, relationships, methods, and Meta classes. Create and run migrations.

**Acceptance Criteria:**
- [ ] Topic model created with all fields
- [ ] Article model created with all fields
- [ ] PromptLog model created with all fields
- [ ] ContentRevision model created with all fields
- [ ] All relationships configured correctly
- [ ] All model methods implemented
- [ ] Migrations created and applied
- [ ] Can create records via Django admin
- [ ] Unit tests passing

**Files to Create:**
- `apps/content/__init__.py`
- `apps/content/apps.py`
- `apps/content/models.py`
- `apps/content/tests/__init__.py`
- `apps/content/tests/test_models.py`
- `apps/content/migrations/0001_initial.py` (auto-generated)

**Files to Modify:**
- `extradime/settings/base.py` (add 'apps.content' to INSTALLED_APPS)

**Implementation Notes:**
- Topic model fields:
  - name (CharField, unique)
  - slug (SlugField, unique, auto-generated)
  - description (TextField, nullable)
  - created_at, updated_at
- Article model fields:
  - title (CharField)
  - slug (SlugField, unique, auto-generated)
  - body (TextField, rich text)
  - status (CharField: draft, review, published, archived)
  - publish_date (DateTimeField, nullable, indexed)
  - author (ForeignKey to User, nullable)
  - ai_generated (BooleanField)
  - llm_used (CharField, nullable)
  - prompt_ref (ForeignKey to PromptLog, nullable)
  - generation_metadata (JSONField, nullable)
  - source_opportunities (ManyToManyField to ScrapedOpportunity)
  - topics (ManyToManyField to Topic)
  - seo_title, meta_description (CharField, nullable)
  - featured_image (ImageField, nullable)
  - created_at, updated_at
- PromptLog model fields:
  - prompt_text (TextField)
  - response_text (TextField, nullable)
  - created_at (DateTimeField)
  - llm_used (CharField)
  - metadata (JSONField: tokens, cost, etc.)
- ContentRevision model fields:
  - article (ForeignKey to Article)
  - editor (ForeignKey to User)
  - timestamp (DateTimeField)
  - previous_body (TextField)
  - change_summary (CharField, nullable)
- Add indexes for performance
- Implement __str__ methods
- Add auto-slug generation using django-autoslug or custom save method

**Testing Requirements:**
- Run migrations
- Unit tests for all models
- Test relationships
- Test slug auto-generation
- Test revision tracking
- Run: `pytest apps/content/tests/test_models.py`

---

### EXT-018: Content Admin Interface
**Type:** Task
**Priority:** High
**Estimated Time:** 6 hours
**Dependencies:** EXT-017
**Phase:** Phase 1 - Week 5

**Description:**
Create customized Django admin interface for content models with rich text editor integration, review queue, custom actions, and revision history display.

**Acceptance Criteria:**
- [ ] Topic admin registered with custom configuration
- [ ] Article admin registered with CKEditor rich text editor
- [ ] PromptLog admin registered (read-only)
- [ ] ContentRevision displayed as inline in Article admin
- [ ] Review queue filter working (shows only articles with status='review')
- [ ] Custom actions implemented (Publish, Send to Review, Generate Draft)
- [ ] CKEditor integrated with full toolbar and image upload capability
- [ ] Revision history visible (shows all ContentRevision entries for each article)
- [ ] Admin interface user-friendly: all CRUD operations accessible within 2 clicks, clear field labels, helpful error messages

**Files to Create:**
- `apps/content/admin.py`
- `static/css/admin_custom.css` (optional)

**Files to Modify:**
- `extradime/settings/base.py` (add CKEditor configuration)
- `requirements.txt` (add django-ckeditor)

**Implementation Notes:**
- **Rich Text Editor Choice: CKEditor**
  - Rationale: Better Django integration via django-ckeditor package, extensive documentation, WYSIWYG editing, image upload support, widely used in Django projects
  - Alternative considered: TinyMCE (good but less Django-specific tooling)
- Install django-ckeditor: `pip install django-ckeditor django-ckeditor-5`
- Configure CKEditor in settings:
  ```python
  INSTALLED_APPS += ['ckeditor', 'ckeditor_uploader']
  CKEDITOR_UPLOAD_PATH = "uploads/"
  CKEDITOR_CONFIGS = {
      'default': {
          'toolbar': 'full',
          'height': 400,
          'width': '100%',
      },
  }
  ```
- Article admin:
  - Use CKEditorWidget for body field
  - list_display: title, status, author, ai_generated, publish_date, created_at
  - list_filter: status, ai_generated, topics, publish_date
  - search_fields: title, body
  - actions: publish_articles, send_to_review, generate_draft
  - inlines: ContentRevisionInline
  - readonly_fields: created_at, updated_at, generation_metadata
- Topic admin:
  - list_display: name, slug, created_at
  - prepopulated_fields: {'slug': ('name',)}
- PromptLog admin:
  - list_display: llm_used, created_at, truncated_prompt
  - readonly_fields: all fields
  - list_filter: llm_used, created_at

**Testing Requirements:**
- Access admin: http://localhost:8000/admin/content/
- Test rich text editor functionality
- Test review queue filter
- Test custom actions
- Create test article and verify all features
- Test revision history display

---

### EXT-019: Content Views and Templates
**Type:** Task
**Priority:** High
**Estimated Time:** 10 hours
**Dependencies:** EXT-017, EXT-004
**Phase:** Phase 1 - Week 5

**Description:**
Create views and templates for displaying articles, opportunities, and topics on the frontend. Implement list views, detail views, pagination, and filtering.

**Acceptance Criteria:**
- [ ] Article list view working
- [ ] Article detail view working
- [ ] Opportunity list view working
- [ ] Opportunity detail view working
- [ ] Topic list view working
- [ ] Topic-filtered article list working
- [ ] Pagination implemented
- [ ] SEO meta tags included
- [ ] Responsive design
- [ ] Templates extend base template

**Files to Create:**
- `apps/content/views.py`
- `apps/content/urls.py`
- `apps/content/templates/content/article_list.html`
- `apps/content/templates/content/article_detail.html`
- `apps/content/templates/content/opportunity_list.html`
- `apps/content/templates/content/opportunity_detail.html`
- `apps/content/templates/content/topic_list.html`

**Files to Modify:**
- `extradime/urls.py` (include content.urls)
- `apps/core/templates/core/base.html` (add navigation links)

**Implementation Notes:**
- Implement views:
  ```python
  class ArticleListView(ListView):
      model = Article
      queryset = Article.objects.filter(status='published').order_by('-publish_date')
      paginate_by = 10
      template_name = 'content/article_list.html'

  class ArticleDetailView(DetailView):
      model = Article
      queryset = Article.objects.filter(status='published')
      template_name = 'content/article_detail.html'

      def get_context_data(self, **kwargs):
          context = super().get_context_data(**kwargs)
          # Add related articles
          # Add source opportunities
          return context

  class OpportunityListView(ListView):
      model = ScrapedOpportunity
      queryset = ScrapedOpportunity.objects.filter(status='PROCESSED').order_by('-date_discovered')
      paginate_by = 20
      template_name = 'content/opportunity_list.html'

  class TopicArticleListView(ListView):
      model = Article
      template_name = 'content/article_list.html'
      paginate_by = 10

      def get_queryset(self):
          topic_slug = self.kwargs['slug']
          return Article.objects.filter(
              status='published',
              topics__slug=topic_slug
          ).order_by('-publish_date')
  ```
- URL patterns:
  - /articles/ → ArticleListView
  - /articles/<slug>/ → ArticleDetailView
  - /opportunities/ → OpportunityListView
  - /opportunities/<int:pk>/ → OpportunityDetailView
  - /topics/ → TopicListView
  - /topics/<slug>/ → TopicArticleListView
- Templates should include:
  - SEO meta tags (title, description, og:tags)
  - Structured data (JSON-LD)
  - Social sharing buttons
  - Related content
  - Breadcrumbs
- Use Bootstrap or Tailwind for styling

**Testing Requirements:**
- Access all views and verify rendering
- Test pagination
- Test topic filtering
- Test with no results
- Verify SEO meta tags in HTML
- Test responsive design
- Check HTML validation

---

### EXT-020: RSS Feed Implementation
**Type:** Task
**Priority:** Medium
**Estimated Time:** 4 hours
**Dependencies:** EXT-017
**Phase:** Phase 1 - Week 6

**Description:**
Implement RSS feeds for articles and topics using Django's syndication framework. Provide feeds for all articles, topic-specific articles, and optionally opportunities.

**Acceptance Criteria:**
- [ ] Main articles feed working
- [ ] Topic-specific feeds working
- [ ] Feed validates against RSS 2.0 spec
- [ ] Contains correct data (title, link, description, pubDate)
- [ ] Accessible at /feeds/articles/
- [ ] Feed autodiscovery meta tags in HTML
- [ ] Feed includes proper author information
- [ ] Feed includes enclosures for images

**Files to Create:**
- `apps/content/feeds.py`

**Files to Modify:**
- `apps/content/urls.py` (add feed URLs)
- `apps/core/templates/core/base.html` (add feed autodiscovery)

**Implementation Notes:**
- Implement feeds using django.contrib.syndication:
  ```python
  from django.contrib.syndication.views import Feed
  from django.utils.feedgenerator import Atom1Feed

  class ArticlesFeed(Feed):
      title = "Extradime.com - Latest Articles"
      link = "/articles/"
      description = "Latest articles on earning extra income online"

      def items(self):
          return Article.objects.filter(status='published').order_by('-publish_date')[:20]

      def item_title(self, item):
          return item.title

      def item_description(self, item):
          return item.meta_description or item.body[:200]

      def item_link(self, item):
          return f'/articles/{item.slug}/'

      def item_pubdate(self, item):
          return item.publish_date

      def item_author_name(self, item):
          return item.author.get_full_name() if item.author else "Extradime Team"

  class TopicFeed(Feed):
      def get_object(self, request, slug):
          return Topic.objects.get(slug=slug)

      def title(self, obj):
          return f"Extradime.com - {obj.name} Articles"

      def link(self, obj):
          return f'/topics/{obj.slug}/'

      def description(self, obj):
          return obj.description or f"Latest articles about {obj.name}"

      def items(self, obj):
          return Article.objects.filter(
              status='published',
              topics=obj
          ).order_by('-publish_date')[:20]
  ```
- URL patterns:
  - /feeds/articles/ → ArticlesFeed
  - /feeds/topics/<slug>/ → TopicFeed
- Add feed autodiscovery to base.html:
  ```html
  <link rel="alternate" type="application/rss+xml" title="Extradime Articles" href="{% url 'articles_feed' %}">
  ```

**Testing Requirements:**
- Access feed: http://localhost:8000/feeds/articles/
- Validate feed: https://validator.w3.org/feed/
- Test in feed reader (Feedly, etc.)
- Verify all fields present
- Test topic-specific feeds
- Check feed autodiscovery in browser

---

## Epic 1.4: AI Content Generation (Week 7-8)

### EXT-021: Prompt Templates Implementation
**Type:** Task
**Priority:** Critical
**Estimated Time:** 6 hours
**Dependencies:** EXT-017
**Phase:** Phase 1 - Week 7

**Description:**
Implement all AI prompt templates for article generation, content enhancement, and summarization. Create a centralized prompts module with all templates from PROMPT_TEMPLATES.md.

**Acceptance Criteria:**
- [ ] All article generation prompts implemented
- [ ] All content enhancement prompts implemented
- [ ] All prompts accept dynamic variables
- [ ] Prompts properly formatted with clear instructions
- [ ] Safety guidelines included in prompts
- [ ] Prompts tested manually with LLM
- [ ] Documentation for each prompt
- [ ] Unit tests for prompt formatting

**Files to Create:**
- `apps/content/prompts.py`
- `apps/content/tests/test_prompts.py`

**Implementation Notes:**
- Reference: docs/PROMPT_TEMPLATES.md for all prompt templates
- Implement prompt templates:
  ```python
  BEGINNERS_GUIDE_PROMPT = """
  You are an expert content writer for Extradime.com...

  **Opportunity Title:** {opportunity_title}
  **Description:** {opportunity_description}
  ...
  """

  OPPORTUNITY_REVIEW_PROMPT = """..."""
  COMPARISON_ARTICLE_PROMPT = """..."""
  WEEKLY_ROUNDUP_PROMPT = """..."""
  TITLE_GENERATION_PROMPT = """..."""
  META_DESCRIPTION_PROMPT = """..."""
  SUMMARIZATION_PROMPT = """..."""
  KEYWORD_EXTRACTION_PROMPT = """..."""

  def format_beginners_guide_prompt(opportunity):
      """Format beginner's guide prompt with opportunity data."""
      return BEGINNERS_GUIDE_PROMPT.format(
          opportunity_title=opportunity.title,
          opportunity_description=opportunity.description,
          opportunity_url=opportunity.url,
          earnings_text=opportunity.potential_earnings_text or "Earnings vary",
          requirements_text=opportunity.requirements_text or "No specific requirements listed",
      )

  def format_review_prompt(opportunity, additional_context=""):
      """Format review prompt with opportunity data."""
      # Similar implementation

  # ... other formatting functions
  ```
- Validate all required variables present before formatting
- Add default values for optional variables
- Include comprehensive docstrings

**Testing Requirements:**
- Unit tests for each formatting function
- Test with missing optional variables
- Test with None values
- Manually test prompts with OpenAI/Anthropic
- Verify output quality
- Run: `pytest apps/content/tests/test_prompts.py`

---

### EXT-022: AI Utility Functions
**Type:** Task
**Priority:** Critical
**Estimated Time:** 8 hours
**Dependencies:** EXT-021
**Phase:** Phase 1 - Week 7

**Description:**
Create utility functions for calling LLM APIs (OpenAI, Anthropic), handling responses, error handling, token counting, cost tracking, and retry logic.

**Acceptance Criteria:**
- [ ] OpenAI API integration working
- [ ] Anthropic API integration working
- [ ] Error handling implemented
- [ ] Retry logic with exponential backoff
- [ ] Token counting working
- [ ] Cost tracking implemented
- [ ] Response validation
- [ ] Logging all API calls
- [ ] Unit tests passing

**Files to Create:**
- `apps/content/ai_utils.py`
- `apps/content/tests/test_ai_utils.py`

**Implementation Notes:**
- Implement AI utility functions:
  ```python
  import openai
  import anthropic
  from tenacity import retry, stop_after_attempt, wait_exponential

  def get_openai_client():
      """Get configured OpenAI client."""
      return openai.OpenAI(api_key=settings.OPENAI_API_KEY)

  def get_anthropic_client():
      """Get configured Anthropic client."""
      return anthropic.Anthropic(api_key=settings.ANTHROPIC_API_KEY)

  @retry(stop=stop_after_attempt(3), wait=wait_exponential(multiplier=1, min=4, max=10))
  def call_openai_api(prompt, model="gpt-4", max_tokens=2000, temperature=0.7):
      """Call OpenAI API with retry logic."""
      client = get_openai_client()
      try:
          response = client.chat.completions.create(
              model=model,
              messages=[{"role": "user", "content": prompt}],
              max_tokens=max_tokens,
              temperature=temperature,
          )
          content = response.choices[0].message.content
          tokens_used = response.usage.total_tokens
          cost = calculate_openai_cost(model, tokens_used)

          return {
              'content': content,
              'tokens': tokens_used,
              'cost': cost,
              'model': model,
          }
      except Exception as e:
          logger.error(f"OpenAI API error: {e}")
          raise

  @retry(stop=stop_after_attempt(3), wait=wait_exponential(multiplier=1, min=4, max=10))
  def call_anthropic_api(prompt, model="claude-3-sonnet-20240229", max_tokens=2000):
      """Call Anthropic API with retry logic."""
      client = get_anthropic_client()
      try:
          response = client.messages.create(
              model=model,
              max_tokens=max_tokens,
              messages=[{"role": "user", "content": prompt}]
          )
          content = response.content[0].text
          tokens_used = response.usage.input_tokens + response.usage.output_tokens
          cost = calculate_anthropic_cost(model, response.usage.input_tokens, response.usage.output_tokens)

          return {
              'content': content,
              'tokens': tokens_used,
              'cost': cost,
              'model': model,
          }
      except Exception as e:
          logger.error(f"Anthropic API error: {e}")
          raise

  def calculate_openai_cost(model, tokens):
      """Calculate cost for OpenAI API call."""
      # GPT-4: $0.03/1K input tokens, $0.06/1K output tokens (approximate)
      # Simplified calculation
      cost_per_1k = 0.045  # Average
      return (tokens / 1000) * cost_per_1k

  def calculate_anthropic_cost(model, input_tokens, output_tokens):
      """Calculate cost for Anthropic API call."""
      # Claude 3 Sonnet: $0.003/1K input, $0.015/1K output
      input_cost = (input_tokens / 1000) * 0.003
      output_cost = (output_tokens / 1000) * 0.015
      return input_cost + output_cost

  def count_tokens(text, model="gpt-4"):
      """Count tokens in text using tiktoken."""
      import tiktoken
      encoding = tiktoken.encoding_for_model(model)
      return len(encoding.encode(text))

  def validate_response(response_text, min_length=100):
      """Validate LLM response."""
      if not response_text or len(response_text) < min_length:
          raise ValueError("Response too short or empty")
      return True
  ```
- Use tenacity library for retry logic
- Log all API calls with prompt, response, tokens, cost
- Handle rate limiting errors
- Implement circuit breaker pattern for repeated failures

**Testing Requirements:**
- Unit tests with mocked API responses
- Test error handling
- Test retry logic
- Test token counting
- Test cost calculation
- Integration test with real API (optional, use VCR.py to record)
- Run: `pytest apps/content/tests/test_ai_utils.py`

---

### EXT-023: Article Generation Tasks
**Type:** Task
**Priority:** Critical
**Estimated Time:** 10 hours
**Dependencies:** EXT-022
**Phase:** Phase 1 - Week 7

**Description:**
Create Celery tasks for generating article drafts from opportunities, batch generation, and article regeneration. Implement workflow logic for auto-creation with manual review.

**Acceptance Criteria:**
- [ ] generate_article_draft_task implemented
- [ ] batch_generate_articles_task implemented
- [ ] regenerate_article_task implemented
- [ ] Articles saved with 'review' status
- [ ] PromptLog created for each generation
- [ ] Metadata stored correctly (tokens, cost, model)
- [ ] Source opportunities linked to articles
- [ ] Error handling and retry logic
- [ ] Unit tests passing
- [ ] Integration tests passing

**Files to Create:**
- `apps/content/tasks.py`
- `apps/content/tests/test_tasks.py`

**Implementation Notes:**
- Implement Celery tasks:
  ```python
  from celery import shared_task
  from apps.content.prompts import format_beginners_guide_prompt
  from apps.content.ai_utils import call_openai_api, call_anthropic_api
  from apps.content.models import Article, PromptLog
  from apps.scraping.models import ScrapedOpportunity

  @shared_task(bind=True, max_retries=3)
  def generate_article_draft_task(self, opportunity_id, workflow='review', llm='openai'):
      """Generate article draft from opportunity."""
      try:
          # Get opportunity
          opportunity = ScrapedOpportunity.objects.get(id=opportunity_id)

          # Format prompt
          prompt = format_beginners_guide_prompt(opportunity)

          # Call LLM
          if llm == 'openai':
              result = call_openai_api(prompt, model=settings.OPENAI_MODEL)
          else:
              result = call_anthropic_api(prompt, model=settings.ANTHROPIC_MODEL)

          # Create PromptLog
          prompt_log = PromptLog.objects.create(
              prompt_text=prompt,
              response_text=result['content'],
              llm_used=result['model'],
              metadata={
                  'tokens': result['tokens'],
                  'cost': result['cost'],
              }
          )

          # Generate title and meta description
          title = generate_title_from_content(result['content'])
          meta_desc = generate_meta_description(result['content'], title)

          # Create Article
          article = Article.objects.create(
              title=title,
              body=result['content'],
              status='review' if workflow == 'review' else 'published',
              ai_generated=True,
              llm_used=result['model'],
              prompt_ref=prompt_log,
              generation_metadata={
                  'tokens': result['tokens'],
                  'cost': result['cost'],
                  'workflow': workflow,
              },
              seo_title=title,
              meta_description=meta_desc,
          )

          # Link source opportunity
          article.source_opportunities.add(opportunity)

          # Mark opportunity as used
          opportunity.mark_used_in_content()

          logger.info(f"Generated article {article.id} from opportunity {opportunity_id}")
          return article.id

      except Exception as e:
          logger.error(f"Error generating article: {e}")
          self.retry(exc=e, countdown=60 * (2 ** self.request.retries))

  @shared_task
  def batch_generate_articles(opportunity_ids, workflow='review', llm='openai'):
      """Generate articles for multiple opportunities."""
      results = []
      for opp_id in opportunity_ids:
          result = generate_article_draft_task.delay(opp_id, workflow, llm)
          results.append(result.id)
      return results

  @shared_task
  def regenerate_article_task(article_id, llm=None):
      """Regenerate an existing article."""
      article = Article.objects.get(id=article_id)
      # Get original opportunity
      opportunity = article.source_opportunities.first()
      if not opportunity:
          raise ValueError("No source opportunity found")

      # Use same LLM or specified one
      llm = llm or article.llm_used or 'openai'

      # Generate new version
      new_article_id = generate_article_draft_task.delay(opportunity.id, 'review', llm)

      # Archive old article
      article.status = 'archived'
      article.save()

      return new_article_id

  def generate_title_from_content(content):
      """
      Generate SEO-optimized title from article content using LLM.

      Uses the TITLE_GENERATION_PROMPT from prompts.py to create
      an engaging, keyword-rich title under 60 characters.

      Args:
          content (str): Full article content

      Returns:
          str: Generated title
      """
      from apps.content.prompts import TITLE_GENERATION_PROMPT
      from django.conf import settings

      try:
          # Truncate content to first 1000 characters for context
          content_preview = content[:1000] if len(content) > 1000 else content

          # Format prompt with content
          prompt = TITLE_GENERATION_PROMPT.format(content=content_preview)

          # Call LLM with shorter max_tokens for title
          result = call_openai_api(
              prompt,
              model=settings.OPENAI_MODEL,
              max_tokens=100,
              temperature=0.7
          )

          # Extract and clean title
          title = result['content'].strip()

          # Remove quotes if LLM added them
          title = title.strip('"\'')

          # Truncate to 60 characters for SEO
          if len(title) > 60:
              title = title[:57] + '...'

          logger.info(f"Generated title: {title}")
          return title

      except Exception as e:
          logger.error(f"Error generating title: {e}")
          # Fallback to first sentence or truncated content
          fallback = content.split('.')[0][:60]
          return fallback if fallback else "Untitled Article"

  def generate_meta_description(content, title):
      """
      Generate SEO-optimized meta description from content.

      Uses the META_DESCRIPTION_PROMPT from prompts.py to create
      a compelling description under 160 characters.

      Args:
          content (str): Full article content
          title (str): Article title for context

      Returns:
          str: Generated meta description
      """
      from apps.content.prompts import META_DESCRIPTION_PROMPT
      from django.conf import settings

      try:
          # Truncate content to first 1000 characters for context
          content_preview = content[:1000] if len(content) > 1000 else content

          # Format prompt with content and title
          prompt = META_DESCRIPTION_PROMPT.format(
              title=title,
              content=content_preview
          )

          # Call LLM with shorter max_tokens for description
          result = call_openai_api(
              prompt,
              model=settings.OPENAI_MODEL,
              max_tokens=150,
              temperature=0.7
          )

          # Extract and clean description
          description = result['content'].strip()

          # Remove quotes if LLM added them
          description = description.strip('"\'')

          # Truncate to 160 characters for SEO
          if len(description) > 160:
              description = description[:157] + '...'

          logger.info(f"Generated meta description: {description}")
          return description

      except Exception as e:
          logger.error(f"Error generating meta description: {e}")
          # Fallback to first sentence or truncated content
          fallback = content.split('.')[0][:160]
          return fallback if fallback else title
  ```

- **Required Prompts** (defined in apps/content/prompts.py from EXT-021):
  - `TITLE_GENERATION_PROMPT`: Template for generating article titles
  - `META_DESCRIPTION_PROMPT`: Template for generating meta descriptions
  - These prompts should be imported from PROMPT_TEMPLATES.md

- Add task to Celery Beat for scheduled generation (optional)
- Implement quality checks before saving (minimum length, keyword presence)
- Add notification for review queue (email or admin notification)

**Testing Requirements:**
- Unit tests with mocked LLM calls
- Test all workflows (review, published)
- Test error handling
- Test batch generation
- Integration test with real LLM (optional)
- Verify article created correctly
- Verify PromptLog created
- Run: `pytest apps/content/tests/test_tasks.py`

---

### EXT-024: Content Generation Admin Actions
**Type:** Task
**Priority:** High
**Estimated Time:** 4 hours
**Dependencies:** EXT-023, EXT-018
**Phase:** Phase 1 - Week 8

**Description:**
Add custom admin actions for generating article drafts from opportunities, batch generation, and triggering regeneration. Integrate with the admin interface for easy content creation.

**Acceptance Criteria:**
- [ ] "Generate Article Draft" action in ScrapedOpportunity admin
- [ ] "Batch Generate Articles" action in ScrapedOpportunity admin
- [ ] "Regenerate Article" action in Article admin
- [ ] Actions trigger Celery tasks
- [ ] Success/error messages displayed
- [ ] Task status visible in admin
- [ ] Can select LLM (OpenAI/Anthropic) in action
- [ ] Actions respect permissions

**Files to Modify:**
- `apps/scraping/admin.py`
- `apps/content/admin.py`

**Implementation Notes:**
- Add admin actions to ScrapedOpportunity admin:
  ```python
  from apps.content.tasks import generate_article_draft_task, batch_generate_articles

  @admin.action(description='Generate article draft (OpenAI)')
  def generate_article_openai(modeladmin, request, queryset):
      """Generate article drafts using OpenAI."""
      opportunity_ids = list(queryset.values_list('id', flat=True))
      batch_generate_articles.delay(opportunity_ids, workflow='review', llm='openai')
      modeladmin.message_user(
          request,
          f"Queued {len(opportunity_ids)} articles for generation using OpenAI.",
          messages.SUCCESS
      )

  @admin.action(description='Generate article draft (Anthropic)')
  def generate_article_anthropic(modeladmin, request, queryset):
      """Generate article drafts using Anthropic."""
      opportunity_ids = list(queryset.values_list('id', flat=True))
      batch_generate_articles.delay(opportunity_ids, workflow='review', llm='anthropic')
      modeladmin.message_user(
          request,
          f"Queued {len(opportunity_ids)} articles for generation using Anthropic.",
          messages.SUCCESS
      )

  class ScrapedOpportunityAdmin(admin.ModelAdmin):
      actions = [generate_article_openai, generate_article_anthropic, ...]
  ```
- Add admin actions to Article admin:
  ```python
  @admin.action(description='Regenerate article')
  def regenerate_article(modeladmin, request, queryset):
      """Regenerate selected articles."""
      for article in queryset:
          regenerate_article_task.delay(article.id)
      modeladmin.message_user(
          request,
          f"Queued {queryset.count()} articles for regeneration.",
          messages.SUCCESS
      )

  class ArticleAdmin(admin.ModelAdmin):
      actions = [regenerate_article, ...]
  ```
- Add task status display (optional, using django-celery-results)
- Add permission checks

**Testing Requirements:**
- Test actions in admin interface
- Verify tasks queued correctly
- Check success messages
- Test with multiple selections
- Verify permissions work
- Check Celery logs for task execution

---

### EXT-025: Review Queue Dashboard
**Type:** Task
**Priority:** Medium
**Estimated Time:** 6 hours
**Dependencies:** EXT-018, EXT-023
**Phase:** Phase 1 - Week 8

**Description:**
Create a dedicated review queue dashboard for editors to efficiently review AI-generated articles. Include filtering, sorting, preview, and quick actions.

**Acceptance Criteria:**
- [ ] Review queue page accessible
- [ ] Shows all articles with status='review'
- [ ] Filtering by topic, date, LLM used
- [ ] Sorting by date, quality score
- [ ] Preview of article content
- [ ] Quick actions (Approve, Edit, Reject)
- [ ] Statistics displayed (pending count, avg review time)
- [ ] Responsive design
- [ ] Only accessible to editors

**Files to Create:**
- `apps/content/views.py` (add ReviewQueueView)
- `apps/content/templates/content/review_queue.html`
- `apps/content/urls.py` (add review queue URL)

**Files to Modify:**
- `apps/core/templates/core/base.html` (add review queue link in nav)

**Implementation Notes:**
- Implement ReviewQueueView:
  ```python
  from django.contrib.auth.mixins import PermissionRequiredMixin

  class ReviewQueueView(PermissionRequiredMixin, ListView):
      model = Article
      template_name = 'content/review_queue.html'
      permission_required = 'content.change_article'
      paginate_by = 20

      def get_queryset(self):
          qs = Article.objects.filter(status='review').select_related('prompt_ref').prefetch_related('topics', 'source_opportunities')

          # Apply filters
          topic = self.request.GET.get('topic')
          if topic:
              qs = qs.filter(topics__slug=topic)

          llm = self.request.GET.get('llm')
          if llm:
              qs = qs.filter(llm_used=llm)

          # Apply sorting
          sort = self.request.GET.get('sort', '-created_at')
          qs = qs.order_by(sort)

          return qs

      def get_context_data(self, **kwargs):
          context = super().get_context_data(**kwargs)
          context['pending_count'] = Article.objects.filter(status='review').count()
          context['topics'] = Topic.objects.all()
          return context
  ```
- Template should include:
  - Filter form (topic, LLM, date range)
  - Sort options
  - Article cards with preview
  - Quick action buttons
  - Statistics panel
- Quick actions should use HTMX or AJAX for smooth UX
- Add permission checks

**Testing Requirements:**
- Access review queue as editor
- Test all filters
- Test sorting
- Test quick actions
- Verify permissions (non-editors can't access)
- Test responsive design

---

### EXT-026: Testing Infrastructure Setup
**Type:** Task
**Priority:** High
**Estimated Time:** 6 hours
**Dependencies:** EXT-001
**Phase:** Phase 1 - Week 8

**Description:**
Set up comprehensive testing infrastructure with pytest, pytest-django, factories, fixtures, and coverage reporting. Configure test settings and create base test classes.

**Acceptance Criteria:**
- [ ] pytest and pytest-django configured
- [ ] Test settings file created
- [ ] Factory Boy factories created for all models
- [ ] Base test classes created
- [ ] Fixtures created for common test data
- [ ] Coverage reporting configured
- [ ] Can run all tests successfully
- [ ] Coverage report generated

**Files to Create:**
- `pytest.ini`
- `conftest.py`
- `apps/scraping/tests/factories.py`
- `apps/content/tests/factories.py`
- `apps/core/tests/test_base.py`

**Files to Modify:**
- `extradime/settings/test.py`
- `requirements-dev.txt` (add testing dependencies)

**Implementation Notes:**
- Configure pytest.ini:
  ```ini
  [pytest]
  DJANGO_SETTINGS_MODULE = extradime.settings.test
  python_files = tests.py test_*.py *_tests.py
  addopts = --cov=apps --cov-report=html --cov-report=term-missing
  ```
- Test settings should:
  - Use in-memory SQLite database
  - Disable migrations (use --reuse-db)
  - Set DEBUG=False
  - Use fast password hasher
  - Disable Celery (CELERY_TASK_ALWAYS_EAGER=True)
- Create factories using Factory Boy:
  ```python
  import factory
  from apps.scraping.models import DataSource, ScrapedOpportunity

  class DataSourceFactory(factory.django.DjangoModelFactory):
      class Meta:
          model = DataSource

      name = factory.Faker('company')
      url = factory.Faker('url')
      source_type = 'RSS'
      is_active = True

  class ScrapedOpportunityFactory(factory.django.DjangoModelFactory):
      class Meta:
          model = ScrapedOpportunity

      title = factory.Faker('sentence')
      description = factory.Faker('paragraph')
      url = factory.Faker('url')
      source = factory.SubFactory(DataSourceFactory)
      status = 'NEW'
  ```
- Create base test classes with common setup/teardown
- Add fixtures for common test data

**Testing Requirements:**
- Run all tests: `pytest`
- Generate coverage report: `pytest --cov=apps --cov-report=html`
- Verify coverage > 80%
- Check coverage report: `open htmlcov/index.html`

---

### EXT-027: Phase 1 Integration Testing
**Type:** Task
**Priority:** High
**Estimated Time:** 8 hours
**Dependencies:** EXT-026, EXT-009, EXT-017, EXT-023
**Phase:** Phase 1 - Week 8

**Description:**
Create comprehensive integration tests for Phase 1 functionality: scraping workflow, content generation workflow, and end-to-end article creation from opportunity discovery to publication.

**Acceptance Criteria:**
- [ ] Scraping workflow integration test
- [ ] Content generation workflow integration test
- [ ] End-to-end test (scrape → generate → review → publish)
- [ ] Admin interface integration tests
- [ ] API integration tests (if API exists)
- [ ] All tests passing
- [ ] Test coverage > 80%

**Files to Create:**
- `apps/scraping/tests/test_integration.py`
- `apps/content/tests/test_integration.py`
- `tests/test_e2e.py`

**Implementation Notes:**
- Scraping workflow test:
  ```python
  @pytest.mark.django_db
  def test_scraping_workflow():
      # Create DataSource
      source = DataSourceFactory(source_type='RSS', feed_url='https://example.com/feed.xml')

      # Run spider task (mocked)
      with patch('apps.scraping.tasks.run_spider') as mock_spider:
          mock_spider.return_value = {'items_scraped': 5}
          run_spider_task(spider_name='rss', source_id=source.id)

      # Verify opportunities created
      assert ScrapedOpportunity.objects.filter(source=source).count() == 5

      # Verify DataSource updated
      source.refresh_from_database()
      assert source.last_checked is not None
      assert source.total_opportunities_found == 5
  ```
- Content generation workflow test:
  ```python
  @pytest.mark.django_db
  def test_content_generation_workflow():
      # Create opportunity
      opportunity = ScrapedOpportunityFactory()

      # Generate article (mocked LLM)
      with patch('apps.content.ai_utils.call_openai_api') as mock_llm:
          mock_llm.return_value = {
              'content': 'Generated article content...',
              'tokens': 1500,
              'cost': 0.045,
              'model': 'gpt-4',
          }
          article_id = generate_article_draft_task(opportunity.id, workflow='review')

      # Verify article created
      article = Article.objects.get(id=article_id)
      assert article.status == 'review'
      assert article.ai_generated is True
      assert article.source_opportunities.filter(id=opportunity.id).exists()

      # Verify PromptLog created
      assert article.prompt_ref is not None
      assert article.prompt_ref.llm_used == 'gpt-4'

      # Verify opportunity marked as used
      opportunity.refresh_from_database()
      assert opportunity.status == 'USED_IN_CONTENT'
  ```
- End-to-end test:
  ```python
  @pytest.mark.django_db
  @pytest.mark.integration
  def test_end_to_end_article_creation():
      # 1. Create and scrape source
      source = DataSourceFactory()
      # ... scrape and create opportunities

      # 2. Generate article from opportunity
      # ... generate article

      # 3. Review and publish
      article = Article.objects.get(status='review')
      article.status = 'published'
      article.publish_date = timezone.now()
      article.save()

      # 4. Verify article accessible on frontend
      response = client.get(f'/articles/{article.slug}/')
      assert response.status_code == 200
      assert article.title in response.content.decode()

      # 5. Verify RSS feed includes article
      response = client.get('/feeds/articles/')
      assert response.status_code == 200
      assert article.title in response.content.decode()
  ```

**Testing Requirements:**
- Run integration tests: `pytest -m integration`
- Run all tests: `pytest`
- Verify all workflows work end-to-end
- Check test coverage
- Fix any failing tests

---

### EXT-028: Documentation and README
**Type:** Task
**Priority:** Medium
**Estimated Time:** 4 hours
**Dependencies:** EXT-027
**Phase:** Phase 1 - Week 8

**Description:**
Create comprehensive project documentation including README, setup guide, API documentation, and developer guide. Document all Phase 1 features and how to use them.

**Acceptance Criteria:**
- [ ] README.md updated with project overview
- [ ] Setup guide complete
- [ ] API documentation created (if API exists)
- [ ] Developer guide created
- [ ] All environment variables documented
- [ ] All admin features documented
- [ ] Troubleshooting guide included
- [ ] Contributing guidelines added

**Files to Create/Modify:**
- `README.md`
- `docs/SETUP.md`
- `docs/API.md`
- `docs/DEVELOPER_GUIDE.md`
- `docs/TROUBLESHOOTING.md`
- `CONTRIBUTING.md`

**Implementation Notes:**
- README should include:
  - Project description
  - Features list
  - Tech stack
  - Quick start
  - Links to detailed docs
  - License
  - Contact info
- Setup guide should include:
  - Prerequisites
  - Installation steps
  - Database setup
  - Environment configuration
  - Running the application
  - Running tests
- Developer guide should include:
  - Project structure
  - Code style guidelines
  - Testing guidelines
  - Git workflow
  - How to add new features
- Document all admin actions and workflows
- Include screenshots where helpful

**Testing Requirements:**
- Follow setup guide on fresh machine
- Verify all commands work
- Check all links
- Proofread all documentation

---

# Phase 2: User & Community Features (Weeks 9-16)

## Epic 2.1: User Management (Week 9-10)

### EXT-029: User Models and Authentication
**Type:** Story
**Priority:** High
**Estimated Time:** 12 hours
**Dependencies:** EXT-002
**Phase:** Phase 2 - Week 9

**Description:**
Create custom user model with profile, implement authentication system (registration, login, logout, password reset), and set up user permissions.

**Acceptance Criteria:**
- [ ] Custom User model created
- [ ] UserProfile model created
- [ ] Registration working
- [ ] Login/logout working
- [ ] Password reset working
- [ ] Email verification implemented
- [ ] User permissions configured
- [ ] Unit tests passing

**Files to Create:**
- `apps/users/__init__.py`
- `apps/users/models.py`
- `apps/users/forms.py`
- `apps/users/views.py`
- `apps/users/urls.py`
- `apps/users/admin.py`
- `apps/users/templates/users/*.html`
- `apps/users/tests/test_models.py`
- `apps/users/tests/test_views.py`

**Implementation Notes:**
- Extend Django's AbstractUser or AbstractBaseUser
- UserProfile fields: bio, avatar, location, website, social_links, email_preferences
- Use Django's built-in authentication views where possible
- Implement email verification with tokens
- Configure permissions for content creation, moderation

**Testing Requirements:**
- Test registration flow
- Test login/logout
- Test password reset
- Test email verification
- Test permissions

---

### EXT-030: User Profile Pages
**Type:** Task
**Priority:** Medium
**Estimated Time:** 8 hours
**Dependencies:** EXT-029
**Phase:** Phase 2 - Week 9

**Description:**
Create user profile pages with view and edit functionality, activity history, and user statistics.

**Acceptance Criteria:**
- [ ] Profile view page working
- [ ] Profile edit page working
- [ ] Avatar upload working
- [ ] Activity history displayed
- [ ] User statistics shown
- [ ] Privacy settings implemented
- [ ] Responsive design

**Files to Create:**
- `apps/users/templates/users/profile.html`
- `apps/users/templates/users/profile_edit.html`

**Implementation Notes:**
- Display user's articles, forum posts, comments
- Show statistics: join date, posts count, reputation
- Allow editing profile fields
- Implement avatar upload with image processing (Pillow)
- Add privacy settings (public/private profile)

**Testing Requirements:**
- Test profile view
- Test profile edit
- Test avatar upload
- Test privacy settings

---

## Epic 2.2: Forum Integration (Week 11-12)

### EXT-031: Forum Package Evaluation and Installation
**Type:** Task
**Priority:** High
**Estimated Time:** 8 hours
**Dependencies:** EXT-029
**Phase:** Phase 2 - Week 11

**Description:**
Evaluate forum packages (django-machina, custom build), select best option, install and configure, and integrate with user system.

**Acceptance Criteria:**
- [ ] Forum package evaluated
- [ ] Package installed and configured
- [ ] Integrated with User model
- [ ] Basic forum structure created
- [ ] Can create forums and topics
- [ ] Can post and reply
- [ ] Permissions configured

**Files to Create/Modify:**
- Depends on package chosen
- Configuration in settings
- URL routing

**Implementation Notes:**
- Evaluate django-machina vs custom build
- Consider: features, maintenance, customization, performance
- If using django-machina:
  - Install: `pip install django-machina`
  - Configure in settings
  - Run migrations
  - Customize templates
- Create initial forum structure (categories, forums)

**Testing Requirements:**
- Test forum creation
- Test topic creation
- Test posting
- Test permissions

---

### EXT-032: AI Avatar Models and Personas
**Type:** Story
**Priority:** High
**Estimated Time:** 10 hours
**Dependencies:** EXT-031
**Phase:** Phase 2 - Week 12

**Description:**
Create AIAvatarProfile model, implement persona prompts, and create system for AI avatars to participate in forum discussions.

**Acceptance Criteria:**
- [ ] AIAvatarProfile model created
- [ ] Persona prompts implemented
- [ ] Can create AI avatar profiles
- [ ] AI avatars can post in forums
- [ ] Responses stay in character
- [ ] AI avatar posts clearly marked
- [ ] Unit tests passing

**Files to Create:**
- `apps/community/__init__.py`
- `apps/community/models.py`
- `apps/community/avatar_prompts.py`
- `apps/community/tasks.py`
- `apps/community/tests/test_models.py`

**Implementation Notes:**
- Reference: docs/PROMPT_TEMPLATES.md Section 3 for persona prompts
- AIAvatarProfile fields:
  - name, bio, avatar_image, persona_prompt
  - expertise_areas, personality_traits
  - is_active, response_frequency
- Implement personas: Freelance Expert, Side Hustle Enthusiast, Passive Income Strategist
- Create task for AI avatar to respond to forum posts
- Mark AI posts with special badge/indicator

**Testing Requirements:**
- Test AI avatar creation
- Test persona prompt formatting
- Test AI response generation
- Test forum integration

---

## Epic 2.3: Content Moderation (Week 13-14)

### EXT-033: Moderation Configuration and Models
**Type:** Task
**Priority:** High
**Estimated Time:** 6 hours
**Dependencies:** EXT-031
**Phase:** Phase 2 - Week 13

**Description:**
Create moderation models, configure moderation thresholds, and implement moderation workflow.

**Acceptance Criteria:**
- [ ] ModerationLog model created
- [ ] Moderation thresholds configured
- [ ] Moderation workflow defined
- [ ] Can flag content for review
- [ ] Can approve/reject content
- [ ] Moderation queue working

**Files to Create:**
- `apps/community/models.py` (add ModerationLog)
- `apps/community/moderation_config.py`
- `apps/community/moderation.py`

**Implementation Notes:**
- ModerationLog fields:
  - content_type, object_id, moderator, action, reason, timestamp
- Configure thresholds:
  - Toxicity: 0.7 (auto-flag), 0.9 (auto-reject)
  - Spam: 0.8 (auto-flag)
  - Profanity: 0.6 (auto-flag)
- Implement moderation actions: approve, reject, flag, ban_user

**Testing Requirements:**
- Test moderation log creation
- Test threshold configuration
- Test moderation actions

---

### EXT-034: Perspective API Integration
**Type:** Task
**Priority:** High
**Estimated Time:** 8 hours
**Dependencies:** EXT-033
**Phase:** Phase 2 - Week 13

**Description:**
Integrate Google Perspective API for automated content moderation, implement scoring, and create moderation pipeline.

**Acceptance Criteria:**
- [ ] Perspective API integrated
- [ ] Can analyze content for toxicity
- [ ] Scoring working correctly
- [ ] Moderation pipeline implemented
- [ ] Auto-flagging working
- [ ] Error handling implemented
- [ ] Unit tests passing

**Files to Create:**
- `apps/community/perspective_api.py`
- `apps/community/tests/test_perspective.py`

**Implementation Notes:**
- Use google-api-python-client
- Implement functions:
  ```python
  def analyze_text(text):
      """Analyze text using Perspective API."""
      # Call API
      # Return scores for: TOXICITY, SEVERE_TOXICITY, IDENTITY_ATTACK, INSULT, PROFANITY, THREAT

  def should_flag(scores, thresholds):
      """Determine if content should be flagged."""
      # Compare scores to thresholds
      # Return True if any threshold exceeded

  def moderate_content(content):
      """Moderate content using Perspective API."""
      scores = analyze_text(content)
      if should_flag(scores, MODERATION_THRESHOLDS):
          # Flag for review
          # Create ModerationLog
      return scores
  ```
- Handle API errors and rate limits
- Cache results to avoid duplicate API calls

**Testing Requirements:**
- Test with mocked API responses
- Test threshold logic
- Test error handling
- Integration test with real API (optional)

---

### EXT-035: Automated Moderation Workflow
**Type:** Task
**Priority:** High
**Estimated Time:** 8 hours
**Dependencies:** EXT-034
**Phase:** Phase 2 - Week 14

**Description:**
Implement automated moderation workflow with signals, Celery tasks, and moderation queue for human review.

**Acceptance Criteria:**
- [ ] Content analyzed on creation
- [ ] Auto-flagging working
- [ ] Auto-rejection working (high scores)
- [ ] Moderation queue populated
- [ ] Moderators can review flagged content
- [ ] Signals implemented
- [ ] Celery tasks working

**Files to Create:**
- `apps/community/signals.py`
- `apps/community/tasks.py` (add moderation tasks)
- `apps/community/views.py` (add moderation queue view)
- `apps/community/templates/community/moderation_queue.html`

**Implementation Notes:**
- Implement post_save signal for forum posts:
  ```python
  @receiver(post_save, sender=ForumPost)
  def moderate_post(sender, instance, created, **kwargs):
      if created:
          moderate_content_task.delay(instance.id, 'forumpost')
  ```
- Implement Celery task:
  ```python
  @shared_task
  def moderate_content_task(object_id, content_type):
      # Get content
      # Analyze with Perspective API
      # Apply moderation rules
      # Create ModerationLog if flagged
      # Notify moderators if needed
  ```
- Create moderation queue view for moderators
- Implement moderation actions in admin

**Testing Requirements:**
- Test signal triggers
- Test moderation task
- Test auto-flagging
- Test moderation queue
- Test moderator actions

---

# Phase 3: Advanced Features (Weeks 17-24)

## Epic 3.1: Newsletter System (Week 17-18)

### EXT-036: Newsletter Models and Subscription
**Type:** Story
**Priority:** Medium
**Estimated Time:** 10 hours
**Dependencies:** EXT-029
**Phase:** Phase 3 - Week 17

**Description:**
Create newsletter subscription system with models, subscription management, preferences, and unsubscribe functionality.

**Acceptance Criteria:**
- [ ] Subscription model created
- [ ] NewsletterIssue model created
- [ ] Subscription form working
- [ ] Email verification for subscriptions
- [ ] Preference management working
- [ ] Unsubscribe working
- [ ] Double opt-in implemented

**Files to Create:**
- `apps/newsletter/__init__.py`
- `apps/newsletter/models.py`
- `apps/newsletter/forms.py`
- `apps/newsletter/views.py`
- `apps/newsletter/urls.py`
- `apps/newsletter/templates/newsletter/*.html`

**Implementation Notes:**
- Subscription model fields:
  - email, user (ForeignKey, nullable), is_active, subscribed_at
  - preferences (JSONField: topics, frequency)
  - verification_token, verified_at
- NewsletterIssue model fields:
  - title, content, sent_at, recipient_count
  - featured_articles (ManyToManyField)
- Implement double opt-in with email verification
- Allow preference management (topics, frequency)
- Implement one-click unsubscribe

**Testing Requirements:**
- Test subscription flow
- Test email verification
- Test preference management
- Test unsubscribe

---

### EXT-037: Newsletter Content Curation
**Type:** Task
**Priority:** Medium
**Estimated Time:** 8 hours
**Dependencies:** EXT-036
**Phase:** Phase 3 - Week 17

**Description:**
Implement automated content curation for newsletters using AI to select and summarize articles, identify trending topics, and create newsletter content.

**Acceptance Criteria:**
- [ ] Content curation logic implemented
- [ ] Can select featured articles
- [ ] Can identify trending topics
- [ ] Can generate newsletter summaries
- [ ] Curation task working
- [ ] Unit tests passing

**Files to Create:**
- `apps/newsletter/curation.py`
- `apps/newsletter/tasks.py`
- `apps/newsletter/tests/test_curation.py`

**Implementation Notes:**
- Implement curation functions:
  ```python
  def select_featured_articles(since_date, limit=5):
      """Select top articles based on engagement."""
      # Query articles published since date
      # Order by views, comments, etc.
      # Return top N articles

  def identify_trending_topics(since_date):
      """Identify trending topics from recent content."""
      # Analyze recent articles and opportunities
      # Count topic mentions
      # Return trending topics

  def generate_newsletter_content(articles, opportunities, topics):
      """Generate newsletter content using LLM."""
      # Format newsletter prompt
      # Call LLM
      # Return formatted content
  ```
- Use engagement metrics for article selection
- Use LLM for content summarization
- Reference: docs/PROMPT_TEMPLATES.md Section 4 for newsletter prompts

**Testing Requirements:**
- Test article selection
- Test topic identification
- Test content generation
- Test with various date ranges

---

### EXT-038: Newsletter Generation and Sending
**Type:** Task
**Priority:** Medium
**Estimated Time:** 10 hours
**Dependencies:** EXT-037
**Phase:** Phase 3 - Week 18

**Description:**
Implement newsletter generation, HTML email templates, sending via email service, and scheduling with Celery Beat.

**Acceptance Criteria:**
- [ ] Newsletter generation task working
- [ ] HTML email templates created
- [ ] Email sending working
- [ ] Personalization working
- [ ] Scheduled sending working
- [ ] Bounce/complaint handling
- [ ] Analytics tracking

**Files to Create:**
- `apps/newsletter/tasks.py` (add generation/sending tasks)
- `apps/newsletter/templates/newsletter/email_base.html`
- `apps/newsletter/templates/newsletter/weekly_digest.html`

**Implementation Notes:**
- Implement newsletter tasks:
  ```python
  @shared_task
  def generate_newsletter_task():
      """Generate newsletter content."""
      # Curate content
      # Generate newsletter
      # Create NewsletterIssue
      # Queue sending task

  @shared_task
  def send_newsletter_task(issue_id):
      """Send newsletter to all subscribers."""
      issue = NewsletterIssue.objects.get(id=issue_id)
      subscribers = Subscription.objects.filter(is_active=True, verified_at__isnull=False)

      for subscriber in subscribers:
          send_newsletter_email.delay(issue.id, subscriber.id)

  @shared_task
  def send_newsletter_email(issue_id, subscriber_id):
      """Send newsletter to individual subscriber."""
      # Get issue and subscriber
      # Personalize content
      # Send email
      # Track sending
  ```
- Use django-anymail for email sending
- Implement HTML email templates with inline CSS
- Add unsubscribe link to all emails
- Configure Celery Beat for weekly sending
- Implement webhook handlers for bounces/complaints

**Testing Requirements:**
- Test newsletter generation
- Test email sending (use Mailtrap for testing)
- Test personalization
- Test scheduled sending
- Test bounce handling

---

## Summary and Next Steps

### Phase 1 Tickets Summary
- **Total Tickets:** 28 (EXT-001 to EXT-028)
- **Total Estimated Time:** ~180 hours (~22.5 days)
- **Critical Path:** EXT-001 → EXT-002 → EXT-009 → EXT-017 → EXT-021 → EXT-022 → EXT-023

### Phase 2 Tickets Summary
- **Total Tickets:** 10 (EXT-029 to EXT-038)
- **Total Estimated Time:** ~88 hours (~11 days)

### Parallel Development Opportunities

**Week 1-2 (Foundation):**
- EXT-001, EXT-005, EXT-006 can start immediately
- EXT-003, EXT-004 can start after EXT-001
- EXT-002 independent of EXT-003/EXT-004

**Week 3-4 (Scraping):**
- EXT-010, EXT-011 can start after EXT-009
- EXT-012, EXT-013, EXT-014 can be developed in parallel after EXT-011
- EXT-016 independent, can start anytime after EXT-009

**Week 5-6 (Content):**
- EXT-018, EXT-019, EXT-020 can start after EXT-017
- All three can be developed in parallel

**Week 7-8 (AI Generation):**
- EXT-021, EXT-022 sequential
- EXT-024, EXT-025 can start after EXT-023
- EXT-026, EXT-027, EXT-028 can be developed in parallel

### Implementation Priority

**Must Have (Phase 1):**
- EXT-001 to EXT-023 (Core functionality)
- EXT-026, EXT-027 (Testing)

**Should Have (Phase 1):**
- EXT-024, EXT-025 (Enhanced UX)
- EXT-028 (Documentation)

**Nice to Have (Phase 1):**
- EXT-008 (Docker)
- EXT-020 (RSS Feeds)

**Phase 2 Priority:**
- EXT-029, EXT-030 (User system - required for community)
- EXT-031, EXT-032 (Forum - core feature)
- EXT-033, EXT-034, EXT-035 (Moderation - required for safety)

**Phase 3 Priority:**
- EXT-036, EXT-037, EXT-038 (Newsletter - engagement feature)

---

## Ticket Status Tracking

Use this section to track ticket completion:

### Phase 1 - Week 1-2: Foundation
- [ ] EXT-001: Django Project Initial Setup
- [ ] EXT-002: PostgreSQL Database Configuration
- [ ] EXT-003: Celery and Redis Setup
- [ ] EXT-004: Core App Setup
- [ ] EXT-005: Requirements and Dependencies Installation
- [ ] EXT-006: Environment Variables and Configuration
- [ ] EXT-007: Logging Configuration
- [ ] EXT-008: Docker Configuration (Optional)

### Phase 1 - Week 3-4: Scraping Infrastructure
- [ ] EXT-009: Scraping App Models
- [ ] EXT-010: Scraping Admin Interface
- [ ] EXT-011: Scrapy Project Setup
- [ ] EXT-012: Base Spider Implementation
- [ ] EXT-013: RSS Feed Spider
- [ ] EXT-014: Website Spider Template
- [ ] EXT-015: Scraping Celery Tasks
- [ ] EXT-016: Scraping Utilities and Helpers

### Phase 1 - Week 5-6: Content Management
- [ ] EXT-017: Content App Models
- [ ] EXT-018: Content Admin Interface
- [ ] EXT-019: Content Views and Templates
- [ ] EXT-020: RSS Feed Implementation

### Phase 1 - Week 7-8: AI Content Generation
- [ ] EXT-021: Prompt Templates Implementation
- [ ] EXT-022: AI Utility Functions
- [ ] EXT-023: Article Generation Tasks
- [ ] EXT-024: Content Generation Admin Actions
- [ ] EXT-025: Review Queue Dashboard
- [ ] EXT-026: Testing Infrastructure Setup
- [ ] EXT-027: Phase 1 Integration Testing
- [ ] EXT-028: Documentation and README

### Phase 2 - Week 9-10: User Management
- [ ] EXT-029: User Models and Authentication
- [ ] EXT-030: User Profile Pages

### Phase 2 - Week 11-12: Forum Integration
- [ ] EXT-031: Forum Package Evaluation and Installation
- [ ] EXT-032: AI Avatar Models and Personas

### Phase 2 - Week 13-14: Content Moderation
- [ ] EXT-033: Moderation Configuration and Models
- [ ] EXT-034: Perspective API Integration
- [ ] EXT-035: Automated Moderation Workflow

### Phase 3 - Week 17-18: Newsletter System
- [ ] EXT-036: Newsletter Models and Subscription
- [ ] EXT-037: Newsletter Content Curation
- [ ] EXT-038: Newsletter Generation and Sending

---

**End of Enhanced Tickets Document**

**Total Tickets Created:** 38
**Total Estimated Time:** ~268 hours (~33.5 days of full-time development)
**Phases Covered:** Phase 1 (complete), Phase 2 (partial), Phase 3 (partial)

**Next Steps:**
1. Review and prioritize tickets
2. Assign tickets to sprints
3. Begin implementation with EXT-001
4. Track progress using the checklist above
5. Update ticket status as work progresses

### EXT-006: Environment Variables and Configuration
**Type:** Task  
**Priority:** High  
**Estimated Time:** 2 hours  
**Dependencies:** EXT-001  
**Phase:** Phase 1 - Week 1

**Description:**
Create comprehensive .env.example file with all required environment variables, set up environment variable loading in Django settings, and document all configuration options.

**Acceptance Criteria:**
- [ ] .env.example created with all variables
- [ ] All variables documented with comments
- [ ] Environment variable loading working in settings
- [ ] Sensitive values not committed to git
- [ ] .env added to .gitignore
- [ ] README updated with setup instructions
- [ ] Default values provided where appropriate

**Files to Create:**
- `.env.example`
- `.env` (local, not committed)

**Files to Modify:**
- `.gitignore` (add .env)
- `README.md` (add setup instructions)
- `extradime/settings/base.py` (configure env loading)

**Implementation Notes:**
- Reference: docs/implementation_specs.md Section 11.1 for complete .env.example
- Use python-decouple or django-environ
- Categories of variables:
  - Django settings (DEBUG, SECRET_KEY, ALLOWED_HOSTS)
  - Database configuration
  - Celery configuration
  - Redis configuration
  - API keys (OpenAI, Anthropic, Perspective)
  - Email configuration
  - AWS configuration (optional)
  - Scraping configuration
  - Feature flags
- Provide sensible defaults for development
- Document which variables are required vs optional

**Testing Requirements:**
- Verify all environment variables load correctly
- Test with missing optional variables (should use defaults)
- Test with missing required variables (should raise error)
- Verify sensitive values not in git: `git status`

---

### EXT-007: Logging Configuration
**Type:** Task  
**Priority:** Medium  
**Estimated Time:** 3 hours  
**Dependencies:** EXT-001  
**Phase:** Phase 1 - Week 2

**Description:**
Set up comprehensive logging configuration for Django, Celery, and Scrapy. Configure log levels, formatters, handlers, and log file rotation. Ensure proper logging for debugging and production monitoring.

**Acceptance Criteria:**
- [ ] Logging configured in Django settings
- [ ] Separate log files for Django, Celery, and Scrapy
- [ ] Log rotation configured
- [ ] Different log levels for dev/prod
- [ ] Console and file handlers working
- [ ] Structured logging format
- [ ] Error logs captured properly
- [ ] Log directory created automatically

**Files to Create:**
- `logs/.gitkeep`

**Files to Modify:**
- `extradime/settings/base.py` (add LOGGING configuration)
- `extradime/settings/development.py` (set DEBUG logging)
- `extradime/settings/production.py` (set INFO/WARNING logging)
- `.gitignore` (add logs/*.log)

**Implementation Notes:**
- Configure LOGGING in base.py:
  ```python
  LOGGING = {
      'version': 1,
      'disable_existing_loggers': False,
      'formatters': {
          'verbose': {
              'format': '{levelname} {asctime} {module} {message}',
              'style': '{',
          },
      },
      'handlers': {
          'file': {
              'level': 'INFO',
              'class': 'logging.handlers.RotatingFileHandler',
              'filename': 'logs/django.log',
              'maxBytes': 1024*1024*15,  # 15MB
              'backupCount': 10,
              'formatter': 'verbose',
          },
          'console': {
              'level': 'DEBUG',
              'class': 'logging.StreamHandler',
              'formatter': 'verbose',
          },
      },
      'loggers': {
          'django': {
              'handlers': ['file', 'console'],
              'level': 'INFO',
              'propagate': True,
          },
      },
  }
  ```
- Create logs directory: `mkdir -p logs`
- Add separate loggers for celery, scrapy, apps

**Testing Requirements:**
- Verify log files created in logs/ directory
- Test logging at different levels
- Verify log rotation works
- Check log format is readable
- Test console output in development

---


