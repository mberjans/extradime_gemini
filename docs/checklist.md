Of course. Here is a detailed checklist of tiny tasks for each software development ticket, structured to follow a Test-Driven Development (TDD) workflow.

### **Phase 1: Foundation & Core Scraping**

#### **EXD-001: Initial Project Setup and Core Infrastructure**

*This ticket involves setting up the foundational project structure. For each configurable component, a test will be written to validate its configuration before implementation.*

* \[ \] **EXD-001-01:** Initialize the Django project extradime and create the core and users applications.  
* \[ \] **EXD-001-02:** Write a unit test to check that the DATABASES setting in settings.py is configured to use the django.db.backends.postgresql engine.  
* \[ \] **EXD-001-03:** Configure the project's settings.py to connect to the PostgreSQL database.  
* \[ \] **EXD-001-04:** Run the database configuration test to ensure it passes.  
* \[ \] **EXD-001-05:** Write a simple test case using Django's Test Client to check for a 200 OK response from the root URL (/).  
* \[ \] **EXD-001-06:** Create a basic view and URL pattern in the core app to serve the homepage and make the test pass.  
* \[ \] **EXD-001-07:** Run the homepage view test again to confirm it passes.  
* \[ \] **EXD-001-08:** Run the initial manage.py migrate command to create the necessary default Django tables in the PostgreSQL database.

#### **EXD-002: Integrate Celery and Redis for Background Task Processing**

*This ticket focuses on integrating the task queue. Tests will validate the configuration and the ability to execute a task asynchronously.*

* \[ \] **EXD-002-01:** Write a unit test to verify that Celery is correctly configured in the Django settings (e.g., CELERY\_BROKER\_URL points to Redis).  
* \[ \] **EXD-002-02:** Install celery and redis-py packages and add Celery configuration to settings.py and a celery.py module.  
* \[ \] **EXD-002-03:** Run the configuration test to ensure it passes.  
* \[ \] **EXD-002-04:** Write a test for a simple Celery task (e.g., an add(x, y) function) that asserts the task can be called with .delay() and returns the correct result. Use task\_always\_eager=True for testing.  
* \[ \] **EXD-002-05:** Implement the simple Celery task.  
* \[ \] **EXD-002-06:** Run the Celery task test to confirm it passes.

#### **EXD-003: Create scraping App and Data Models**

*This ticket involves creating the data schema for scraped information. Each model's fields and behaviors will be tested before the model is written.*

* \[ \] **EXD-003-01:** Create the scraping app.  
* \[ \] **EXD-003-02:** Write a failing unit test in scraping/tests.py to create an instance of the DataSource model and assert that all specified fields (name, url, source\_type, is\_active, etc.) exist and have the correct types and defaults.  
* \[ \] **EXD-003-03:** Define the DataSource model in scraping/models.py to make the test pass.  
* \[ \] **EXD-003-04:** Run the DataSource model test to confirm it passes.  
* \[ \] **EXD-003-05:** Write a failing unit test to create a ScrapedOpportunity instance, asserting its fields and its Foreign Key relationship to DataSource.  
* \[ \] **EXD-003-06:** Define the ScrapedOpportunity model in scraping/models.py to make the test pass.  
* \[ \] **EXD-003-07:** Run the ScrapedOpportunity model test to confirm it passes.  
* \[ \] **EXD-003-08:** Run manage.py makemigrations scraping and manage.py migrate to apply the new models to the database.

#### **EXD-004: Implement Admin Interface for Scraping Models**

*This ticket focuses on backend usability. Tests will ensure the models are registered and customizations are applied correctly.*

* \[ \] **EXD-004-01:** Write a test to assert that DataSource is registered with the Django admin site.  
* \[ \] **EXD-004-02:** Register DataSource in scraping/admin.py.  
* \[ \] **EXD-004-03:** Run the DataSource admin registration test.  
* \[ \] **EXD-004-04:** Write a test to assert that ScrapedOpportunity is registered with the Django admin site and that its ModelAdmin class specifies status and source in list\_filter.  
* \[ \] **EXD-004-05:** Register ScrapedOpportunity in scraping/admin.py with a custom ModelAdmin to add the required filters.  
* \[ \] **EXD-004-06:** Run the ScrapedOpportunity admin registration test to confirm it passes.

