# python-docs-offline

Automated daily builds of Python documentation for offline use, published to
[GitHub Pages](https://m-aciek.github.io/python-docs-offline/).

## Available formats

* PDF
* Zipped offline HTML
* Plain text
* Texinfo
* EPUB

## Supported versions and languages

Builds are generated for all currently supported CPython versions (fetched
dynamically from the [Python release cycle](https://peps.python.org/api/release-cycle.json))
and all languages that are active in production on [docs.python.org](https://docs.python.org)
(fetched dynamically from [docsbuild-scripts config](https://github.com/python/docsbuild-scripts/blob/main/config.toml)).

## How it works

A scheduled GitHub Actions workflow runs daily. It queries the CPython release
cycle API and the docsbuild-scripts configuration to determine which
(version, language) combinations to build. Each combination is built using
the [build.yaml](.github/workflows/build.yaml) reusable workflow, which checks
out the CPython source, builds the documentation with Sphinx, and uploads the
resulting archives as artifacts. After all builds complete, a single deploy job
merges the artifacts into the `gh-pages` branch and publishes them to GitHub
Pages.

## Rejected idea

I wanted to present a waiting page in place(s) of file(s) that are being generated, that would render similarly to 404 page.
But [GitHub Pages don't give control over HTTP headers](https://github.com/orgs/community/discussions/54257), i.e. Content-Type header, where I'd like to set
Content-Type: text/html to present a page at the URL that ends with `.zip`. In practice browser wants to download such page always.

Therefore I'm going to strip this functionality from the project. To improve, we
* either need a different backend than GH Pages (to control Content-Type header)
* or this project would need to generate the entire downloads page.
