### Magemaker Documentation

This repository contains the **documentation site** for [Magemaker](https://github.com/slashml/magemaker).  
If you are looking for the actual source-code, visit the Magemaker repo above.  

---

## Local Development Workflow

Follow the steps below to preview documentation updates or to add new pages.

### 1. Install Mintlify CLI

We use the [Mintlify CLI](https://www.npmjs.com/package/mintlify) to run the docs locally.

```bash
npm i -g mintlify   # requires Node >= 16
```

<Note>
If you receive a "command not found" error after installation, make sure your global npm
bin folder is in your $PATH.
</Note>

### 2. Start the Docs Site

Run the following command from the root of the documentation repository (the folder that
contains `mint.json`).

```bash
mintlify dev
```

This spins-up a hot-reloading server at `http://localhost:3000` where you can preview your
changes.

### 3. Update / Add Pages

1. Create or edit `.mdx` / `.md` files inside the docs tree (see `mint.json` for the
   navigation structure).  
2. Follow the existing component conventions (front-matter, `<Card/>`, `<Steps/>`, etc.).  
3. Commit the new/updated files and open a Pull Request.

### Troubleshooting

• **`mintlify dev` isn’t running** – Execute `mintlify install` to re-install
  dependencies.  
• **404 after launch** – Make sure you are in the directory that contains
  `mint.json`.  
• **Styles/components look off** – Delete the `node_modules` folder and run
  `mintlify install` again.


---

## Contributing Docs

See the main project’s **Contributing** guide for coding standards. When updating docs:

1. Ensure every new feature in the code-base has at least one corresponding docs page.
2. Cross-link related pages for better discoverability.
3. Run the full docs site locally (`mintlify dev`) and verify:
   • Navigation entry exists.  
   • No broken links / images.  
   • Dark-mode renders correctly.

<Warning>
Never commit secrets or `.env` files to the documentation repository.
</Warning>


## Related Resources

• **Production Docs Site:** <https://magemaker.slashml.com>  
• **API Proxy Docs:** Newly added – see "Core Concepts → API Proxy" in the left sidebar for
  information on the FastAPI server included with Magemaker.

---

Happy documenting! 🎉