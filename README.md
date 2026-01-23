# python-docs-offline
Offline builds of Python documentation in various formats:
* PDF
* Zipped offline HTML
* Plain text
* Texinfo
* EPUB

## Rejected idea

I wanted to present a waiting page in place(s) of file(s) that are being generated, that would render similarly to 404 page.
But [GitHub Pages don't give control over HTTP headers](https://github.com/orgs/community/discussions/54257), i.e. Content-Type header, where I'd like to set
Content-Type: text/html to present a page at the URL that ends with `.zip`. In practice browser wants to download such page always.

Therefore I'm going to strip this functionality from the project. To improve, we
* either need a different backend than GH Pages (to control Content-Type header)
* or this project would need to generate the entire downloads page.
