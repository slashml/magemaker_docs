### These are docs for the [Magemaker-Docs](https://magemaker.slashml.com) documentation site.

The source code of magemaker is located at [Magemaker](https://github.com/slashml/magemaker)

### Development

Install the [Mintlify CLI](https://www.npmjs.com/package/mintlify) to preview the documentation changes locally. To install, use the following command

```
npm i -g mintlify
```

you need to have Node.js installed to use npm.

Run the following command at the root of your documentation (where mint.json is)

```
mintlify dev
```

#### Troubleshooting

- Mintlify dev isn't running - Run `mintlify install` it'll re-install dependencies.
- Page loads as a 404 - Make sure you are running in a folder with `mint.json`

<!-- Updated by docsalot for PR #95 at 2025-10-16T00:47:43.861Z -->
