# Brutal

Brutal is a clean, responsive theme based on the Hugo theme with the same name featuring categories, tags and pagination.

## Contents

- [Installation](#installation)
- [Options](#options)
  - [Top menu](#top-menu)
  - [Title](#title)

## Installation

I prefer adding the theme as a submodule

```bash
$ git submodule add https://github.com/maxild/zola-brutal-theme.git themes/brutal
```

and then enable it in your `config.toml`

```toml
theme = "brutal"
```

## Development

When developing the theme inside a container repository, where this repo is a submodule, there are a few basic rules to follow

- When pushing new commits to the master branch of the brutal theme repo, then the
container repo is tracking the old commit/sha1 in its object database unless we remember to update the commit/sha1 as seen on the last line in the following bash code

```bash
$ cd themes/brutal
# Local work, and then
$ git commit -am "Update to brautal theme: blah blah blah"
$ git push
$ cd -
$ git commit -am "Updated brutal theme to: blah blah blah"
```

> Note that we always push submodule changes first (see above).

- When grabbing external updates to the theme repository the following commands are used

```bash
$ git pull
# The following is equivalent to running `git pull` in the themes/brutal submodule
$ git submodule update --remote
```

> NOTE: From here on the content is from the Even themes readme...

The theme requires tags and categories taxonomies to be enabled in your `config.toml`:

```toml
taxonomies = [
    # You can enable/disable RSS
    {name = "categories", rss = true},
    {name = "tags", rss = true},
]
```

If you want to paginate taxonomies pages, you will need to overwrite the templates
as it only works for non-paginated taxonomies by default.

It also requires to put the posts in the root of the `content` folder and to enable pagination, for example in `content/_index.md`:

```markdown
+++
paginate_by = 5
sort_by = "date"
+++
```

## Options

### Top-menu

Set a field in `extra` with a key of `even_menu`:

```toml
# This is the default menu
even_menu = [
    {url = "$BASE_URL", name = "Home"},
    {url = "$BASE_URL/categories", name = "Categories"},
    {url = "$BASE_URL/tags", name = "Tags"},
    {url = "$BASE_URL/about", name = "About"},
]
```

If you put `$BASE_URL` in a url, it will automatically be replaced by the actual
site URL.

### Title

The site title is shown on the header. As it might be different from the `<title>`
element that the `title` field in the config represents, you can set the `even_title`
instead.

### KaTeX math formula support

This theme contains math formula support using [KaTeX](https://katex.org/),
which can be enabled by setting `katex_enable = true` in the `extra` section
of `config.toml`:

```toml
[extra]
katex_enable = true
```

After enabling this extension, the `katex` short code can be used in documents:

- `{{ katex(body="\KaTeX") }}` to typeset a math formula inlined into a text,
  similar to `$...$` in LaTeX
- `{% katex(block=true) %}\KaTeX{% end %}` to typeset a block of math formulas,
  similar to `$$...$$` in LaTeX

#### Automatic rendering without short codes

Optionally, `\\( \KaTeX \\)` inline and `\\[ \KaTeX \\]` / `$$ \KaTeX $$`
block-style automatic rendering is also supported, if enabled in the config:

```toml
[extra]
katex_enable = true
katex_auto_render = true
```
