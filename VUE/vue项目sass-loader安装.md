###vue项目sass-loader安装

####npm

> 1.安装sass的依赖包

```undefined
npm install --save-dev sass-loader
```

> 2.//sass-loader依赖于node-sass,所以要安装node-sass

```undefined
npm install --save-dev node-sass
```

> 3.在build文件夹下的webpack.base.conf.js的rules里面添加配置

```css
{
  test: /\.sass$/,
  loaders: ['style', 'css', 'sass']
}
```

> 注意：下面这个 加不加视情况定（css的）

```css
 {
    test:/\.css$/,
    loader:'style-loader'
 },
 {
    test:/\.css$/,
    loader:'css-loader'
 },
```

> 4.在APP.vue中修改style标签

```xml
<style lang="scss">
```

> 5.然后运行项目

```ruby
$ npm run dev
```

#### yarn

1、创建一个基于 webpack 模板的新项目

```kotlin
vue init webpack myApp
```

2、在当前目录下，安装依赖（此处应用yarn安装依赖，小伙伴们可以根据自己的喜好用npm或是cnpm）

```bash
cd myApp
yarn install
```

3、安装sass的依赖包

```csharp
yarn add sass-loader
//sass-loader依赖于node-sass
yarn add node-sass
```

4、在build文件夹下的webpack.base.conf.js的module模块下rules里面添加配置

```css
...,
{
  test: /\.sass$/,
  loaders: ['style', 'css', 'sass']
}
```

5、在相应的vue文件中修改style标签

```xml
<style lang="scss">
...
</style>
```

6、然后运行项目

```undefined
yarn run dev
```

