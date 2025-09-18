---
title: CONTRIBUTING.md
description: How to contribute to Magemaker
"og:title": "Contributing to Magemaker"
---

## Contributing to Magemaker

We love your input! We want to make contributing to Magemaker as easy and transparent as possible, whether it's:

- Reporting a bug
- Discussing the current state of the code or docs
- Submitting a fix
- Proposing new features
- Becoming a maintainer

<Note>
  If you add a user-facing feature (e.g. a new CLI flag, REST route, or YAML option) **you must also update the documentation**. See “Documentation Changes” below.
</Note>

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
3. If you've changed APIs, update or create a docs page (see **Documentation Changes**)
4. Ensure the test suite passes: `pytest -q`
5. Run linters/formatters (`black . && isort . && flake8`)
6. Issue that pull request!

<Card title="Creating a pull request" icon="github" href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request">
  Create a Pull Request to propose and collaborate on changes to a repository.
</Card>

## Development Process

<Steps>
  <Step title="Fork & Clone">
    ```bash
    git clone https://github.com/YOUR_USERNAME/magemaker.git
    cd magemaker
    ```
  </Step>
  <Step title="Install Runtime & Dev Dependencies">
    ```bash
    # main requirements + dev extras
    pip install -e ".[dev]"
    ```
  </Step>
  <Step title="Run Tests & Linters">
    ```bash
    pytest -q            # run unit + integration tests
    black --check .      # format check
    flake8               # style check
    ```
  </Step>
  <Step title="Docs Preview (optional but recommended)">
    ```bash
    npm i -g mintlify   # once
    mintlify dev        # hot-reload docs server
    ```
  </Step>
</Steps>

## Documentation Changes

Magemaker’s docs are written in **MDX** and served by [Mintlify](https://mintlify.com/).

1. New pages should live under an existing logical folder (e.g. `concepts/`, `tutorials/`) and be linked in `mint.json`.
2. Use the existing front-matter style:
   ```mdx
   ---
   title: Awesome Feature
   description: Short description here
   ---
   ```
3. Keep tone & components consistent (Cards, Steps, Notes, etc.).
4. Run `mintlify dev` locally to preview.

<Warning>
  A PR that adds a new feature without updating docs **will not be merged**.
</Warning>

### Updating the API Reference
The FastAPI server (see `server.py`) exposes REST routes such as `/chat/completions` and `/endpoint/{endpoint_name}`. If you modify or add routes, update `concepts/api.mdx` accordingly and include example requests.

## Pull Request Checklist

- <Icon icon="check" iconType="solid" /> Code builds & tests pass
- <Icon icon="check" iconType="solid" /> New/updated tests added when appropriate
- <Icon icon="check" iconType="solid" /> Docs updated (or not needed)
- <Icon icon="check" iconType="solid" /> Follows [Conventional Commits](https://www.conventionalcommits.org/)

## Commit Message Convention

We follow the Conventional Commits spec:

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation only changes
- `style:` Code style updates (formatting, missing semicolons, etc.)
- `refactor:` Code change that neither fixes a bug nor adds a feature
- `test:` Adding or correcting tests
- `chore:` Other changes that don’t modify src or test files

Example:
```bash
git commit -m "feat(api): add /v1/embeddings route"
```

## License

By contributing, you agree that your contributions will be licensed under the **Apache 2.0 License**.

## Questions?

Feel free to contact us at [support@slashml.com](mailto:support@slashml.com) if you have any questions about contributing!
