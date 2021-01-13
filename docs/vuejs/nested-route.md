# Nested Route

## Default Named Child Route

You can't have parent named route when you have a default child route like below:

```js
const routes = [
  {
    path: "/admin",
    name: "admin",  // parent named route
    component: Admin,
    children: [
      { path: "role", name: "admin-role", component: AdminRole },
      { path: "setting", name: "admin-setting", component: AdminSetting },

      // The default child route
      { path: "", redirect: { name: "admin-role" } },
    ],
  },
];
```

You'll get below error and `{ path: "", redirect: { name: "admin-role" } }` will not work either.

```text
[vue-router] Named Route 'admin' has a default child route. When navigating to this named route (:to="{name: 'admin'"}), the default child route will not be rendered. Remove the name from this route and use the name of the default child route for named links instead.
```

To fix this, remove the parent route name then add that name to the default child route.

```js
const routes = [
  {
    path: "/admin",
    component: Admin,
    children: [
      { path: "role", name: "admin-role", component: AdminRole },
      { path: "setting", name: "admin-setting", component: AdminSetting },

      // Add the desired parent route name to this default child route
      { path: "", name: "admin", redirect: { name: "admin-role" } },
    ],
  },
];
```

Use the named route with router link:

```html
<router-link :to="{name: 'admin'}">Admin</router-link>
```
