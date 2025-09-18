### Magemaker Documentation Repository

This repository contains the source files that power the public Magemaker docs site – [https://magemaker.slashml.com](https://magemaker.slashml.com).

If you are **updating or adding documentation** please work inside this repo, **not** the main `slashml/magemaker` code repository.

---

## Local Development

Magemaker docs are built with **[Mintlify](https://docs.mintlify.com/)**. Use the Mintlify CLI to preview changes locally before you open a pull-request.

1. Install the CLI (requires Node.js ≥ 16):

   ```bash
   npm install -g mintlify
   ```

2. From the root of this repository start the local dev server:

   ```bash
   mintlify dev
   ```

3. Open `http://localhost:3000` in your browser – changes hot-reload automatically.

### Common Issues

| Symptom                                  | Fix                                              |
| ---------------------------------------- | ------------------------------------------------- |
| `mintlify` command not found             | Run `npm i -g mintlify`                           |
| 404 when dev server starts               | Ensure you are in the folder that contains `mint.json` |
| Build fails after adding new dependencies | Run `mintlify install` to regenerate the lock-file |

---

## Folder Structure

```
.
├── about.mdx
├── concepts/
│   ├── api.mdx            # ← NEW – API reference for FastAPI proxy
│   ├── deployment.mdx
│   └── …
├── configuration/
│   └── …
├── tutorials/
│   └── …
└── mint.json
```

*Pages inside `concepts`, `tutorials`, and `configuration` are automatically
collected by Mintlify. When you add a new page remember to update the
`navigation` section of **mint.json** so the page appears in the sidebar.*

---

## Adding / Updating Docs

1. Create or edit an `.mdx` or `.md` file.
2. Add front-matter:

   ```yaml
   ---
   title: My New Page
   description: Short one-sentence description
   ---
   ```

3. Preview locally (`mintlify dev`) and confirm links / images work.
4. If you introduced new functionality in `slashml/magemaker` **also add docs** for it here (see the newly-added `concepts/api.mdx` for an example).
5. Commit using [Conventional Commits](https://www.conventionalcommits.org/) conventions, open a PR, and request review.

---

## Reference Links

* Main codebase – <https://github.com/slashml/magemaker>
* Live documentation – <https://magemaker.slashml.com>
* Contribution guidelines – [`CONTRIBUTING.md`](./CONTRIBUTING.md)
* **NEW** – FastAPI / OpenAI-style proxy reference – [`concepts/api.mdx`](./concepts/api.mdx)