#### **EXD-005: Develop RSS Feed Scraper Task**

*This ticket creates the first data gathering mechanism. Tests will mock the external feedparser library to ensure the task's logic is correct in isolation.*

* \[ \] **EXD-005-01:** Write a failing unit test for the RSS scraper Celery task. The test should create a mock DataSource object in the test database.  
* \[ \] **EXD-005-02:** In the test, use unittest.mock.patch to mock feedparser.parse to return a predictable, sample feed structure.  
* \[ \] **EXD-005-03:** The test should assert that after the task runs, new ScrapedOpportunity objects corresponding to the mock feed entries are created in the database.  
* \[ \] **EXD-005-04:** Implement the basic structure of the Celery task in scraping/tasks.py, querying for active DataSource objects with a source\_type of 'RSS'.  
* \[ \] **EXD-005-05:** Add the logic to the task to call feedparser.parse and create ScrapedOpportunity instances from the results, making the test pass.  
* \[ \] **EXD-005-06:** Write a new test to handle potential exceptions during feed parsing (e.g., a malformed URL) and assert that the task does not crash.  
* \[ \] **EXD-005-07:** Implement the error handling logic in the task.  
* \[ \] **EXD-005-08:** Run all tests for the RSS scraper task to confirm they pass.

#### **EXD-006: Develop Initial Scrapy Spider for a Target Website**

*This ticket integrates Scrapy. Tests will use saved HTML files as inputs to validate the spider's parsing logic without hitting the live web.*

* \[ \] **EXD-006-01:** Integrate the Scrapy project structure within the Django app.  
* \[ \] **EXD-006-02:** Write a failing unit test for the Django item pipeline that checks if it correctly receives a Scrapy item and creates a ScrapedOpportunity model instance.  
* \[ \] **EXD-006-03:** Implement the Scrapy pipeline in scraping/pipelines.py to save items to the database.  
* \[ \] **EXD-006-04:** Run the pipeline test to confirm it passes.  
* \[ \] **EXD-006-05:** Save a sample HTML file from the target website locally for testing.  
* \[ \] **EXD-006-06:** Write a failing spider unit test that runs the spider on the local HTML file and asserts that it yields the correct number of Scrapy items with correctly parsed data.  
* \[ \] **EXD-006-07:** Implement the spider's parsing logic in scraping/spiders/ using CSS selectors or XPath to make the test pass.  
* \[ \] **EXD-006-08:** Run the spider parsing test to confirm it passes.

#### **EXD-007: Implement Ethical Scraping Best Practices**

*This ticket focuses on configuration. Tests will inspect the spider's settings object to ensure compliance.*

* \[ \] **EXD-007-01:** Write a unit test that loads the Scrapy project settings and asserts that ROBOTSTXT\_OBEY is True.  
* \[ \] **EXD-007-02:** Set ROBOTSTXT\_OBEY \= True in the Scrapy settings.py.  
* \[ \] **EXD-007-03:** Run the ROBOTSTXT\_OBEY test.  
* \[ \] **EXD-007-04:** Write a test to assert that DOWNLOAD\_DELAY is set to a reasonable value (e.g., \>= 1).  
* \[ \] **EXD-007-05:** Set the DOWNLOAD\_DELAY in the Scrapy settings.  
* \[ \] **EXD-007-06:** Run the DOWNLOAD\_DELAY test.  
* \[ \] **EXD-007-07:** Write a test to ensure the User-Agent middleware is enabled and configured.  
* \[ \] **EXD-007-08:** Implement or configure the User-Agent rotation middleware.  
* \[ \] **EXD-007-09:** Run the User-Agent middleware test to confirm it passes.

### **Phase 2: Content Display & Basic AI Generation**

