[![REUSE Compliance](https://github.com/noi-techpark/opendatahub-docs-v2/actions/workflows/reuse-lint.yml/badge.svg)](https://github.com/noi-techpark/opendatahub-docs/wiki/REUSE#badges)

Open Data Hub Documentation
=============================

This repository contains documentation about the Open Data Hub project.

Note: If you experience any issue when using the APIs (like e.g., endpoints down or throwing errors, query outcome not meeting the expected result), please send an email directly to help@opendatahub.com. Your feedback or request will be processed directly by the Customer Care Team and you will likely receive a quick response!

# Website

This website is built using [Docusaurus](https://docusaurus.io/), a modern static website generator.

## Installation

```bash
yarn
npm i --legacy-peer-deps
```

## Local Development

```bash
yarn start
npm run start
```

This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server.

## Build

```bash
yarn build
npm run build
```

This command generates static content into the `build` directory and can be served using any static contents hosting service.

## Docs to PDF

Below are the commands to generate a PDF starting from Docusaurus. The plugin is a scraper which navigates the documentation using "next buttons" in the footer of the page.

https://github.com/jean-humann/docs-to-pdf

```
npm install -g docs-to-pdf
```

```
npx docs-to-pdf docusaurus --initialDocURLs="[url_of_page_you_want_scrape_from]" --contentSelector="article"  --paginationSelector="a.pagination-nav__link.pagination-nav__link--next"
```

## Deployment

### GitHub Actions

| Workflow | Trigger | Description |
| :--- | :--- | :--- |
| `deploy-typesense.yml` | Manual (environment: test/prod) | Deploy Typesense server to Docker runner |
| `index-docs.yml` | Manual / Tag `v*` (prod) / Tag `rc*` (test) | Run DocSearch scraper to index documentation |

### Required Secrets

| Secret | Description |
| :--- | :--- |
| `TYPESENSE_API_KEY_TEST/PROD` | Admin API key for Typesense (scraper) |
| `TYPESENSE_SEARCH_ONLY_API_KEY_TEST/PROD` | Search-only API key (frontend) |
| `SSH_PRIVATE_KEY` | SSH key for deployment |
| `GH_PERSONAL_ACCESS_TOKEN` | GitHub token for Docker registry |
| `AWS_S3_ACCESS_KEY_ID` | AWS S3 access key |
| `AWS_S3_SECRET_ACCESS_KEY` | AWS S3 secret key |

Note: Typesense hosts are configured as env variables in the workflow files.

### Deployment Flow

1. **Deploy Typesense**: Run `deploy-typesense.yml` manually, selecting environment
2. **Deploy Documentation**: Deploy the Docusaurus site (separate workflow)
3. **Index Documentation**:
   - Automatically triggered on `v*` tags (prod) or `rc*` tags (test)
   - Or run `index-docs.yml` manually after deployment



*****

**Note:** If you experience any issue when using the APIs (like e.g.,
endpoints down or throwing errors, query outcome not meeting the
expected result), please send an email directly to
help@opendatahub.com. Your feedback or request will be processed
directly by the Customer Care Team and you will likely receive a quick
response!

### REUSE

This project is [REUSE](https://reuse.software) compliant, more information about the usage of REUSE in NOI Techpark repositories can be found [here](https://github.com/noi-techpark/odh-docs/wiki/Guidelines-for-developers-and-licenses#guidelines-for-contributors-and-new-developers).

Since the CI for this project checks for REUSE compliance you might find it useful to use a pre-commit hook checking for REUSE compliance locally. The [pre-commit-config](.pre-commit-config.yaml) file in the repository root is already configured to check for REUSE compliance with help of the [pre-commit](https://pre-commit.com) tool.

Install the tool by running:
```bash
pip install pre-commit
```
Then install the pre-commit hook via the config file by running:
```bash
pre-commit install
```
