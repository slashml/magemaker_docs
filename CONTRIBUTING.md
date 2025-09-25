---
title: CONTRIBUTING
description: How to contribute to Magemaker
"og:title": "Contributing to Magemaker"
---

## Contributing to Magemaker

We love your input! We want to make contributing to Magemaker as easy and transparent as possible, whether it's:

- Reporting a bug
- Discussing the current state of the code or documentation
- Submitting a fix
- Proposing new features
- Becoming a maintainer

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
2. If you've added code that should be tested, add tests (`pytest`)
3. If you've changed APIs or behaviour, update the documentation (`.mdx` files)
4. Ensure the test suite passes: `pytest`
5. Make sure your code lints: `black . && isort . && flake8`
6. Open that pull request!

<Card title="Creating a pull request" icon="github" href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request">
  Create a Pull Request to propose and collaborate on changes to a repository.
</Card>

## Local Development Workflow

<Steps>
  <Step title="Clone & Install">
    ```bash
    git clone https://github.com/slashml/magemaker.git
    cd magemaker
    # Install core + dev dependencies
    pip install -e ".[dev]"
    ```
  </Step>
  <Step title="Run Unit Tests">
    ```bash
    pytest -q
    ```
  </Step>
  <Step title="Run the Local API Server (Optional)">
    ```bash
    uvicorn server:app --reload --port 8000
    ```
    The server exposes:
    - `GET /endpoint/{endpoint_name}` – Returns SageMaker endpoint metadata
    - `POST /endpoint/{endpoint_name}/query` – Sends an inference request
    - `POST /chat/completions` – OpenAI-compatible chat completion proxy
  </Step>
  <Step title="Preview Docs Changes">
    Install Mintlify CLI once:
    ```bash
    npm i -g mintlify
    ```
    Then run at repo root:
    ```bash
    mintlify dev
    ```
  </Step>
</Steps>

## Pull Request Guidelines

- <Icon icon="check" iconType="solid" /> Keep PRs small and focused
- <Icon icon="check" iconType="solid" /> Follow existing code style (`black`, `isort`, `flake8`)
- <Icon icon="check" iconType="solid" /> Include or update tests
- <Icon icon="check" iconType="solid" /> Update or create documentation pages for any new feature (see *Docs Style Guide* below)
- <Icon icon="check" iconType="solid" /> Write clear commit messages (Conventional Commits preferred)

### Docs Style Guide

1. All docs live in `docs/` or a top-level `.mdx` file.
2. Use MDX components already present in other pages (e.g. `<Card>`, `<Steps>`).
3. For a **brand-new feature**, create a new page under an appropriate folder (e.g. `concepts/`, `tutorials/`) and reference it in `mint.json` (navigation update will be reviewed during PR).
4. Screenshots should be placed in `docs/Images/` and referenced with a relative path.

## Commit Message Convention

We follow [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation only
- `style:` Formatting, missing semicolons, etc.
- `refactor:` Code change that neither fixes a bug nor adds a feature
- `test:` Adding or correcting tests
- `chore:` Build process or auxiliary tools changes

Example:
```bash
feat(api): add chat completions proxy endpoint
```

## License

By contributing, you agree that your contributions will be licensed under the Apache 2.0 License.

## Questions?

Feel free to contact us at [support@slashml.com](mailto:support@slashml.com) or join our [Discord](https://discord.gg/SBQsD63d) if you have any questions about contributing!
