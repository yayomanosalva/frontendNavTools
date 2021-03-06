frontend-nanodegree-mobile-portfolio
====================================

## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository, inspect the code,

### Getting started

#step for Website Performance Optimization

###collaborative optimization
##Jiar Manosalva

#Optimizing the CRP

1. Async javascript
1. window.onload event

  ```bash
  asynchronousJS
  <script src="analytics.js" async ></script>
  ```
1. validate cached response

  ```bash
  <img src="img/control.png" class="center" cache-control="HTTP">
  ```
1. minimize css, js
1. minimizing gzip

1. Proect structure for Front end project


  ```bash
  $> git init
  $> ls -a
  $> touch README.md
  $> subl README.md
  $> touch .gitignore
  $> subl
  ```
1. Edit .gitignore

  ```bash
  node_modules/
  bower_components/
  .DS_store
  .sass_cache
  .env
  dist
  *debug.log
  ```

  ```bash
  $> npm install async
  $> touch package.json
  $> touch bower.json
  $> npm install --save-dev gulp
  $> mkdir src
  $> mkdir src/scripts src/styles
  $> touch src/index.html src/scripts/app.js  src/styles/main.css
  $> open src/index.html
  $> touch gulpfile.js
  $> npm install --save-dev browser-sync gulp-uglify gulp-minify gulp-html-replace gulp-sourcemaps
  $> gulp content
  $> npm install -g gulpfile-install
  $> gulpfile-install
  $> gulp <<< el nombre de la tarea >>> y enter en la consola
  
  // Tambien si trabajamos con css y js
  $> mkdir src
  $> mkdir src/js src/css
  $> touch src/index.html src/js/app.js  src/css/main.css
  ```
1. Edit package.json

  ```bash
  {
    "name": "project_name",
    "version": "0.0.1",
    "description": "optimizing project",
    "author": {
      "name": "Jair Manosalva",
      "email": "yayomanosalva@gmail.com"
    },
    "script": {
      "start": "npm install && gulp"
    },
    "dependencies": {
      "async": "^1.5.2"
    },
    "devDependencies": {
      "axios": "^0.8.1",
    "browser-sync": "^2.12.3",
    "gulp": "^3.9.0",
    "gulp-html-replace": "^1.5.5",
    "gulp-jasmine": "^2.3.0",
    "gulp-minify": "0.0.10",
    "gulp-sourcemaps": "^1.6.0",
    "gulp-uglify": "^1.5.3"
    }
  }
  ```

1. Edit gulpfile.js

  ```bash
  var gulp = require('gulp');
  var browserSync = require('browser-sync').create();
  var reload = browserSync.reload;
  var uglify = require('gulp-uglify');
  var concat = require('gulp-concat');
  var minifyCSS = require('gulp-minify-css');
  var replace =  require('gulp-html-replace');
  var sourcemaps = require('gulp-sourcemaps');
  var modernizr = require('gulp-modernizr');
  const jasmine = require('gulp-jasmine');
  
  gulp.task('default', () =>
    gulp.src('./src/jasmine/spec/test.js')
      // gulp-jasmine works on filepaths so you can't have any plugins before it 
      .pipe(jasmine())
  );
  
  gulp.task('content', function(){
    gulp.src('./src/index.html')
        .pipe(gulp.dest('./src/'))
        .pipe(reload({stream: true}))
  });
  
  gulp.task('js', function(){
    gulp.src('src/js/*.js')
      .pipe(sourcemaps.init())
        .pipe(uglify())
        .pipe(concat('app.js'))
      .pipe(sourcemaps.write())
      .pipe(gulp.dest('./src/js/min'))
      .pipe(reload({stream: true}))
  });
  
  gulp.task('css', function(){
    return gulp.src('./src/css/*.js')
      .pipe(uglify())
        .pipe(gulp.dest('./src/css/min'))
  });
  
  gulp.task('modernizr', function() {
    gulp.src('./src/js/*.js')
      .pipe(modernizr())
      .pipe(gulp.dest("build/"))
  });
  
  gulp.task('serve', function() {
      browserSync.init({
          server: {
              baseDir: "./src/"
          }
      });
      gulp.watch('./src/index.html', ['content']);
      gulp.watch('./src/js/*.js', ['js']);
      gulp.watch('./src/css/*.css', ['css']);
      gulp.watch('./src/jasmine/spec/*.js', ['js']);
  });
  ```

1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok http 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! Optional: [More on integrating ngrok, Grunt or gulp and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

