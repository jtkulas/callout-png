---
format: html
---

# Callout Image Extension For Quarto

`callout-png` facilitates ***image*** specification within (reasonable facsimiles of) Quarto callouts. 

These image specifications supplant the [native & hacked bootstrap icon options](https://github.com/orgs/quarto-dev/discussions/3563) currently available with Quarto callouts and extends the icon customization beyond the limited default palette.

The extension is named `callout-png` because the .png format is known to support transparency (images with transparent backgrounds will return the most visually appealing results). Some format types allow flexible image sourcing; others are more restrictive.

>Native images should be used with typst and traditional pdf document types (url image--grabbing is not supported with `format: typst` or `format: pdf`).

## Installing

```bash
quarto add jtkulas/callout-png
```

This will install the extension under the `_extensions` subdirectory.
If you're using version control, you will want to check in this directory.

## Using

Identify the extension within your YAML with `filters:`, then implement via fenced div:

```bash
---
title: "My Callout Document"
format: html
filters:
  - callout-png  
---

::: {.callout-png}  
Content here...
:::

```

The default callout should display with the Pink Panther as an image and "Pinktacular Callout" as a title. The displayed font will mirror your document `mainfont` with the title presented in bold.

![](images/default.JPG)

### Customization options 

|Option   | Description           |  Default Value         |  Example  |
|---------|-----------------------|------------------------|-----------|
|color    | Banner color (left--hand border will render 7% darker)^[not supported in typst or pdf]                 | #ff99ff       | color="#bada55"     |
|title    | Content displayed to the right of image | Pinktacular Callout | title="My special callout"  |
|image    | Image filename & location | pink-panther.png | image="prettypic.png"   |
|image-height | Vertical sizing of image | 4.8em  | image-height="2em"  |
|header-vpad | Banner padding (vertical -- top & bottom) | 0em | header-vpad="1em"  |

### Image Resolution

When you specify an `image` parameter:

1. **URLs** (e.g., `https://example.com/image.png`) — used directly
2. **Project-relative paths** (e.g., `images/my-image.png`) — resolved from your document directory first
3. **Bundled extension images** (e.g., `pink-panther.png`, `snoopylocal.png`) — automatically resolved from the extension's `images/` folder

This means the default images work seamlessly for all users, whether rendering locally or in CI/CD pipelines. You can override bundled images by creating a file with the same name in your project's working directory.

## Examples

Two specifications of the 5 different attribute parameters:

```bash

::: {.callout-png title="This is BIGGER snoopy" color="#c9c9c3" image="snoopylocal.png" header-vpad="1em" icon-height="8em"}

+ bundled extension image (snoopylocal.png)
+ color=grey 
+ height=8em 
+ vertical padding=1em

:::

::: {.callout-png title="This is smaller snoopy" color="#cb6ed4" image="https://pngimg.com/uploads/snoopy/snoopy_PNG78.png" header-vpad="0em" icon-height="3em"}

+ online image location
+ color=purple 
+ height=3em 
+ vertical padding=0em

:::

```

![](images/bigsnoop.JPG)

![](images/smallsnoop.JPG)

Here is the source code for a minimal example: [example.qmd](example.qmd).

## Known issues

|             |  html  | RevealJS    | typst  | $\LaTeX$ |
|-------------|--------|-------------|--------|----------|
|local images | &#x2705; |&#x2705;  |&#x2705;  |&#x2705;  |
|url images | &#x2705; |&#x2705;  |&#x274C;   |&#x274C;  |
|dark left border| &#x2705; |&#x2705;  |&#x274C;   |&#x274C;  |
|negative `header-vpad` values | &#x274C;| &#x274C;|&#x2705; |&#x2705; |
|collapsable  | &#x274C;|  &#x274C;    | &#x274C;|&#x274C;   |

## Contributing 

Issues and pull requests are welcome! Please open an issue on the GitHub repository to propose changes or make feature requests.
