# PART II: IMPLEMENTATION SPECIFICATIONS

> **This document provides concrete implementation details, code examples, and specifications to complement the original Technical Development Plan.**

---

## **10. Complete File and Directory Structure**

```
extradime_gemini/
├── .env.example                    # Environment variables template
├── .gitignore                      # Git ignore file
├── README.md                       # Project documentation
├── requirements.txt                # Python dependencies
├── manage.py                       # Django management script
├── pytest.ini                      # Pytest configuration
├── setup.cfg                       # Project configuration
├── Dockerfile                      # Docker container definition
├── docker-compose.yml              # Docker services configuration
├── .github/
│   └── workflows/
│       └── ci.yml                  # GitHub Actions CI/CD
│
├── extradime/                      # Main project directory
│   ├── __init__.py
│   ├── settings/
│   │   ├── __init__.py
│   │   ├── base.py                 # Base settings
│   │   ├── development.py          # Development settings
│   │   ├── production.py           # Production settings
│   │   └── test.py                 # Test settings
│   ├── urls.py                     # Main URL configuration
│   ├── wsgi.py                     # WSGI application
│   ├── asgi.py                     # ASGI application
│   └── celery.py                   # Celery configuration
│
├── apps/                           # Django applications
│   ├── __init__.py
│   │
│   ├── core/                       # Core functionality
│   │   ├── __init__.py
│   │   ├── models.py
│   │   ├── views.py
│   │   ├── urls.py
│   │   ├── utils.py
│   │   ├── middleware.py
│   │   ├── management/
│   │   │   └── commands/
│   │   │       └── init_data.py
│   │   ├── templates/
│   │   │   └── core/
│   │   │       ├── base.html
│   │   │       ├── home.html
│   │   │       └── about.html
│   │   └── tests/
│   │       ├── __init__.py
│   │       ├── test_views.py
│   │       └── test_utils.py
│   │
│   ├── users/                      # User management
│   │   ├── __init__.py
│   │   ├── models.py
│   │   ├── views.py
│   │   ├── urls.py
│   │   ├── forms.py
│   │   ├── admin.py
│   │   ├── signals.py
│   │   ├── templates/
│   │   │   └── users/
│   │   │       ├── login.html
│   │   │       ├── register.html
│   │   │       ├── profile.html
│   │   │       └── password_reset.html
│   │   └── tests/
│   │       ├── __init__.py
│   │       ├── test_models.py
│   │       ├── test_views.py
│   │       └── test_forms.py
│   │
│   ├── scraping/                   # Web scraping
│   │   ├── __init__.py
│   │   ├── models.py               # DataSource, ScrapedOpportunity
│   │   ├── admin.py
│   │   ├── tasks.py                # Celery tasks
│   │   ├── utils.py
│   │   ├── robots_checker.py       # robots.txt validation
│   │   ├── spiders/                # Scrapy spiders
│   │   │   ├── __init__.py
│   │   │   ├── base_spider.py
│   │   │   ├── rss_spider.py
│   │   │   ├── upwork_spider.py
│   │   │   ├── reddit_spider.py
│   │   │   └── freelancer_spider.py
│   │   ├── items.py                # Scrapy items
│   │   ├── pipelines.py            # Scrapy pipelines
│   │   ├── middlewares.py          # Scrapy middlewares
│   │   ├── settings.py             # Scrapy settings
│   │   ├── scrapy.cfg              # Scrapy configuration
│   │   └── tests/
│   │       ├── __init__.py
│   │       ├── test_models.py
│   │       ├── test_tasks.py
│   │       ├── test_spiders.py
│   │       └── fixtures/
│   │           └── sample_html.html
│   │
│   ├── content/                    # Content management
│   │   ├── __init__.py
│   │   ├── models.py               # Article, Topic, PromptLog, ContentRevision
│   │   ├── views.py
│   │   ├── urls.py
│   │   ├── admin.py
│   │   ├── forms.py
│   │   ├── tasks.py                # AI generation tasks
│   │   ├── prompts.py              # LLM prompt templates
│   │   ├── ai_utils.py             # AI helper functions
│   │   ├── feeds.py                # RSS feed classes
│   │   ├── templates/
│   │   │   └── content/
│   │   │       ├── article_list.html
│   │   │       ├── article_detail.html
│   │   │       ├── opportunity_list.html
│   │   │       ├── opportunity_detail.html
│   │   │       └── topic_list.html
│   │   └── tests/
│   │       ├── __init__.py
│   │       ├── test_models.py
│   │       ├── test_views.py
│   │       ├── test_tasks.py
│   │       └── test_prompts.py
│   │
│   ├── community/                  # Forum and community
│   │   ├── __init__.py
│   │   ├── models.py               # AIAvatarProfile, custom forum models
│   │   ├── views.py
│   │   ├── urls.py
│   │   ├── admin.py
│   │   ├── forms.py
│   │   ├── tasks.py                # Avatar generation tasks
│   │   ├── avatar_prompts.py       # Avatar persona prompts
│   │   ├── moderation.py           # Moderation logic
│   │   ├── moderation_config.py    # Moderation thresholds
│   │   ├── signals.py              # Post creation signals
│   │   ├── templates/
│   │   │   └── community/
│   │   │       ├── forum_list.html
│   │   │       ├── thread_list.html
│   │   │       ├── thread_detail.html
│   │   │       └── moderation_queue.html
│   │   └── tests/
│   │       ├── __init__.py
│   │       ├── test_models.py
│   │       ├── test_views.py
│   │       ├── test_tasks.py
│   │       └── test_moderation.py
│   │
│   ├── newsletter/                 # Newsletter system
│   │   ├── __init__.py
│   │   ├── models.py               # Subscription, NewsletterIssue
│   │   ├── views.py
│   │   ├── urls.py
│   │   ├── admin.py
│   │   ├── tasks.py                # Newsletter generation tasks
│   │   ├── curation.py             # Content curation logic
│   │   ├── templates/
│   │   │   └── newsletter/
│   │   │       ├── email_base.html
│   │   │       ├── weekly_digest.html
│   │   │       └── subscription_confirm.html
│   │   └── tests/
│   │       ├── __init__.py
│   │       ├── test_models.py
│   │       ├── test_tasks.py
│   │       └── test_curation.py
│   │
│   └── api/                        # REST API (optional)
│       ├── __init__.py
│       ├── serializers.py
│       ├── views.py
│       ├── urls.py
│       ├── permissions.py
│       └── tests/
│           ├── __init__.py
│           └── test_api.py
│
├── static/                         # Static files
│   ├── css/
│   │   ├── main.css
│   │   └── admin_custom.css
│   ├── js/
│   │   ├── main.js
│   │   ├── htmx.min.js
│   │   └── alpine.min.js
│   └── images/
│       ├── logo.png
│       └── avatars/
│
├── media/                          # User-uploaded files
│   ├── articles/
│   ├── avatars/
│   └── uploads/
│
├── templates/                      # Global templates
│   ├── base.html
│   ├── 404.html
│   ├── 500.html
│   └── admin/
│       └── custom_admin.html
│
├── logs/                           # Application logs
│   ├── django.log
│   ├── celery.log
│   └── scraping.log
│
├── docs/                           # Documentation
│   ├── plan.md
│   ├── enhanced_plan.md
│   ├── implementation_specs.md
│   ├── api_documentation.md
│   └── deployment_guide.md
│
└── scripts/                        # Utility scripts
    ├── deploy.sh
    ├── backup_db.sh
    └── setup_dev.sh
```

