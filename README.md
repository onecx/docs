# docs
OneCX Documentation

## Working with Local Copies

1. Adjust urls in antora-playbook.yml:

The main documentation repository contains a list of sources that reference remote repositories via their `url` properties. To use local changes during development, you need to replace these remote URLs with your local file paths.

If you made changes to documentation in the `onecx-local-env` repository, in the `antora-playbook.yml` replace:

```yaml
 - url: https://github.com/onecx/onecx-local-env.git
      branches: [HEAD]
      start_path: docs
```

with:

```yaml
 - url: /path/to/your/local/onecx-local-env
      branches: [HEAD]
      start_path: docs
```

Additionally, update the path to the main docs repository to your local path by changing:

```yaml
content:
  sources:
    - url: .
```

to:

```yaml
content:
  sources:
    - url: /path/to/your/local/docs/repo
```

2. Build the documentation:

```bash
npx antora antora-playbook.yml
```

3. Viewing Local Changes:

After a successful build, a `build` directory will be created in the main documentation root. This directory contains all the files needed to display the complete documentation site.

To access the index.html, open the following file in your browser:

file://wsl.localhost/wsldev/your-path-to-docs-repo/docs/build/site/documentation/current/index.html

Replace `/path/to/your/docs/repo` with the actual path to your local docs repository.

Now you can navigate to the relevant pages and view your local changes.