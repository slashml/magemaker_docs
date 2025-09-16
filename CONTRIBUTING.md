---
title: CONTRIBUTING.md
description: How to contribute to Magemaker
"og:title": "Contributing to Magemaker"
---

## Contributing to Magemaker

We love your input! We want to make contributing to Magemaker as easy and transparent as possible, whether it's:

- Reporting a bug
- Discussing the current state of the code
- Submitting a fix
- Proposing new features
- Improving the documentation
- Becoming a maintainer

---

## Ways to Contribute

### 1. Report Issues

If you encounter any bugs or have feature requests:

1. Go to our GitHub repository
2. Click on **Issues**
3. Click **New Issue**
4. Choose the appropriate template (Bug Report or Feature Request)
5. Fill out the template with as much detail as possible

<Card title="Creating an issue" icon="github" href="https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-an-issue">
  Keep track of bugs, enhancements, or other requests with Issues.
</Card>

### 2. Submit Pull Requests

1. Fork the repo and create your branch from `main`
2. If you've added code that should be tested, add **unit and/or integration tests** (see *Testing* below)
3. If you've changed public-facing APIs or added a new feature, update **documentation** (docs live under the `docs/` folder)
4. Ensure the test suite passes: `pytest -q`
5. Run the auto-formatters and linters (see *Code Style*)
6. Issue that pull request!

<Card title="Creating a pull request" icon="github" href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request">
  Create a Pull Request to propose and collaborate on changes to a repository.
</Card>

---

## Local Development Setup

<Steps>
  <Step title="Fork and Clone">
    ```bash
    git clone https://github.com/YOUR_USERNAME/magemaker.git
    cd magemaker
    ```
  </Step>
  <Step title="Create and Activate Virtualenv (optional but recommended)">
    ```bash
    python -m venv .venv
    source .venv/bin/activate  # Linux / macOS
    .venv\Scripts\activate     # Windows
    ```
  </Step>
  <Step title="Install Dependencies (dev)">
    ```bash
    pip install -e ".[dev]"
    ```
  </Step>
  <Step title="Run Tests">
    ```bash
    pytest -q
    ```
  </Step>
  <Step title="Run the Local API Server (optional)">
    If you are working on the FastAPI server (`server.py`) or the OpenAI-compatible proxy, you can spin it up locally:
    ```bash
    uvicorn server:app --reload --port 8000
    ```
    This requires AWS credentials in a `.env` file (see `configuration/Environment`).
  </Step>
</Steps>

---

## Code Style

We use **Black**, **isort**, and **flake8** to maintain code quality.

```bash
black .
isort .
flake8
```

A pre-commit configuration is provided. You can install the Git hooks with:

```bash
pre-commit install
```

This will automatically run the formatters and linters before every commit.

---

## Testing

All new features **must** include tests. We use **pytest** for our test suite:

- **Unit tests** live next to the module being tested (e.g. `magemaker/gcp/test_*.py`).
- **Integration tests** should be marked with `@pytest.mark.integration` so they can be skipped in CI if needed.
- When adding a new cloud provider or API route, include at least one happy-path test and one failure test.

Run the full test suite:

```bash
pytest
```

Run only fast unit tests:

```bash
pytest -m "not integration"
```

---

## Documentation

Documentation lives in the `docs/` folder and is built with [Mintlify](https://www.mintlify.com/).

<Steps>
  <Step title="Install Mintlify CLI">
    ```bash
    npm install -g mintlify
    ```
  </Step>
  <Step title="Preview Docs Locally">
    ```bash
    mintlify dev
    ```
  </Step>
  <Step title="Add / Update Pages">
    Create or edit `.mdx`/`.md` files under `docs/` following the existing structure. Make sure to add your page to `mint.json` **navigation** if it should appear in the sidebar.
  </Step>
</Steps>

When you introduce a new user-facing capability (e.g., the FastAPI server or a new cloud deployment target), **create a dedicated docs page** and cross-link it from relevant sections.

---

## Pull Request Checklist

<Checklist>
  <Check icon="check">Code builds & tests pass (`pytest`)</Check>
  <Check icon="check">Documentation updated</Check>
  <Check icon="check">Linters/formatters run</Check>
  <Check icon="check">Commits follow Conventional Commits</Check>
</Checklist>

---

## Commit Message Convention

We follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style (formatting) changes
- `refactor:` Code refactor (no behaviour change)
- `test:` Adding or updating tests
- `chore:` Build processes or auxiliary tooling

Example:

```bash
feat(api): add OpenAI-compatible /chat/completions route
```

---

## License

By contributing, you agree that your contributions will be licensed under the **Apache 2.0 License**.

---

## Questions?

Feel free to contact us at [support@slashml.com](mailto:support@slashml.com) or join the discussion on GitHub.
