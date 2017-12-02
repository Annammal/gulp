### Project Strcture 

``` sh
mkdir gulp && cd gulp
npm init
cd scripts styles 
```

#### Install npm depedencies

``` 
npm install gulp -g
npm install --save-dev gulp-connect
npm install --save-dev gulp-less
npm install --save-dev gulp-coffee
npm install --save-dev gulp-watch
```

after installing npm dependencies make sure your package.json looks like below:

```json
{
  "name": "gulp",
  "version": "1.0.0",
  "description": "gulp starter project",
  "main": "gulpfile.js",
  "dependencies": {},
  "devDependencies": {
    "gulp": "^3.9.1",
    "gulp-coffee": "^1.4.3",
    "gulp-connect": "^2.3.1",
    "gulp-less": "^1.3.9",
    "gulp-watch": "^0.6.10"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Annammal",
  "license": "ISC"
}
```

also verify there is a folder named node_modules created with above dependencices.

##### Using npm library

```shell
touch index.html
```

``` html
<html>
<head>
	<title>grunt-starter</title>
	<link rel="stylesheet" type="text/css" href="styles/main.css">
</head>
<body>
	<script src="scripts/main.js"></script>
</body>
</html>
```
```shell
 touch gulpfile.js
```
##### gulpfile.js

```js
var gulp = require('gulp'),
  connect = require('gulp-connect'),
  watch = require('gulp-watch'),
  less = require('gulp-less'),
  coffee = require('gulp-coffee');

gulp.task('webserver', function() {
  connect.server({
    livereload: true,
    root: ['.', '.tmp']
  });
});

gulp.task('livereload', function() {
  gulp.src(['.tmp/styles/*.css', '.tmp/scripts/*.js'])
    .pipe(watch())
    .pipe(connect.reload());
});

gulp.task('less', function() {
  gulp.src('styles/main.less')
    .pipe(less())
    .pipe(gulp.dest('.tmp/styles'));
});

gulp.task('coffee', function() {
  gulp.src('scripts/*.coffee')
    .pipe(coffee())
    .pipe(gulp.dest('.tmp/scripts'));
});

gulp.task('watch', function() {
  gulp.watch('styles/*.less', ['less']);
  gulp.watch('scripts/*.coffee', ['coffee']);
})

gulp.task('default', ['less', 'coffee', 'webserver', 'livereload', 'watch']);
```
```shell 
cd scripts
touch main.coffee
```
##### main.coffee

```coffeescript
h1 = document.createElement("h1")
text = document.createTextNode("Styled Hello World from gulp-stater")
h1.appendChild text
document.body.appendChild h1
p = document.createElement("p")
paratext = document.createTextNode("Good Day!!!")
h1.appendChild paratext
document.body.appendChild p
```
```shell 
cd styles
touch main.less
```
##### main.less

```less
@green: #00ff00
@blue: #0000ff
@black: #000
h1 {
	font-family: "HelveticaNeue-Light", "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial, "Lucida Grande";
	background: @green;
	color: @black;
	padding: 6px;
}
```
#### To run this application 
```sh
gulp
```
