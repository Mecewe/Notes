# vue如何获取当前页面的url

当前页面
完整url可以用 `window.location.href`
路由路径可以用 `this.$route.path`
路由路径参数 `this.$route.params` 例如：/user/:id → /user/2044011030 → this.$route.params.id
路由查询参数 `this.$route.query` 例如：/user/search?name=sf → this.$route.query.name