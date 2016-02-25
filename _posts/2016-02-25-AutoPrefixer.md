---
layout: post
title: AutoPrefixer
tags: [CSS3, Gulp, Webpack]
categories: [Css]
---

众所周知为兼容所有浏览器，有的CSS属性需要对不同的浏览器加上前缀，然而有时添加一条属性，需要添加3~4条类似的属性只是为了满足浏览器的兼容，这不仅会增加许多的工作量，还会使得你的思路被打断。

如何解决这个问题？最近写项目时，就发现了一个处理CSS前缀问题的神器——**AutoPrefixer**。

![AutoPrefixer](http://upload-images.jianshu.io/upload_images/1258730-04af23dfecfac121.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####What is AutoPrefixer
Autoprefixer是一个后处理程序，你可以同Sass，Stylus或LESS等预处理器共通使用。它适用于普通的CSS，而你无需关心要为哪些浏览器加前缀，只需全新关注于实现，并使用W3C最新的规范。

####How to use AutoPrefixer
介绍了这么多，如果用起来很麻烦，那还不如直接手写，而**AutoPrefixer**的另一大特点就是使用简便，现在来说说怎么用。

**AutoPrefixer**可以简单的通过下载plugin配置到`Sublime`，`Brackets`或`Atom`等IDE里，而在`WebStorm`中无法通过plugin直接安装和使用AutoPrefixer，需要通过External Tools或File Watchers来实现，详细的在`WebStorm`中如何安装可以参考 [这篇文章](http://www.css88.com/archives/5670)。

如果单单只能通过IDE才能使用这个功能，那它远称不上神器，真正让其拥有神器之名的原因是：它可以很简单、有效地同现有的打包工具（`gulp`, `webpack`等）一同使用，来完成对项目中所有的`css`文件中的属性添加前缀。

下面，我们就分别来看在这两种打包工具下如何使用**AutoPrefixer**。
* gulp
在gulp中，可以使用 [AutoPrefixer官网](https://github.com/postcss/autoprefixer) 推荐的`postcss` + `autoprefixer`两个插件的组合，也可以通过`gulp-autoprefixer`这一个插件。
```javascript
// Method 1: postcss + autoprefixer
gulp.task('autoprefixer', function () { 
    var postcss = require('gulp-postcss');
    var sourcemaps = require('gulp-sourcemaps');
    var autoprefixer = require('autoprefixer');

    return gulp.src('./src/*.css')
      .pipe(sourcemaps.init())
      .pipe(postcss([ autoprefixer({ browsers: ['last 2 versions'] }) ]))
      .pipe(sourcemaps.write('.'))
      .pipe(gulp.dest('./dest'));
});
// Method 2: gulp-autoprefixer
gulp.task('autoprefixer', function () { 
    var autoprefixer = require('gulp-autoprefixer');

    return gulp.src('./src/*.css')
      .pipe([ autoprefixer({ browsers: ['last 2 versions'] }) ])
      .pipe(gulp.dest('./dest'));
});
```
* webpack
而在最近很火的`webpack`中使用**AutoPrefixer**更是轻而易举、如虎添翼。
使用`webpack`可以通过简单的配置将本文开头提到的sass这样的预处理器同`autoprefixer`这样的后处理程序结合在一起。
```javascript
var autoprefixer = require('autoprefixer');
module.exports = {
    module: {
      loaders: [
        { test: /\.css$/, loader: "style!css!postcss" },
        { test: /\.scss$/, loader: "style!css!postcss!sass" }
      ]
    },
    postcss: [ autoprefixer({ browsers: ['last 2 versions'] })
]}
```
注： 另外`webpack`还有一个`autoprefixer-loader`，但npm官网已将其标为【deprecated】，推荐使用上面示例中通过`postcss-loader`的方式使用`autoprefixer`。