---
title: "Quick Start"
description: "Guides lead a user through a specific task they want to accomplish, often with a sequence of steps."
summary: ""
date: 2025-06-06T15:33:00+02:00
lastmod: 2026-03-20T09:07:37+01:00
draft: false
weight: 810
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  robots: "" # custom robot tags (optional)
---

`@thulite/inline-svg` is a package that enables seamless integration of SVG icons and graphics into your Thulite projects. It allows you to inline SVG content directly into your HTML, making it easy to style and manipulate SVG elements with CSS.

## Installation


{{< tabs "installation" >}}
{{< tab "npm" >}}

```bash
npm install @thulite/inline-svg
```

{{< /tab >}}
{{< tab "pnpm" >}}

```bash
pnpm install @thulite/inline-svg
```

{{< /tab >}}
{{< tab "Yarn" >}}

```bash
yarn install @thulite/inline-svg
```

{{< /tab >}}
{{< tab "bun" >}}

```bash
bun install @thulite/inline-svg
```

{{< /tab >}}
{{< /tabs >}}

## Basic Usage

### Using the Partial

The simplest way to include an SVG is by using the partial:

```html
{{</* partial "inline-svg" "path/to/icon" */>}}
```

Where `path/to/icon` is the path to your SVG file relative to the `assets` directory (without the `.svg` extension).

### Using the Shortcode

For content files, you can use the shortcode:

```md
{{</* inline-svg "path/to/icon" */>}}
```

Or with named parameters:

```md
{{</* inline-svg src="path/to/icon" class="custom-class" */>}}
```

## Advanced Usage

### Passing Parameters

You can pass additional parameters to customize the SVG:

```html
{{ partial "inline-svg" (dict
  "src" "path/to/icon"
  "class" "icon-large primary-color"
  "width" "24"
  "height" "24"
) }}
```

### Available Parameters

| Parameter | Description | Default |
| --- | --- | --- |
| `src` | Path to the SVG file (required) | - |
| `id` | Custom ID for the SVG element | `svg-[filename]` |
| `class` | CSS classes to add to the SVG | `svg-inline` |
| `role` | ARIA role attribute | `img` |
| `title` | Accessible title for the SVG | - |
| `desc` | Accessible description for the SVG | - |
| `width` | Width of the SVG | - |
| `height` | Height of the SVG| - |

### Using Page Resources

You can also reference SVGs from your page resources:

```html
{{ $svg := .Resources.GetMatch "icon.svg" }}
{{ partial "inline-svg" (dict "src" $svg) }}
```

### Icon Sets

The package supports using icon sets. If an SVG isn't found in the specified path, it will look for it in the icon set directory.

Configure the icon set directory in your site parameters:

```toml {title="config/_default/params.toml"}
# Inline SVG (@thulite/inline-svg)
[inline_svg]
  iconSetDir = "tabler-icons" # "tabler-icons" (default)
```

Then use icons from the set:

```html
{{ partial "inline-svg" "icon-name" }}
```

This will look for the SVG in `assets/svgs/tabler-icons/icon-name.svg`.

## Accessibility Features

The package automatically enhances SVGs for accessibility:

- Adds proper ARIA attributes
- Supports adding title and description elements
- Sets appropriate ARIA roles

Example with accessibility features:

```html
{{ partial "inline-svg" (dict
  "src" "check-circle"
  "title" "Success"
  "desc" "Operation completed successfully"
  "role" "img"
) }}
```

## CSS Styling

All inlined SVGs receive the `svg-inline` class by default, making it easy to style them with CSS:

```css {title="assets/scss/common/_custom.scss"}
.svg-inline {
  fill: currentColor;
}

.svg-inline.large {
  width: 2em;
  height: 2em;
}
```

## Examples

### Basic Icon

```html
{{ partial "inline-svg" "check" }}
```

{{< inline-svg "outline/check" >}}

### Styled Icon with Title

```html
{{ partial "inline-svg" (dict
  "src" "alert-triangle"
  "class" "warning-icon"
  "title" "Warning"
  "width" "24"
  "height" "24"
  "stroke" "orange"
) }}
```

{{< inline-svg src="outline/alert-triangle" class="warning-icon" title="Warning" width="24" height="24" stroke="orange" >}}

## Using in Navigation

```html
<nav>
  <a href="/">
    {{ partial "inline-svg" (dict "src" "home" "class" "nav-icon") }}
    Home
  </a>
</nav>
```

## Troubleshooting

If your SVG doesn't appear, check:

1. The path is correct relative to the `assets` directory
2. The SVG file exists and is valid
3. You've removed the `.svg` extension in the path

## License

This package is licensed under the MIT License. See the [LICENSE](https://github.com/thuliteio/inline-svg/blob/main/LICENSE) file for details.
