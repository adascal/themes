<p align="center">
  <a href="https://www.gatsbyjs.com">
    <img alt="Gatsby" src="https://www.gatsbyjs.com/Gatsby-Monogram.svg" width="60" />
  </a>
</p>
<h1 align="center">
  The Gatsby Blog theme
</h1>

A Gatsby theme for creating a blog.

## Installation

### For a new site

If you're creating a new site and want to use the blog theme, you can use the blog theme starter. This will generate a new site that pre-configures use of the blog theme.

```shell
gatsby new my-themed-blog https://github.com/gatsbyjs/gatsby-starter-blog-theme
```

### For an existing site

If you already have a site you'd like to add the blog theme to, you can manually configure it.

1. Install the blog theme

```shell
npm install gatsby-theme-blog
```

2. Add the configuration to your `gatsby-config.js` file

```js
// gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-blog`,
      options: {
        // basePath defaults to `/`
        basePath: `/blog`,
      },
    },
  ],
}
```

3. Add blog posts to your site by creating `md` or `mdx` files inside `/content/posts`.

   > Note that if you've changed the default `contentPath` in the configuration, you'll want to add your markdown files in the directory specified by that path.

4. Add an image with the file name `avatar` (can be jpg or png) inside the `/assets` directory to include a small image next to the footer on every post page.

> Note that if you've changed the default `assetPath` in the configuration, you'll want to add your asset files in the directory specified by that path.

5. Run your site using `gatsby develop` and navigate to your blog posts. If you used the above configuration, your URL will be `http://localhost:8000/blog`

## Usage

### Theme options

| Key                      | Default value            | Description                                                                                                                                                                                                                       |
| ------------------------ | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `basePath`               | `/`                      | Root url for all blog posts                                                                                                                                                                                                       |
| `contentPath`            | `content/posts`          | Location of blog posts                                                                                                                                                                                                            |
| `assetPath`              | `content/assets`         | Location of assets                                                                                                                                                                                                                |
| `mdxOtherwiseConfigured` | `false`                  | Set this flag `true` if `gatsby-plugin-mdx` is already configured for your site.                                                                                                                                                  |
| `preset`                 | `gatsby-theme-ui-preset` | Theme UI compatible package name that will act as the base styles for your project. Be sure to install the package you're referencing. Set to `false` to ignore all presets and only use local styles.                            |
| `prismPreset`            | `null`                   | Theme UI compatible package name that will act as the prism syntax highlighting for your project. Be sure to install the package you're referencing. For themes in `@theme-ui/prism` the name will suffice, e.g. `prism-okaidia`. |
| `excerptLength`          | `140`                    | Length of the auto-generated excerpt of a blog post                                                                                                                                                                               |
| `webfontURL`             | `''`                     | URL for the webfont you'd like to include. Be sure that your local theme does not override it.                                                                                                                                    |
| `imageMaxWidth`          | `1380`                   | Set the max width of images in your blog posts. This applies to your featured image in frontmatter as well.                                                                                                                       |

#### Example configuration

```js
// gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-blog`,
      options: {
        // basePath defaults to `/`
        basePath: `/blog`,
        prismPreset: `prism-okaidia`,
      },
    },
  ],
}
```

### Additional configuration

In addition to the theme options, there are a handful of items you can customize via the `siteMetadata` object in your site's `gatsby-config.js`

```js
// gatsby-config.js
module.exports = {
  siteMetadata: {
    // Used for the site title and SEO
    title: `My Blog Title`,
    // Used to provide alt text for your avatar
    author: `My Name`,
    // Used for SEO
    description: `My site description...`,
    // Used for resolving images in social cards
    siteUrl: `https://example.com`,
    // Used for social links in the root footer
    social: [
      {
        name: `Twitter`,
        url: `https://twitter.com/gatsbyjs`,
      },
      {
        name: `GitHub`,
        url: `https://github.com/gatsbyjs`,
      },
    ],
  },
}
```

### Blog Post Fields

The following are the defined blog post fields based on the node interface in the schema

| Field       | Type     |
| ----------- | -------- |
| id          | String   |
| title       | String   |
| body        | String   |
| slug        | String   |
| date        | Date     |
| tags        | String[] |
| excerpt     | String   |
| image       | String   |
| imageAlt    | String   |
| socialImage | String   |

### Image Behavior

Blog posts can include references to images inside frontmatter. Note that this works for a relative path as shown below, or an external URL.

```md
---
title: Hello World (example)
date: 2019-04-15
image: ./some-image.jpg
---
```

`image` refers to the featured image at the top of a post and is not required. It will also appear as the preview image inside a social card. Note that this requires you to set `siteUrl` in your `gatsby-config.js` file metadata to your site's domain.

When adding an `image`, `imageAlt` is available to provide alt text for the featured image within the post. If this is not included, it defaults to the post excerpt.

You may want to use a different image for social sharing than the one that appears in your blog post. You can do so by setting `socialImage` in frontmatter.

### How Styles work

This theme enables `gatsby-plugin-theme-ui` which allows you to leverage [Theme UI](https://theme-ui.com/) to style your project.

By default, `gatsby-theme-ui-preset` operates as your base theme styles. Any local shadowed styles deep merge with that preset.

Alternatively, you can pass a preset of your own choosing by installing the package and passing the package name as the `preset` in `gatsby-config.js`. Again, local shadowed styles will deep merge with this preset if they exist.

```js
// gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-blog`,
      options: {
        preset: `my-preset-name-here`,
      },
    },
  ],
}
```

If you'd rather use only local shadowed styles with no underlying preset, pass the `preset` option as `false`.

#### Prism

You can also configure your prism theme for syntax highlighting in code snippets by passing the `prismPreset` option.

`@theme-ui/prism` is included by default, so any [available presets](https://theme-ui.com/packages/prism#syntax-themes) can be passed using only their name, e.g. `dracula`.

```js
// gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-blog`,
      options: {
        prismPreset: `dracula`,
      },
    },
  ],
}
```

As an alternative, you can install a package with a prism theme into your project and pass the package name.

This option is null by default, and in all cases local shadowed styles take precedent.

##### Highlight Line

You can highlight code snippets using `// highlight line` or a combination of `// highlight-start` and `// highlight-end`.

