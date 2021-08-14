# Congo

Congo is designed to be a fast, lightweight theme for Hugo. It's based upon Tailwind CSS with a clean and minimalist design.

[View Demo site](https://jpanther.github.io/Congo/)

![Screenshot](https://raw.githubusercontent.com/jpanther/Congo/stable/images/screenshot.png)

## Features

- Built with Tailwind CSS JIT for minified stylesheets without any excess code
- Fully responsive layout
- Dark mode (auto-switching based upon browser)
- Highly customisable configuration
- Flexible with any content types, taxonomies and menus
- Diagrams and visualisations using Mermaid JS
- SVG icons from FontAwesome 5
- Heading anchors
- HTML and Emoji support in articles
- SEO friendly
- Fathom Analytics and Google Analytics support
- Favicons support
- Comments support
- Advanced customisation using simple Tailwind colour definitions and styles
- Well documented (see below)

---

## Documentation

### Table of Contents

- [Congo](#congo)
  - [Features](#features)
  - [Documentation](#documentation)
    - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
    - [1. Install Hugo](#1-install-hugo)
    - [2. Create a new site](#2-create-a-new-site)
    - [3. Download the Congo theme](#3-download-the-congo-theme)
      - [Install using git](#install-using-git)
      - [Install manually](#install-manually)
    - [4. Set up your configuration files](#4-set-up-your-configuration-files)
  - [Configuration](#configuration)
    - [Getting started](#getting-started)
    - [Organising content](#organising-content)
  - [Shortcodes](#shortcodes)
    - [Alert](#alert)
    - [Icon](#icon)
    - [Lead](#lead)
    - [Mermaid](#mermaid)
  - [Partials](#partials)
    - [Analytics.html](#analyticshtml)
      - [Fathom Analytics](#fathom-analytics)
      - [Google Analytics](#google-analytics)
      - [Custom analytics providers](#custom-analytics-providers)
    - [Comments.html](#commentshtml)
    - [Favicons.html](#faviconshtml)
    - [Icon.html](#iconhtml)
    - [Extend-head.html and Extend-footer.html](#extend-headhtml-and-extend-footerhtml)
  - [Advanced customisation](#advanced-customisation)
  - [Contributing](#contributing)
    - [Bugs & Suggestions](#bugs--suggestions)

---

## Installation

Simply follow the standard Hugo [Quick Start](https://gohugo.io/getting-started/quick-start/) procedure to get up and running quickly.

Detailed instructions can be found below.

### 1. Install Hugo

You can find specific instructions for your platform in the official [Hugo docs](https://gohugo.io/getting-started/installing.).

Make sure you are using **Hugo version 0.86.1** or later as the theme takes advantage of some of the latest Hugo features.

### 2. Create a new site

Run the command `hugo new site mywebsite` to create a new Hugo site in a folder named `mywebsite`.

### 3. Download the Congo theme

There are a couple of ways to install the Congo theme into your Hugo website. The git method is the easiest to keep the theme up-to-date, but you can also download and install manually if you don't have git available.

#### Install using git

Change into the directory for your Hugo website, initialise a new repository and add Congo as a submodule.

```bash
cd mywebsite
git init
git submodule add https://github.com/jpanther/Congo.git themes/congo
```

_**Note:** You need to substitute `mywebsite` for the correct folder name you used in Step 2._

#### Install manually

Download the latest version of the theme from: [https://github.com/jpanther/Congo/archive/stable.zip](https://github.com/jpanther/Congo/archive/stable.zip)

Extract the archive and you should have a folder named `Congo-stable`.

Rename the folder to `congo` and move it to the `themes/` directory inside your `mywebsite` folder.

_**Note:** You need to substitute `mywebsite` for the correct folder name you used in Step 2._

### 4. Set up your configuration files

In the root folder of your website, delete the `config.toml` file that was generated by Hugo. Copy the entire `themes/congo/config/` folder into the root of your website. This will ensure you have all the correct theme settings and will enable you to easily customise the theme.

You're now all set up to use Congo. From here you can add some content and start the Hugo server.

Refer to the Hugo docs for more information or read the next section to learn more about configuring the theme.

## Configuration

Congo is a highly customisable theme and uses some of the latest Hugo features to simplify how it is configured.

The theme ships with a default configuration that gets you up and running with a basic blog or static website. This default configuration can be found in the `themes/congo/config/_default/` folder.

> Configuration files bundled with the theme are provided in TOML format as this is the default Hugo syntax. Feel free to convert your config to YAML or JSON as you wish.

The default theme configuration is documented in each file so you can freely adjust the settings to meet your needs.

### Getting started

The config files that ship with Congo contain all of the possible settings that the theme recognises. By default, many of these are commented out but you can simply uncomment them to activate or change a specific feature.

A few things you need to set for a new installation:

```toml
# config/_default/config.toml

baseURL = "https://your_domain.com"
languageCode = "en-AU"

title = "My awesome website"
```

It's also useful to set the author configuration in the `config/_default/author.toml` file. You can also add links to your profiles here to enable them in the theme.

```toml
# config/_default/author.toml

[author]
name = "Your name"
twitter = "https://twitter.com/username"
```

### Organising content

By default, Congo doesn't force you to use a particular content type. In doing so you are free to define your content as you wish. You might prefer _pages_ for a static site, _posts_ for a blog, or _projects_ for a portfolio.

The same logic applies to taxonomies. Some people prefer to use _tags_ and _categories_, others prefer to use _topics_.

Hugo defaults to using posts, tags and categories out of the box and this will work fine if that's what you want. If you wish to customise this, however, you can do so by creating the following files:

```toml
# config/_default/taxonomies.toml

topic = "topics"
```

This will replace the default _tags_ and _categories_ with _topics_. Refer to the [Hugo Taxonomy docs](https://gohugo.io/content-management/taxonomies/) for more information on naming taxonomies.

When you create a new taxonomy, you will need to adjust the navigation links on the website to point to the new sections:

```toml
# config/_default/menus.toml

[[main]]
  name = "Blog"
  pageRef = "posts"
  weight = 10

[[main]]
  name = "Topics"
  pageRef = "topics"
  weight = 20
```

## Shortcodes

In addition to all the [default Hugo shortcodes](https://gohugo.io/content-management/shortcodes/), Congo adds a few extras for additional functionality.

### Alert

`alert` outputs its contents as a stylised message box within your article. It's useful for drawing attention to important information that you don't want the reader to miss.

The input is written in Markdown so you can format it however you please.

**Usage:**

```md
{{< alert >}}
**Warning!** This action is destructive!
{{< /alert >}}
```

### Icon

`icon` outputs an SVG icon and takes the icon name as its only parameter. The icon is scaled to match the current text size.

**Usage:**

```md
{{< icon "github" >}}
```

Icons are populated using Hugo pipelines which makes them very flexible. Congo ships with a default set of icons for social, email, and generic links. If you want to add your own icons, you can simply place them in `/assets/icons/` and reference them using the `icon` shortcode passing in the icon's filename (without the `.svg.` extension).

Icons can also be used in partials by calling the [`icon.html` partial](#iconhtml).

### Lead

`lead` is used to bring emphasis to the start of an article. It can be used to style an introduction, or to call out an important piece of information. Simply wrap any Markdown content in the `lead` shortcode.

```md
{{< lead >}}
When life gives you lemons, make lemonade.
{{< /lead >}}
```

### Mermaid

`mermaid` allows you to draw detailed diagrams and visualisations using text. It uses MermaidJS under the hood and supports a wide variety of diagrams, charts and other output formats.

Simply write your Mermaid syntax within the `mermaid` shortcode and let the plugin do the rest.

**Usage:**

```md
{{< mermaid >}}
graph LR;
A[Lemons]-->B[Lemonade];
B-->C[Profit]
{{< /mermaid >}}
```

Refer to the [official Mermaid docs](https://mermaid-js.github.io/) for details on syntax and supported diagram types.

## Partials

### Analytics.html

Congo provides built-in support for Fathom Analytics and Google Analytics. Fathom is a paid alternative to Google Analytics that respects user privacy. If you're interested you can [receive $10 credit](https://usefathom.com/ref/RLAJSV) and try the service.

> **Note:** This is an affiliate link but helps to support the development of Congo.

#### Fathom Analytics

To enable Fathom Analytics support, simply provide your Fathom site code in the `config/_default/params.toml` file. If you also use the custom domain feature of Fathom and would like to serve their script from your domain, you can also additionally provide the `domain` configuration value. If you don't provide a `domain` value, the script will load directly from Fathom DNS.

```toml
# config/_default/params.toml

[fathomAnalytics]
  site = "ABC12345"
  domain = "llama.yoursite.com"
```

#### Google Analytics

Google Analytics support is provided through the internal Hugo partial. Simply provide the `googleAnalytics` key in the `config/_default/config.toml` file and the script will be added automatically.

```toml
# config/_default/config.toml

googleAnalytics = "UA-PROPERTY_ID"
```

#### Custom analytics providers

If you wish to use a different analytics provider on your website you can also override the analytics partial and provide your own script. Simply create the file `layouts/partials/analytics.html` in your project and it will automatically include it in the `<head>` of the website.

### Comments.html

To add comments to your articles, Congo includes support for a comments partial that is included at the base of each article page. Simply provide a `layouts/partials/comments.html` which contains the code required to display your chosen comments.

You can use either the built-in Hugo Disqus template, or provide your own custom code. Refer to the [Hugo docs](https://gohugo.io/content-management/comments/) for further information.

### Favicons.html

Congo provides a default set of blank favicons to get started but you can provide your own assets to override them. The easiest way to obtain new favicon assets is to generate them using a third-party provider like [favicon.io](https://favicon.io).

Icon assets should be placed directly in the `static/` folder of your website and named as per the listing below. If you use [favicon.io](https://favicon.io), these will be the filenames that are automatically generated for you, but you can provide your own assets if you wish.

```shell
static/
├─ android-chrome-192x192.png
├─ android-chrome-512x512.png
├─ apple-touch-icon.png
├─ favicon-16x16.png
├─ favicon-32x32.png
├─ favicon.ico
└─ site.webmanifest
```

Alternatively, you can also completely override the default favicon behaviour and provide your own favicon HTML tags and assets. Simply provide a `layouts/partials/favicons.html` file in your project and this will be injected into the site `<head>` in place of the default assets.

### Icon.html

Similar to the [icon shortcode](#icon), you can include icons in your own templates and partials by using Congo's `icon.html` partial. The partial takes one parameter which is the name of the icon to be included.

**Usage:**

```go
  {{ partial "icon.html" "github" }}
```

Congo includes a number of built-in icons for social, links and other purposes. You can also provide your own icon assets by including the SVG in `assets/icons/`.

### Extend-head.html and Extend-footer.html

The theme allows for inserting additional code directly into the `<head>` and `<footer>` sections of the template. These can be useful for providing scripts or other logic that isn't part of the theme.

Simply create either `layouts/partials/extend-head.html` or `layouts/partials/extend-footer.html` in your site folder and these will automatically be included in your website build. Both partials are injected as the last items in `<head>` and `<footer>` so they can be used to override theme defaults.

## Advanced customisation

There are a couple of ways you can make style changes to Congo.

If you just need to add or override some simple styles, you can do so by creating a `custom.css` file in your project's `static/css/` folder. This file will be loaded automatically after the theme's default styles.

Alternatively, if you'd like to make a major change, you can take advantage of Tailwind CSS's JIT compiler and rebuild the entire theme CSS from scratch.

> **Note:** Building the theme manually is intended for advanced users.

Change into the `themes/congo/` folder and install the project dependencies.

```bash
npm install
```

Once installed, you can edit the `themes/congo/tailwind.config.js` to change the styles that are applied throughout the theme. You can also adjust specific styles in `themes/congo/assets/css/main.css`.

To allow for easy theme colour changes, Congo defines a `primary` and `secondary` colour palette that is used throughout the theme. In order to change the colour across the entire theme, simply edit the `tailwind.config.js` file accordingly.

For example, to change to a green colour scheme, you could apply these changes:

```js
  // themes/congo/tailwind.config.js

  theme: {
    colors: {
      transparent: "transparent",
      white: colors.white,
      gray: colors.gray,
      primary: colors.lime,
      secondary: colors.teal,
    },
    ...
  }
```

For a full list of colours available, and their corresponding configuration values, see the official [Tailwind docs](https://tailwindcss.com/docs/customizing-colors#color-palette-reference).

After editing the configuration, you need to rebuild the theme's stylesheets.

```bash
npm run build
```

This will automatically output a minified CSS file to `/themes/congo/static/css/main.css`.

To aid with testing style changes, you can also run the Tailwind JIT comiler in watch mode.

```bash
npm run dev
```

Now whenever you make a change, the (non-minified) CSS files will be rebuilt automatically. This mode is useful to run when using `hugo server` to preview your site during development. Remember to perform a full build before publishing your website.

## Contributing

Congo is still very much a work in progress. I intend to keep adding features and making changes as required.

### Bugs & Suggestions

Feel free to get in touch with any issues or suggestions for new features you'd like to see. Please use GitHub issues for all bug reports and suggestions to help keep everything in one spot.

If you're able to fix a bug or implement a new feature, I welcome PRs for this purpose.

All development occurs on the `dev` branch and new PRs should be forked from here.
