# Propshaft Sample App

A Rails 7 application to try a few things with Propshaft. This README will contain some issues I encountered.

## Specs

- Rails 7.0.0.rc1
- Ruby 3.0.3
- Propshaft
- JSBundling-Rails (with esbuild)
- CSSBundling-Rails (with sass)
- Bootstrap 5
- Bootstrap Icons
- Font Awesome 5 Icons

## Issues

### Bootstrap Icons - Font files

Bootstrap 5 Icons did not work out-of-the-box. Fonts were not imported correctly.

In the original `bootstrap-icons.scss`, they are imported via the `$bootstrap-icons-font-src` variable.

Default value:
```scss
$bootstrap-icons-font-src: url("./fonts/bootstrap-icons.woff2?30af91bf14e37666a085fb8a161ff36d") format("woff2"),
url("./fonts/bootstrap-icons.woff?30af91bf14e37666a085fb8a161ff36d") format("woff") !default;
```

To make the icons work, I had to do two things:

- Create an initializer to add the fonts from `node_modules` in Propshaft's load path.

  In `config/initializers/assets.rb`:
  ```ruby
  Rails.application.config.assets.paths << Rails.root.join("node_modules", "bootstrap-icons", "font")
  ```
- Change the `$bootstrap-icons-font-src` variable before importing `bootstrap-icons` stylesheet. We need to remove the fingerprint.

  In `app/assets/stylesheets/application.sass.scss`:
  ```scss
  $bootstrap-icons-font-src: url("./fonts/bootstrap-icons.woff2") format("woff2"),
  url("./fonts/bootstrap-icons.woff") format("woff");
  @import "bootstrap-icons/font/bootstrap-icons";
  ```

### Font Awesome - Font files

Font Awesome Icons did not work out-of-the-box. Fonts were not imported correctly.

It uses an SCSS variable `$fa-font-path` to determine where to look for font files. (default: `"../webfonts"`)

To make the icons work, I had to:

- Add Font Awesome folder from `node_modules` in Propshaft's load path.

  In `config/initializers/assets.rb`:
  ```ruby
  Rails.application.config.assets.paths << Rails.root.join("node_modules", "@fortawesome", "fontawesome-free")
  ```
- Change the `$fa-font-path` variable before importing `@fortawesome/fontawesome` stylesheets.

  In `app/assets/stylesheets/application.sass.scss`:
  ```scss
  // Before: $fa-font-path: "../webfonts";
  $fa-font-path: "./webfonts";
  @import "@fortawesome/fontawesome-free/scss/fontawesome";
  @import "@fortawesome/fontawesome-free/scss/solid";
  ```