To update the styling for these highlights override the `.highlight` styles inside your prism theme.

### Accessibility and Skip-nav

This theme comes equipt with [skip-nav](https://reacttraining.com/reach-ui/skip-nav/). Note that if you override `header.js` you'll need to add the `SkipNavLink` component yourself. Additionally, if you override `layout.js` you'll need to include `SkipNavContent` manually.

## Migration to 2.0

The 2.0 release includes breaking changes. Note that many of the changes are related to the default styling in the blog theme. If you have no interest in additional flexibility with styles the 1.6 release may be sufficient as it includes new features without the breaking changes.

Before upgrading to 2.0 you'll want to update your core `gatsby` version as well.

**Change in data structure** - Instead of querying for the `node` object inside the `edges` array, all queries now look for `nodes`. If you're shadowing files and accessing data directly you may need to account for this.

**Removal of darkmode toggle** - This theme no longer comes with a darkmode toggle. If you'd like to use the old one it is now available as a parallel theme you can install, [`gatsby-theme-blog-darkmode`](https://www.gatsbyjs.com/plugins/gatsby-theme-blog-darkmode/). Please see the README for further instructions.

### Style specific migration notes

With the new version of `gatsby-plugin-theme-ui` there are a number of changes to the way styles are passed and how they compose.

**Change in shadow structure** - When shadowing files in `gatsby-plugin-theme-ui` the directory can no longer be nested inside the `gatsby-theme-blog` directory. It needs to be at the root level. Additionally, all content needs to be shadowed via `index.js`. You can make use of files like `colors.js` but they will not shadow unless explicitly exported from `index.js`.

**Default deepmerge** - Any shadowed styles will deepmerge with the `gatsby-theme-blog` built-in styles automatically.

If your previous code look like this:

```javascript
import merge from "deepmerge"
import defaultThemeColors from "gatsby-theme-blog/src/gatsby-plugin-theme-ui/colors"

const darkBlue = `#007acc`
const lightBlue = `#66E0FF`
const blueGray = `#282c35`

export default merge(defaultThemeColors, {
  text: blueGray,
  primary: darkBlue,
  heading: blueGray,
})
```

It should now look like this. Noting that the merge still occurs by default.

```javascript
const darkBlue = `#007acc`
const lightBlue = `#66E0FF`
const blueGray = `#282c35`

export default {
  text: blueGray,
  primary: darkBlue,
  heading: blueGray,
}
```

If you did not merge in the official theme styles and instead overrode them you can still do so. You'll want to remove the preset by passing the option in `gatsby-config.js`

```javascript
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-blog`,
      options: {
        preset: false,
      },
    },
  ],
}
```

**No built in Typography.js** - Typography.js is no longer part of the default styling. If you'd like to add it locally follow the [Theme UI docs](https://theme-ui.com/packages/typography/#extending-the-typographyjs-theme) or note the code snippet below. The original theme used `typography-theme-wordpress-2016` and also imported `typeface-montserrat` and `typeface-merriweather`.

Another thing to keep in mind if you're pulling in typography for local shadowing is that the order of merging is different. The most common issue is that the spacing underneath code blocks is off. To fix that, include the following code in `src/gatsby-plugin-theme-ui/index.js`.

```javascript
import { toTheme } from "@theme-ui/typography"
import wp2016 from "typography-theme-wordpress-2016"
import { merge } from "theme-ui"

export default merge(toTheme(wp2016), {
  styles: {
    pre: {
      margin: `0 0 2 0`,
    },
  },
})
```