---

## **11. Environment Configuration**

### **11.1. .env.example**

```bash
# .env.example - Copy this to .env and fill in your values

# Django Settings
DEBUG=True
SECRET_KEY=your-secret-key-here-change-in-production
ALLOWED_HOSTS=localhost,127.0.0.1
DJANGO_SETTINGS_MODULE=extradime.settings.development

# Database Configuration
DB_ENGINE=django.db.backends.postgresql
DB_NAME=extradime_db
DB_USER=extradime_user
DB_PASSWORD=your-secure-database-password
DB_HOST=localhost
DB_PORT=5432

# Celery Configuration
CELERY_BROKER_URL=redis://localhost:6379/0
CELERY_RESULT_BACKEND=redis://localhost:6379/0
CELERY_TASK_ALWAYS_EAGER=False

# Redis Cache
REDIS_URL=redis://localhost:6379/1

# OpenAI API
OPENAI_API_KEY=sk-your-openai-api-key-here
OPENAI_MODEL=gpt-4
OPENAI_MAX_TOKENS=2000

# Anthropic API
ANTHROPIC_API_KEY=your-anthropic-api-key-here
ANTHROPIC_MODEL=claude-3-sonnet-20240229

# Google Gemini API (optional)
GOOGLE_API_KEY=your-google-api-key-here

# Content Moderation
PERSPECTIVE_API_KEY=your-perspective-api-key-here
MODERATION_ENABLED=True

# Email Configuration
EMAIL_BACKEND=django.core.mail.backends.smtp.EmailBackend
EMAIL_HOST=smtp.sendgrid.net
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=apikey
EMAIL_HOST_PASSWORD=your-sendgrid-api-key
DEFAULT_FROM_EMAIL=noreply@extradime.com
ADMIN_EMAIL=admin@extradime.com

# AWS Configuration (if using S3 for media)
AWS_ACCESS_KEY_ID=your-aws-access-key
AWS_SECRET_ACCESS_KEY=your-aws-secret-key
AWS_STORAGE_BUCKET_NAME=extradime-media
AWS_S3_REGION_NAME=us-east-1
USE_S3=False

# Scraping Configuration
USER_AGENT=ExtradimeBot/1.0 (+https://extradime.com/bot; contact@extradime.com)
DOWNLOAD_DELAY=2
CONCURRENT_REQUESTS=8
ROBOTSTXT_OBEY=True

# Proxy Configuration (optional)
USE_PROXIES=False
PROXY_URL=http://your-proxy-service.com
PROXY_USERNAME=your-proxy-username
PROXY_PASSWORD=your-proxy-password

# Monitoring and Logging
SENTRY_DSN=your-sentry-dsn-here
LOG_LEVEL=INFO

# Security
SECURE_SSL_REDIRECT=False
SESSION_COOKIE_SECURE=False
CSRF_COOKIE_SECURE=False
SECURE_HSTS_SECONDS=0

# Feature Flags
ENABLE_AI_AVATARS=True
ENABLE_AUTO_MODERATION=True
ENABLE_NEWSLETTER=True
ENABLE_API=False
```

