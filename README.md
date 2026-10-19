PWPytestFramework
End-to-end Playwright + pytest test framework for web UI automation (page-object style) with built-in reporting and test artifact collection. It's designed for functional and regression tests against e-commerce flows (login, registration, product search, cart, checkout).

Stack
Languages: Python 3.x
Framework / runtime: pytest + Playwright (sync)
Notable libraries: pytest-playwright, playwright, allure-pytest, pytest-xdist
Quick start
Clone the repo git clone https://github.com/Ashish-SDET30/PWPytestFramework.git cd PWPytestFramework

Install Python dependencies pip install -r requirements.txt

Install Playwright browsers (required once) playwright install

(Optionally on some systems) install browser dependencies: playwright install --with-deps

Run tests
Run the full test suite: pytest

Run tests with specific runtime options (examples): pytest --browser=chromium --base_url="https://demo.nopcommerce.com" --headed=True --video=retain-on-failure --tracing=retain-on-failure --screenshot=only-on-failure

Run a single test: pytest tests/test_login.py::test_valid_login --browser=chromium --base_url="https://demo.nopcommerce.com"

Run tests in parallel (xdist): pytest -n 4 --browser=chromium --base_url="https://demo.nopcommerce.com"

Generate and view Allure report (requires Allure CLI installed): pytest --alluredir=reports/allure-results allure serve reports/allure-results

Configuration options (used by conftest.py)
These can be supplied on the pytest command-line or set in pytest.ini:

--browser : chromium | firefox | webkit (default from pytest.ini)
--base_url : base URL for the AUT
--headed : True/False (run browser headed)
--video : on | retain-on-failure | off
--tracing : on | retain-on-failure | off
--screenshot : on | only-on-failure | off
(conftest.py contains the helpers that read these values and configure Playwright contexts/pages accordingly)

Test artifacts / reports
reports/screenshots/ — screenshots saved on failure
reports/videos/ — videos recorded when enabled
reports/traces/ — Playwright trace zips
reports/allure-results — Allure raw results (when run with --alluredir)
Artifacts are attached to Allure reports where supported.

Project structure
pages/ checkout_page.py Page objects for checkout flow home_page.py Home page interactions login_page.py Login page object logout_page.py Logout interactions my_account_page.py Account page actions product_page.py Product detail interactions registration_page.py Registration page object search_results_page.py Search results interactions shopping_cart_page.py Shopping cart interactions

utilties/ data_reader_util.py Utilities to read test data (Excel/csv) random_data_util.py Helpers to generate random test data

tests/ test_login.py test_login_data_driven.py test_user_registration.py test_user_logout.py test_product_search.py test_add_product_to_cart.py test_end_to_end.py

config.py Small config holder (example credentials / test values) conftest.py Pytest fixtures and hooks (Playwright setup, artifact collection) pytest.ini Default pytest configuration (CLI defaults)

Test design notes
Page-object pattern is implemented under pages/*. Tests import page objects and exercise user flows.
conftest.py provides browser_context and page fixtures that:
manage Playwright lifecycle (start/stop)
optionally enable video, tracing, screenshots
attach artifacts to Allure on failures
Test data
testdata/ — place data files used by data-driven tests (example: Excel / CSV)
Utilities
utilties/data_reader_util.py — read test data sheets/files used by data-driven tests
utilties/random_data_util.py — generate random names/emails for registration tests
Security / secrets
Currently config.py contains example credentials for demos. Do NOT commit real credentials. For CI or real runs, prefer environment variables or a secrets manager (python-dotenv is available in requirements if you want .env support).

Contributing
Fork the repo
Add tests or page objects under the appropriate folder
Keep fixtures in conftest.py for cross-cutting behavior
Open a PR with description of changes and test coverage
Troubleshooting
If browsers fail to launch, run: playwright install
If tests cannot find base URL, provide --base_url on the CLI or set it in pytest.ini
For Allure reporting, ensure allure CLI is installed and on PATH
Contact
Maintained by: Ashish-SDET30 (GitHub)
