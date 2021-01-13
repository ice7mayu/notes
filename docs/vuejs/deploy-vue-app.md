# Deploy VueJS App behind Nginx

## Config & build vue app

Setup a `publicPath` to deploy on sub dir instead of the root dir. You can change `outputDir` if needed:

```js
// contents of vue.config.js

module.exports = {
  publicPath: process.env.NODE_ENV == "production" ? "/app" : "/",
  outputDir: "app",
  transpileDependencies: ["vuetify"],
  configureWebpack: {
    devtool: "source-map",
  },
};
```

Change router base url accordingly:

```js
// contents of router.js

const router = new VueRouter({
  mode: "history",
  base: process.env.NODE_ENV == "production" ? "/app" : "/",
})
```

The `vue-cli-service build` or `npm run build` command will set `NODE_ENV` to `production` automatically.

## Nginx configuration

Add a server block to Nginx config:

```nginx
server {
  listen 80;
  server_name example.com;

  location ^~ /app {
    alias /path/to/vue-app/dist;
    index index.html index.htm;
    try_files $uri $uri/ /index.html = 404;
  }
}
```

Use `alias` directive other than `root` directive so that we can refresh the vue app.

## Nginx root vs alias directive

In case of the `root` directive, full path is appended to the root including the location part, whereas in case of the `alias` directive, only the portion of the path **NOT** including the location part is appended to the alias.
