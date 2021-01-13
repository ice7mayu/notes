# Setup Vuetify

## Roboto Font and Material Design Icons

Create a project with VueCli3

```bash
vue create demo-project
```

Add vuetify plugin.

```bash
vue add vuetify
```

Remove CDN reference in *public/index.html*.

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Roboto:100,300,400,500,700,900">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@mdi/font@latest/css/materialdesignicons.min.css">
```

Install font and icons with npm.

```bash
npm install typeface-roboto

npm install @mdi/font
```

Add reference in *plugins/vuetify.js*

```js
import Vue from "vue";
import Vuetify from "vuetify/lib";

// Add reference to roboto font and icon
import "@mdi/font/css/materialdesignicons.css";
import "typeface-roboto/index.css";

Vue.use(Vuetify);

export default new Vuetify({
  icons: {
    iconfont: "mdi",
  },
});
```