---

## **12. Dependencies and Requirements**

### **12.1. requirements.txt**

```txt
# Core Django
Django==5.0.1
psycopg2-binary==2.9.9
python-decouple==3.8
django-environ==0.11.2

# Task Queue
celery==5.3.4
redis==5.0.1
django-celery-beat==2.5.0
django-celery-results==2.5.1

# Web Scraping
scrapy==2.11.0
beautifulsoup4==4.12.2
lxml==5.1.0
requests==2.31.0
httpx==0.26.0
selenium==4.16.0
feedparser==6.0.10
feedsearch-crawler==1.0.5
reppy==0.4.14

# AI/ML Libraries
openai==1.6.1
anthropic==0.8.1
langchain==0.1.0
langchain-openai==0.0.2
langchain-anthropic==0.0.1
tiktoken==0.5.2

# Content Moderation
google-api-python-client==2.111.0

# Forum (choose one based on evaluation)
django-machina==1.2.0
# OR for custom build:
# django-mptt==0.15.0

# Rich Text Editor
django-ckeditor==6.7.0
# OR
# django-tinymce==3.7.1

# Email
django-anymail[sendgrid]==10.2

# API (if using DRF)
djangorestframework==3.14.0
django-filter==23.5
drf-spectacular==0.27.0

# Image Processing
Pillow==10.2.0

# Testing
pytest==7.4.3
pytest-django==4.7.0
pytest-cov==4.1.0
pytest-mock==3.12.0
factory-boy==3.3.0
faker==22.0.0
vcrpy==5.1.0
responses==0.24.1

# Code Quality
black==23.12.1
flake8==7.0.0
isort==5.13.2
pylint==3.0.3
mypy==1.8.0
django-stubs==4.2.7

# Monitoring and Debugging
sentry-sdk==1.39.1
django-debug-toolbar==4.2.0
django-extensions==3.2.3
django-silk==5.0.4

# Utilities
python-slugify==8.0.1
python-dateutil==2.8.2
pytz==2023.3.post1
```

### **12.2. requirements-dev.txt**

```txt
-r requirements.txt

# Development Tools
ipython==8.19.0
ipdb==0.13.13
django-debug-toolbar==4.2.0
django-extensions==3.2.3

# Documentation
sphinx==7.2.6
sphinx-rtd-theme==2.0.0

# Testing Coverage
coverage==7.4.0
pytest-xdist==3.5.0
```

---

## **13. Django Models - Complete Implementation**

### **13.1. Scraping App Models**

**File: `apps/scraping/models.py`**

