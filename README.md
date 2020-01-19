# Rails Bootstrap Starter Kit

Getting started with Bootstrap 4 on Rails 6 using Web Packer.

See *commit diff* for changes.

Up and running:

* Add Bootstrap, jQuery and popper packages with Yarn

```
$ yarn add bootstrap jquery popper.js
```

* Import Bootstrap stylesheets, `_variables.scss` and `application.scss` to Webpack

```
// Create stylesheets folder and application.scss file

$ mkdir app/javascript/stylesheets
$ touch app/javascript/stylesheets/_variables.scss
$ touch app/javascript/stylesheets/_application.scss
```

In `app/javascript/packs/application.js`, import `_variables.scss`, `bootstrap` and `application.scss`

```
import "stylesheets/_variables.scss"
import "bootstrap"
import "stylesheets/application.scss"
```

Checkout Bootstrap [variables](https://github.com/twbs/bootstrap/blob/master/scss/_variables.scss) file on Github repository.

In styles in `app/javascript/stylesheets/application.scss`
```
// Import styles

@import "variables";
@import "bootstrap";
```

* Update Application layout to include application `stylesheet_pack_tag`

```
// Link imported styles using `stylesheet_pack_tag` to `app/views/layouts/application.html.erb`

<%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
<%= stylesheet_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
<%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
```

* Automatically load jQuery and popper.js using Webpack's ProvidePlugin

```
// config/webpack/environment.js

const { environment } = require('@rails/webpacker')
const webpack = require("webpack")

environment.plugins.append("Provide", new webpack.ProvidePlugin({
  $: 'jquery',
  jQuery: 'jquery',
  Popper: ['popper.js', 'default']
}))

module.exports = environment
```

* Setup an `addEventListener` for `tooltip`, `popover` and Toast to work with Turbolinks to load on every page change

```
document.addEventListener("turbolinks:load", () => {
  $('[data-toggle="tooltip"]').tooltip()
  $('[data-toggle="popover"]').popover()
  $('.toast').toast({ autohide: false })
  $('.toast').toast('show')
})
```
