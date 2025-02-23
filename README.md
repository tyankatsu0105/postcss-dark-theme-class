# PostCSS Dark Theme Class

[PostCSS] plugin to make switcher to force dark or light theme by copying styles
from media query to special class.

[PostCSS]: https://github.com/postcss/postcss

```css
@media (prefers-color-scheme: dark) {
  :root { /* :root is <html> for HTML documents */
    --text-color: white
  }
  body {
    background: black
  }
}
```

```css
@media (prefers-color-scheme: dark) {
  :root:not(.is-light) { /* :root is <html> for HTML documents */
    --text-color: white
  }
  html:not(.is-light) body {
    background: black
  }
}
:root.is-dark { /* :root is <html> for HTML documents */
  --text-color: white
}
html.is-dark body {
  background: black
}
```

By default (without classes on `html`), website will use browser dark/light
theme. If user want to use dark theme, you set `html.is-dark` class.
If user want to force light theme, you use `html.is-light`.


## Usage

**Step 1:** Check you project for existed PostCSS config: `postcss.config.js`
in the project root, `"postcss"` section in `package.json`
or `postcss` in bundle config.

If you do not use PostCSS, add it according to [official docs]
and set this plugin in settings.

**Step 2:** Add the plugin to plugins list:

```diff
module.exports = {
  plugins: [
+   require('postcss-dark-theme-class'),
    require('autoprefixer')
  ]
}
```

**Step 3:** Add theme switcher to UI. We recommend to have 3 states: light,
dark, and auto.

**Step 4:** Set `is-dark` and `is-light` classes to `<html>` according
to switcher state:

```js
let html = document.documentElement
themeSwitcher.addEventListener('change', () => {

  if (themeSwitcher.value === 'auto') {
    html.classList.remove('is-dark', 'is-light')

  } else if (themeSwitcher.value === 'light') {
    html.classList.add('is-light')
    html.classList.remove('is-dark')

  } else if (themeSwitcher.value === 'dark') {
    html.classList.add('is-dark')
    html.classList.remove('is-light')

  }
})
```

[official docs]: https://github.com/postcss/postcss#usage


## Options

```js
module.exports = {
  plugins: [
    require('postcss-dark-theme-class')({
      darkClass: 'dark-theme',
      lightClass: 'light-theme'
    })
  ]
}
```

### `darkClass`

Type: `string`. Default: `is-dark`.

`html`’s class, which will switch dark theme.


### `lightClass`

Type: `string`. Default: `is-light`.

`html`’s class, which will switch light theme.
