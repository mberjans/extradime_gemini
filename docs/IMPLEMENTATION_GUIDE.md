# Extradime.com - Complete Implementation Guide

> **This document serves as the master guide for implementing the Extradime.com platform. It references and organizes all implementation specifications across multiple documents.**

---

## Document Structure

This implementation guide is organized across multiple documents for manageability:

1. **docs/plan.md** - Original Technical Development Plan (Strategic/Architectural)
2. **docs/enhanced_plan.md** - Enhanced plan with original content + extensions
3. **docs/implementation_specs.md** - Detailed implementation specifications (THIS IS THE KEY DOCUMENT)
4. **docs/IMPLEMENTATION_GUIDE.md** - This file (Master roadmap and quick reference)

---

## Quick Start for AI Implementation

### Prerequisites Checklist

- [ ] Python 3.11+ installed
- [ ] PostgreSQL 15+ installed and running
- [ ] Redis installed and running
- [ ] Git repository initialized
- [ ] Virtual environment created
- [ ] All API keys obtained (OpenAI, Anthropic, SendGrid, etc.)

### Initial Setup Commands

```bash
# 1. Clone/Create repository
git clone <repository-url> extradime_gemini
cd extradime_gemini

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set up environment variables
cp .env.example .env
# Edit .env with your actual values

# 5. Create database
createdb extradime_db
createuser extradime_user -P

# 6. Run migrations
python manage.py migrate

# 7. Create superuser
python manage.py createsuperuser

# 8. Load initial data (if fixtures exist)
python manage.py loaddata initial_data

# 9. Run development server
python manage.py runserver

# 10. In separate terminals, start Celery
celery -A extradime worker -l info
celery -A extradime beat -l info
```

---

## Implementation Order - Phase 1 (Weeks 1-8)

### Week 1-2: Project Foundation

#### Task 1.1: Django Project Setup (8 hours)
**Files to create:**
- `extradime/__init__.py`
- `extradime/settings/base.py`
- `extradime/settings/development.py`
- `extradime/settings/production.py`
- `extradime/urls.py`
- `extradime/wsgi.py`
- `extradime/asgi.py`
- `manage.py`
- `.env.example`
- `requirements.txt`

**Reference:** See `docs/implementation_specs.md` Section 11-12 for complete file contents.

**Acceptance Criteria:**
- [ ] Django project runs without errors
- [ ] Settings properly split into base/dev/prod
- [ ] Environment variables loading correctly
- [ ] Admin interface accessible at /admin/

#### Task 1.2: Database Configuration (4 hours)
**Actions:**
- Configure PostgreSQL connection in settings
- Set up database user and permissions
- Test database connectivity

**Acceptance Criteria:**
- [ ] Can connect to PostgreSQL
- [ ] Migrations run successfully
- [ ] Can create/read/update/delete test records

#### Task 1.3: Celery Setup (6 hours)
**Files to create:**
- `extradime/celery.py`
- Configure Redis as broker

**Reference:** See implementation_specs.md for complete Celery configuration.

**Acceptance Criteria:**
- [ ] Celery worker starts without errors
- [ ] Celery beat scheduler runs
- [ ] Can execute test task successfully
- [ ] Tasks appear in Redis

#### Task 1.4: Core App Setup (4 hours)
**Files to create:**
- `apps/core/__init__.py`
- `apps/core/models.py`
- `apps/core/views.py`
- `apps/core/urls.py`
- `apps/core/templates/core/base.html`
- `apps/core/templates/core/home.html`

**Acceptance Criteria:**
- [ ] Home page renders correctly
- [ ] Base template includes CSS/JS
- [ ] Navigation structure in place

### Week 3-4: Scraping Infrastructure

#### Task 2.1: Scraping Models (6 hours)
**Files to create:**
- `apps/scraping/models.py` (DataSource, ScrapedOpportunity)
- Migrations

**Reference:** See implementation_specs.md Section 13.1 for complete model code.

**Acceptance Criteria:**
- [ ] Models created and migrated
- [ ] Can create DataSource via admin
- [ ] Can create ScrapedOpportunity via admin
- [ ] All model methods work correctly
- [ ] Unit tests pass

