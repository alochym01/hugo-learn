# Hugo Themes

## Create Hugo Themes

1. Create new themes - `hugo new theme basic`

    ```bash
    themes/
    └── basic
        ├── archetypes
        │   └── default.md
        ├── layouts
        │   ├── 404.html
        │   ├── _default
        │   │   ├── baseof.html # the skeleton for using content block and partials
        │   │   ├── list.html
        │   │   └── single.html
        │   ├── index.html
        │   └── partials
        │       ├── footer.html
        │       ├── header.html
        │       └── head.html
        ├── LICENSE
        ├── static
        │   ├── css
        │   └── js
        └── theme.toml
    ```

1. Using theme by editing config.toml

    ```bash
    baseURL = 'http://example.org/'
    languageCode = 'en-us'
    title = 'My New Hugo Site'
    theme = "basic" # using new theme
    ```

## Using Content Blocks and Partials

1. Create custom css:
    1. `portfolio/themes/basic/static/css/bootstrap.min.css`
    1. `portfolio/themes/basic/static/css/headers.css`

1. Create custom javascript
    1. `portfolio/themes/basic/static/js/bootstrap.min.js`
    1. `portfolio/themes/basic/static/js/popper.min.js`

1. `portfolio/themes/basic/layouts/_default/baseof.html` - the skeleton of content block and partials
1. the `portfolio/themes/basic/layouts/_default/baseof.html` content

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <!-- {{- Placing a dash after the opening braces removes all whitespace in front of the expression -->
            <!-- -}} placing the dash in front of the closing braces removes whitespace after the expression. -->
            {{- partial "head.html" . -}}
        </head>
        <body>
            <div class="container">
                <header>
                    {{- partial "header.html" . -}}
                </header>
            </div>

            <div class="container">
                {{- partial "nav.html" . -}}
            </div>
            <div class="container">
                <!-- portfolio/themes/basic/layouts/index.html for home page -->
                <!-- portfolio/themes/basic/layouts/_default/single.html for single page -->
                {{- block "main" . }}{{- end }}
                <footer>
                    {{- partial "footer.html" . -}}
                </footer>
            </div>
            {{- partial "js.html" . -}}
        </body>
    </html>
    ```

1. `portfolio/themes/basic/layouts/partials/head.html` content

    ```html
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- The relURL function creates site-root-relative link to the file instead of an -->
    <!-- absolute link that contains the site's domain name -->
    <link rel="stylesheet" href='{{ "css/bootstrap.min.css" | relURL }}'>
    <link rel="stylesheet" href='{{ "css/header.css" | relURL }}'>
    <title>{{ .Site.Title }}</title>
    ```

1. `portfolio/themes/basic/layouts/partials/header.html`

    ```html
    <h1>{{ .Site.Title }}</h1>
    ```

1. `portfolio/themes/basic/layouts/partials/nav.html`

    ```html
    <header class="d-flex justify-content-center py-3">
        <ul class="nav nav-pills">
            <li class="nav-item"><a href="/" class="nav-link active" aria-current="page">Home</a></li>
            <li class="nav-item"><a href="/resume" class="nav-link">Résumé</a></li>
            <li class="nav-item"><a href="/contact" class="nav-link">Contact</a></li>
            <li class="nav-item"><a href="/about" class="nav-link">About</a></li>
        </ul>
    </header>
    ```

1. `portfolio/themes/basic/layouts/partials/footer.html`

    ```html
    <small>Copyright {{now.Format "2006"}} Me.</small>
    ```

1. `portfolio/themes/basic/layouts/partials/js.html`

    ```html
    <!-- The relURL function creates site-root-relative link to the file instead of an -->
    <!-- absolute link that contains the site's domain name -->
    <script src='{{ "/js/popper.min.js" | relURL }}'></script>
    <script src='{{ "/js/bootstrap.min.js" | relURL }}'></script>
    ```

1. Create a `main` block `portfolio/themes/basic/layouts/index.html` for home layout page

    ```bash
    {{ define "main" }}
        {{ .Content }}
    {{ end }}
    ```

1. Create a `main` block `portfolio/themes/basic/layouts/_default/single.html` for single layout page

    ```bash
    {{ define "main" }}
        <h2>{{ .Title }}</h2>
        {{ .Content }}
    {{ end }}
    ```
