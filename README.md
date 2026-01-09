# OneCX Documentation

This repository contains the sources and configuration for the [OneCX Platform documentation site](https://onecx.github.io/docs/documentation/current/index.html) built with Antora. 
It contains some main modules and aggregates multiple modules from other OneCX repositories used to build and preview the docs.

Contents
- Antora playbook for CI builds
- Main navigation tree
- Modules:
  - OneCX platform overview including architecture
  - OneCX Applications overview
  - Guide how to write OneCX documentations
  - Guide how to start with OneCX
  - Entry point for all OneCX Development modules

Usage
- See documentation guide on https://onecx.github.io/docs/documentation/current/onecx-docs-doc/index.html

Quick Use
- Clone the repository locally
- Install Antora globally (optional):

```bash
npm install -g @antora/cli @antora/site-generator
```

- Build the site with fetching sources:

```bash
antora --fetch antora-playbook.yml
```

- Or use npx without global install:

```bash
npx antora --fetch antora-playbook.yml
```