```python
"""
Models for web scraping and data source management.
"""
from django.db import models
from django.utils import timezone
from django.core.validators import URLValidator


class DataSource(models.Model):
    """Represents a source of information for scraping."""

    SOURCE_TYPE_CHOICES = [
        ('RSS', 'RSS Feed'),
        ('API', 'API'),
        ('WEBSITE', 'Website'),
        ('FORUM', 'Forum'),
    ]

    name = models.CharField(max_length=255, help_text="Human-readable name of the source")
    url = models.URLField(unique=True, validators=[URLValidator()], help_text="Main URL of the source")
    feed_url = models.URLField(null=True, blank=True, help_text="RSS/Atom feed URL if applicable")
    source_type = models.CharField(max_length=20, choices=SOURCE_TYPE_CHOICES, default='WEBSITE')
    last_checked = models.DateTimeField(null=True, blank=True, help_text="Last time this source was scraped")
    is_active = models.BooleanField(default=True, help_text="Whether to actively scrape this source")
    check_frequency_hours = models.IntegerField(default=24, help_text="How often to check this source (in hours)")
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    # Scraping configuration
    custom_settings = models.JSONField(
        null=True,
        blank=True,
        help_text="Custom Scrapy settings for this source (JSON format)"
    )

    # Statistics
    total_opportunities_found = models.IntegerField(default=0)
    last_error = models.TextField(null=True, blank=True)
    error_count = models.IntegerField(default=0)

    class Meta:
        ordering = ['-last_checked', 'name']
        verbose_name = "Data Source"
        verbose_name_plural = "Data Sources"
        indexes = [
            models.Index(fields=['is_active', 'last_checked']),
            models.Index(fields=['source_type']),
        ]

    def __str__(self):
        return f"{self.name} ({self.get_source_type_display()})"

    def mark_checked(self):
        """Update the last_checked timestamp."""
        self.last_checked = timezone.now()
        self.save(update_fields=['last_checked'])

    def record_error(self, error_message):
        """Record an error that occurred during scraping."""
        self.last_error = error_message
        self.error_count += 1
        self.save(update_fields=['last_error', 'error_count'])

    def reset_error_count(self):
        """Reset error count after successful scrape."""
        self.error_count = 0
        self.last_error = None
        self.save(update_fields=['error_count', 'last_error'])

    @property
    def needs_check(self):
        """Determine if this source needs to be checked based on frequency."""
        if not self.is_active:
            return False
        if not self.last_checked:
            return True
        time_since_check = timezone.now() - self.last_checked
        return time_since_check.total_seconds() / 3600 >= self.check_frequency_hours


class ScrapedOpportunity(models.Model):
    """Stores structured data extracted from a DataSource."""

    STATUS_CHOICES = [
        ('NEW', 'New'),
        ('PROCESSED', 'Processed'),
        ('REJECTED', 'Rejected'),
        ('USED_IN_CONTENT', 'Used in Content'),
    ]

    title = models.CharField(max_length=500)
    description = models.TextField()
    url = models.URLField(unique=True, max_length=1000)
    source = models.ForeignKey(
        DataSource,
        on_delete=models.CASCADE,
        related_name='opportunities'
    )

    # Discovery metadata
    date_discovered = models.DateTimeField(auto_now_add=True, db_index=True)
    processed_at = models.DateTimeField(null=True, blank=True)

    # Opportunity details
    potential_earnings_text = models.CharField(
        max_length=255,
        null=True,
        blank=True,
        help_text="Raw text describing potential earnings"
    )
    requirements_text = models.TextField(
        null=True,
        blank=True,
        help_text="Requirements or qualifications needed"
    )
    location = models.CharField(
        max_length=255,
        null=True,
        blank=True,
        help_text="Geographic location if applicable"
    )

    # Status and processing
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='NEW', db_index=True)

    # Raw data storage
    raw_data = models.JSONField(
        null=True,
        blank=True,
        help_text="Complete raw data extracted from source"
    )

    # Quality scoring
    quality_score = models.FloatField(
        null=True,
        blank=True,
        help_text="Automated quality score (0-1)"
    )

    class Meta:
        ordering = ['-date_discovered']
        verbose_name = "Scraped Opportunity"
        verbose_name_plural = "Scraped Opportunities"
        indexes = [
            models.Index(fields=['status', '-date_discovered']),
            models.Index(fields=['source', '-date_discovered']),
        ]

    def __str__(self):
        return f"{self.title} ({self.source.name})"

    def mark_processed(self):
        """Mark this opportunity as processed."""
        self.status = 'PROCESSED'
        self.processed_at = timezone.now()
        self.save(update_fields=['status', 'processed_at'])

    def mark_used_in_content(self):
        """Mark this opportunity as used in generated content."""
        self.status = 'USED_IN_CONTENT'
        self.save(update_fields=['status'])

    @property
    def is_new(self):
        """Check if this is a new, unprocessed opportunity."""
        return self.status == 'NEW'
```

---

