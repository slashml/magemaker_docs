### Magemaker Documentation Repo

This repository contains **only the documentation** for the Magemaker project.  
The actual source code for Magemaker lives in the main repo:
[github.com/slashml/magemaker](https://github.com/slashml/magemaker).

---
## Local Docs Development

The docs are written in **Mintlify** (`.mdx` & `.md` files).  
Follow the steps below to preview changes locally.

### 1. Install the Mintlify CLI

```bash
npm i -g mintlify
```

> You need Node.js ≥ 18.x for the command above to work.

### 2. Start the Docs Dev-Server

From the root of the documentation folder (where `mint.json` lives):

```bash
mintlify dev
```

Mintlify will build the site and serve it at `http://localhost:3000` with hot-reload.

### 3. Troubleshooting

• **`mintlify dev` isn’t running** – run `mintlify install` to re-install deps.  
• **404 after reload** – ensure you’re inside the folder containing `mint.json`.  
• **Port already in use** – pass a different port: `mintlify dev --port 4000`.

---
## Contributing to the Docs

1. Fork the repo & create your branch: `git checkout -b docs/my-update`  
2. Make your edits / add new pages (follow existing style & front-matter).  
3. Preview with `mintlify dev`.  
4. Open a Pull Request against `main`.

### Writing Style

• Use American English.  
• Keep headings ≤ H3 where possible.  
• Use `<Note>`, `<Warning>`, `<Steps>`, and `<CardGroup>` components when helpful.  
• All code blocks MUST be fenced with the correct language for syntax-highlighting.

### When You Add New Features to Code

If the implementation introduces a **new public-facing capability** (CLI flag, API route, env-var, etc.) you **must**:

1. Create a new `.mdx` page that documents it.  
2. Update `mint.json` navigation if needed.  
3. Link to the new page from at least one existing doc (Quick-Start, Concepts, or Tutorials).

---
## NEW – OpenAI-Compatible Proxy Docs

Magemaker now ships a **FastAPI server** (`server.py`) that exposes OpenAI-style chat completions on top of your SageMaker endpoints.  
The full usage guide lives in the new page:  
`/concepts/openai-proxy` – please read it and keep it updated if you touch `server.py`.

---
## Need Help?

Open a discussion on GitHub or email us at **support@slashml.com**.
