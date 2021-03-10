# vue-router

Error: NavigationDuplicated: Avoided redundant navigation to current location

Solution:

```js
Vue.use(VueRouter);

const originalPush = VueRouter.prototype.push;
VueRouter.prototype.push = function push(location) {
  return originalPush.call(this, location).catch(err => err);
};
```
