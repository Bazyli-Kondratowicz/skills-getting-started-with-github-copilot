## Plan: Add backend FastAPI tests

TL;DR: create a new `tests/` directory with `pytest` tests for the FastAPI backend, add `pytest` to `requirements.txt`, and verify that the API endpoints work as expected using `fastapi.testclient`.

**Steps**
1. Add `pytest` to `requirements.txt` so the project has the test runner dependency.
2. Create a new directory `tests/` at the repository root.
3. Add `tests/test_app.py` containing FastAPI backend tests for the API:
   - use `from fastapi.testclient import TestClient` and `from src.app import app, activities`
   - define a fixture that resets the in-memory `activities` store before each test using a deep copy of the initial activity data.
   - cover the main backend flows:
     - `GET /activities` returns all activities and activity fields
     - `POST /activities/{activity_name}/signup` adds a participant
     - duplicate signup returns `400`
     - signup for missing activity returns `404`
     - `DELETE /activities/{activity_name}/signup` removes a participant
     - unregistering a missing participant returns `404`
4. Use the AAA (Arrange-Act-Assert) pattern in each test to keep structure clear and consistent.
5. Verify by running `pytest` from the repo root and confirm all tests pass.

**Relevant files**
- `/workspaces/skills-getting-started-with-github-copilot/requirements.txt`
- `/workspaces/skills-getting-started-with-github-copilot/tests/test_app.py`
- `/workspaces/skills-getting-started-with-github-copilot/pytest.ini`

**Verification**
1. Confirm `pytest` is present in `requirements.txt`.
2. Confirm `tests/test_app.py` exists and imports `TestClient` plus `app` from `src.app`.
3. Run `pytest` and expect all tests to pass.
4. Confirm there is no reliance on the web UI; tests should exercise the FastAPI backend directly.

**Decisions**
- Use a separate `tests/` folder as requested.
- Keep tests backend-only and avoid frontend coverage.
- Reset in-memory state between tests to avoid flaky failures.