#### Task 2.2: Scrapy Integration (12 hours)
**Files to create:**
- `apps/scraping/spiders/__init__.py`
- `apps/scraping/spiders/base_spider.py`
- `apps/scraping/spiders/rss_spider.py`
- `apps/scraping/items.py`
- `apps/scraping/pipelines.py`
- `apps/scraping/settings.py`
- `apps/scraping/scrapy.cfg`

**Key Implementation Points:**
1. Base spider with robots.txt checking
2. RSS feed spider for initial data gathering
3. Pipeline to save to Django database
4. Rate limiting and user-agent rotation
5. Error handling and logging

**Acceptance Criteria:**
- [ ] RSS spider successfully fetches feeds
- [ ] Data saved to ScrapedOpportunity model
- [ ] Robots.txt respected
- [ ] Rate limiting works
- [ ] Errors logged properly

#### Task 2.3: Scraping Celery Tasks (8 hours)
**Files to create:**
- `apps/scraping/tasks.py`

**Key Tasks to Implement:**
```python
@shared_task
def run_spider_task(spider_name, source_id)

@shared_task
def check_all_sources()

@shared_task
def cleanup_old_opportunities()
```

**Acceptance Criteria:**
- [ ] Can trigger spider via Celery
- [ ] Scheduled tasks run automatically
- [ ] Error handling works
- [ ] Task results logged

#### Task 2.4: Scraping Admin Interface (4 hours)
**Files to create:**
- `apps/scraping/admin.py`

**Features:**
- Custom list display for DataSource
- Custom list display for ScrapedOpportunity
- Filters and search
- Custom admin actions (e.g., "Run Spider Now")

**Acceptance Criteria:**
- [ ] Can manage sources via admin
- [ ] Can view scraped opportunities
- [ ] Can trigger scraping from admin
- [ ] Statistics displayed correctly

### Week 5-6: Content Models and Basic Display

#### Task 3.1: Content Models (8 hours)
**Files to create:**
- `apps/content/models.py` (Topic, Article, PromptLog, ContentRevision)
- Migrations

**Models to Implement:**
- Topic
- Article
- PromptLog
- ContentRevision

**Acceptance Criteria:**
- [ ] All models created and migrated
- [ ] Relationships work correctly
- [ ] Can create articles via admin
- [ ] Revision tracking works
- [ ] Unit tests pass

#### Task 3.2: Content Views (10 hours)
**Files to create:**
- `apps/content/views.py`
- `apps/content/urls.py`
- `apps/content/templates/content/*.html`

**Views to Implement:**
- ArticleListView
- ArticleDetailView
- OpportunityListView
- OpportunityDetailView
- TopicListView

**Acceptance Criteria:**
- [ ] Article list page works
- [ ] Article detail page works
- [ ] Pagination works
- [ ] Topic filtering works
- [ ] SEO meta tags present

#### Task 3.3: RSS Feeds (4 hours)
**Files to create:**
- `apps/content/feeds.py`

**Feeds to Implement:**
- ArticlesFeed
- TopicFeed (optional)

**Acceptance Criteria:**
- [ ] RSS feed validates
- [ ] Contains correct data
- [ ] Accessible at /feeds/articles/

### Week 7-8: Basic AI Content Generation

#### Task 4.1: Prompt Templates (6 hours)
**Files to create:**
- `apps/content/prompts.py`

**Templates to Create:**
- Article generation prompts (beginner guide, review, comparison)
- Summarization prompts
- Title generation prompts

**Reference:** See Section 14 in implementation_specs.md for complete prompt templates.

**Acceptance Criteria:**
- [ ] All prompt templates defined
- [ ] Templates accept dynamic variables
- [ ] Prompts tested manually with LLM

#### Task 4.2: AI Utility Functions (8 hours)
**Files to create:**
- `apps/content/ai_utils.py`

**Functions to Implement:**
```python
def call_openai_api(prompt, model="gpt-4", max_tokens=2000)
def call_anthropic_api(prompt, model="claude-3-sonnet")
def generate_article_from_opportunity(opportunity_id)
def generate_article_title(content)
def summarize_text(text, max_length=200)
```

**Acceptance Criteria:**
- [ ] Can call OpenAI API successfully
- [ ] Can call Anthropic API successfully
- [ ] Error handling works
- [ ] Token counting works
- [ ] Cost tracking implemented

#### Task 4.3: Content Generation Tasks (10 hours)
**Files to create:**
- `apps/content/tasks.py`