#### **EXD-008: Create content App and Data Models**

*This follows the same TDD pattern as EXD-003 for the new content app models.*

* \[ \] **EXD-008-01:** Create the content app.  
* \[ \] **EXD-008-02:** Write failing unit tests for the Topic, Article, ContentRevision, and PromptLog models, asserting their fields, relationships, and any custom methods (e.g., a get\_absolute\_url on Article).  
* \[ \] **EXD-008-03:** Implement the Topic, Article, ContentRevision, and PromptLog models in content/models.py.  
* \[ \] **EXD-008-04:** Run all model tests to confirm they pass.  
* \[ \] **EXD-008-05:** Run makemigrations and migrate for the content app.

#### **EXD-009: Develop Frontend Views for Articles and Topics**

*For each view, a test will be written first to define the expected behavior, context data, and response code.*

* \[ \] **EXD-009-01:** Write a failing test for the article list view (/articles/). Assert it returns a 200 status code, uses the correct template (article\_list.html), and the context contains a list of published Article objects.  
* \[ \] **EXD-009-02:** Implement the article list view to make the test pass.  
* \[ \] **EXD-009-03:** Run the article list view test.  
* \[ \] **EXD-009-04:** Write a failing test for the article detail view (/articles/\<slug\>/). Assert it returns 200 for a published article and 404 for a draft or non-existent article.  
* \[ \] **EXD-009-05:** Implement the article detail view.  
* \[ \] **EXD-009-06:** Run the article detail view test.  
* \[ \] **EXD-009-07:** Write a failing test for the topic filter view (/topics/\<slug\>/), asserting it only returns articles associated with that topic.  
* \[ \] **EXD-009-08:** Implement the topic filter view.  
* \[ \] **EXD-009-09:** Run the topic filter view test.  
* \[ \] **EXD-009-10:** Create the basic HTML templates (base.html, article\_list.html, article\_detail.html).

#### **EXD-010: Build Service for LLM API Integration**

*This ticket creates a wrapper around the LLM API. Tests will mock the external API call to ensure the service's logic and error handling are robust.*

* \[ \] **EXD-010-01:** Write a failing unit test for the LLM service function/method. Use unittest.mock.patch to mock the openai (or equivalent) client library call.  
* \[ \] **EXD-010-02:** The test should assert that the service function calls the external API with the correctly formatted prompt and API key.  
* \[ \] **EXD-010-03:** Implement the LLM service in a services.py or utils.py file, handling API key retrieval from environment variables.  
* \[ \] **EXD-010-04:** Run the test to confirm it passes.  
* \[ \] **EXD-010-05:** Write a new test that simulates an API error from the mocked library and asserts that the service handles the exception gracefully (e.g., logs the error and returns None or raises a custom exception).  
* \[ \] **EXD-010-06:** Implement the error handling logic in the service.  
* \[ \] **EXD-010-07:** Run all service tests to confirm they pass.

#### **EXD-011: Implement "Auto-Create with Manual Review" Content Workflow (Workflow 2\)**

*This ticket combines multiple components. The test will verify the logic of the Celery task, mocking the LLM service created in the previous ticket.*

* \[ \] **EXD-011-01:** Write a failing unit test for the content generation Celery task. The test should create a sample ScrapedOpportunity object.  
* \[ \] **EXD-011-02:** In the test, mock the LLM service (from EXD-010) to return a predictable string of article text.  
* \[ \] **EXD-011-03:** The test should assert that after the task runs, a new Article is created in the database with its status field set to 'review' and its body containing the mocked text.  
* \[ \] **EXD-011-04:** Implement the Celery task in content/tasks.py. The task should fetch the ScrapedOpportunity, build a prompt, call the LLM service, and create the Article object.  
* \[ \] **EXD-011-05:** Run the content generation task test to confirm it passes.

#### **EXD-012: Enhance Admin for Content Review and Publishing**

*This builds on EXD-004. Tests will verify the custom admin actions and filters.*