**Tasks to Implement:**
```python
@shared_task
def generate_article_draft_task(opportunity_id, workflow='review')

@shared_task
def batch_generate_articles(opportunity_ids)

@shared_task
def regenerate_article_task(article_id)
```

**Acceptance Criteria:**
- [ ] Can generate article from opportunity
- [ ] Article saved with 'review' status
- [ ] PromptLog created
- [ ] Metadata stored correctly
- [ ] Error handling works

#### Task 4.4: Content Admin Enhancements (6 hours)
**Files to create:**
- `apps/content/admin.py`

**Features:**
- Custom Article admin with rich text editor
- Review queue filter
- Custom actions (Generate Draft, Publish, etc.)
- PromptLog inline display

**Acceptance Criteria:**
- [ ] Rich text editor works
- [ ] Can filter by status
- [ ] Custom actions work
- [ ] Revision history visible

---

## Implementation Order - Phase 2 (Weeks 9-16)

### Week 9-10: User Management

#### Task 5.1: User Models and Authentication
#### Task 5.2: User Profile Pages
#### Task 5.3: Registration and Login Forms

### Week 11-12: Forum Integration

#### Task 6.1: Evaluate and Install django-machina
#### Task 6.2: Customize Forum Templates
#### Task 6.3: Integrate with User System

### Week 13-14: Basic Moderation

#### Task 7.1: Moderation Configuration
#### Task 7.2: Perspective API Integration
#### Task 7.3: Moderation Workflow Implementation

### Week 15-16: Testing and Refinement

#### Task 8.1: Write Comprehensive Tests
#### Task 8.2: Performance Optimization
#### Task 8.3: Security Audit

---

## Implementation Order - Phase 3 (Weeks 17-24)

### AI Avatars Implementation
### Advanced Moderation
### Newsletter System

---

## Implementation Order - Phase 4 (Weeks 25-32)

### Advanced Features
### Scaling and Optimization
### Deployment

---

## Critical Code Sections Reference

### Where to Find Complete Code Examples

1. **Django Models**: `implementation_specs.md` Section 13
2. **Celery Tasks**: `implementation_specs.md` Section 15
3. **Scrapy Spiders**: `implementation_specs.md` Section 16
4. **Prompt Templates**: `implementation_specs.md` Section 14
5. **Admin Customizations**: `implementation_specs.md` Section 17
6. **Views and URLs**: `implementation_specs.md` Section 18
7. **Forms**: `implementation_specs.md` Section 19
8. **Tests**: `implementation_specs.md` Section 20
9. **Configuration Files**: `implementation_specs.md` Sections 11-12

---

## Testing Strategy

### Unit Tests (Run after each task)
```bash
pytest apps/scraping/tests/
pytest apps/content/tests/
pytest apps/community/tests/
```

### Integration Tests (Run after each week)
```bash
pytest --integration
```

### Coverage Report
```bash
pytest --cov=apps --cov-report=html
```

---

## Deployment Checklist

- [ ] All tests passing
- [ ] Security audit completed
- [ ] Environment variables configured
- [ ] Database backed up
- [ ] Static files collected
- [ ] Celery workers configured
- [ ] Monitoring set up (Sentry)
- [ ] SSL certificates installed
- [ ] Domain configured
- [ ] Email service configured

---

## Troubleshooting Common Issues

### Issue: Celery tasks not running
**Solution:** Check Redis connection, ensure worker is running, check task routing

### Issue: Scrapy spider fails
**Solution:** Check robots.txt, verify selectors, check rate limiting

### Issue: LLM API errors
**Solution:** Verify API keys, check rate limits, verify prompt format

### Issue: Database connection errors
**Solution:** Check PostgreSQL service, verify credentials, check network

---

## Next Steps

1. Review `docs/plan.md` for strategic context
2. Study `docs/implementation_specs.md` for detailed code examples
3. Follow this guide's task order for implementation
4. Test thoroughly after each task
5. Commit frequently with descriptive messages

---

## Support and Resources

- Django Documentation: https://docs.djangoproject.com/
- Celery Documentation: https://docs.celeryproject.org/
- Scrapy Documentation: https://docs.scrapy.org/
- OpenAI API Documentation: https://platform.openai.com/docs
- Anthropic API Documentation: https://docs.anthropic.com/