* \[ \] **EXD-012-01:** Write a test to check that a custom filter for 'review' status is present in the Article admin.  
* \[ \] **EXD-012-02:** Write a test for a custom admin action that changes the status of selected articles from 'review' to 'published'. The test will need to simulate an admin request.  
* \[ \] **EXD-012-03:** Implement the custom filter and the "publish selected" admin action in content/admin.py.  
* \[ \] **EXD-012-04:** Run the admin action and filter tests.  
* \[ \] **EXD-012-05:** Manually integrate and configure a rich text editor package (e.g., django-ckeditor) for the Article admin form.

#### **EXD-013: Implement Main Article RSS Feed**

*Tests will use Django's test client to fetch the feed URL and parse the XML response to validate its structure and content.*

* \[ \] **EXD-013-01:** Write a failing test that makes a GET request to /feeds/articles/.  
* \[ \] **EXD-013-02:** The test should assert that the response has a 200 status code and a content type of application/rss+xml.  
* \[ \] **EXD-013-03:** Create several published Article objects in the test database. The test should then parse the XML response and assert that the article titles and links are present in the feed.  
* \[ \] **EXD-013-04:** Implement the ArticleFeed class using django.contrib.syndication in a feeds.py file.  
* \[ \] **EXD-013-05:** Add the URL pattern for the feed in urls.py.  
* \[ \] **EXD-013-06:** Run the RSS feed test to confirm it passes.

*The remaining phases would follow the same rigorous TDD-based checklist structure. For brevity, a few key examples are provided below.*

### **Phase 3: Basic Community & User Interaction (Sample)**

#### **EXD-014: Evaluate and Integrate django-machina Forum Package**

*Integration tickets are harder to test-drive, but we can test the configuration.*

* \[ \] **EXD-014-01:** Write a test to ensure forum URLs (e.g., /forum/) are correctly resolved after integration.  
* \[ \] **EXD-014-02:** Install and add machina to INSTALLED\_APPS and include its URLs.  
* \[ \] **EXD-014-03:** Run the URL resolution test to confirm it passes.  
* \[ \] **EXD-014-04:** Write a test to ensure that a logged-in user can access the main forum index and receive a 200 response.  
* \[ \] **EXD-014-05:** Complete the django-machina setup, including running its migrations.  
* \[ \] **EXD-014-06:** Run the authenticated access test to confirm it passes.

### **Phase 4: AI Avatars & Auto Moderation (Sample)**

#### **EXD-017: Create AIAvatarProfile Model and Admin Interface**

*This follows the standard model TDD pattern.*

* \[ \] **EXD-017-01:** Create the community app.  
* \[ \] **EXD-017-02:** Write a failing unit test for the AIAvatarProfile model. Assert its One-to-One relationship with the User model and the presence of personality\_description and llm\_persona\_prompt fields.  
* \[ \] **EXD-017-03:** Implement the AIAvatarProfile model in community/models.py.  
* \[ \] **EXD-017-04:** Run the model test to confirm it passes.  
* \[ \] **EXD-017-05:** Write a test to ensure the model is registered in the Django admin.  
* \[ \] **EXD-017-06:** Implement the admin registration in community/admin.py.  
* \[ \] **EXD-017-07:** Run the admin test and then run migrations.

#### **EXD-021: Implement Automated Moderation Workflow**

*This workflow test will mock the external moderation service to validate the internal logic.*

* \[ \] **EXD-021-01:** Write a failing test for the post-creation signal handler or function.  
* \[ \] **EXD-021-02:** In the test, mock the moderation service (from EXD-020) to return a "low" toxicity score. Assert that the created forum post is immediately visible.  
* \[ \] **EXD-021-03:** In a separate test, mock the moderation service to return a "high" toxicity score. Assert that the created forum post is marked as 'pending review' (or equivalent status) and is not publicly visible.  
* \[ \] **EXD-021-04:** Implement the post-creation logic that calls the moderation service via a Celery task and updates the post's status based on the result.  
* \[ \] **EXD-021-05:** Run all moderation workflow tests to confirm they pass.