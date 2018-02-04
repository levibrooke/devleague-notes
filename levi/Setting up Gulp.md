Topic: Setting up Gulp / environment
Date: 1/16/18
***

## Steps w/ empty directory

1. In empty directory, run `git init`.
2. Add to `.gitignore`:
    - node_modules
    - package-lock.json
3. Create directories:
    - `mkdir sass`
    - `mkdir public`
    - `mkdir public/css`
4. Run `npm init`
5. Run `npm install --save gulp-sass`. This will install gulp-sass as a dependency and add it to package.json.
6. Run `npm install --save gulp`. This will install gulp as a local dependency and add it to package.json.
7. Create a gulpfile.js: `touch gulpfile.js`
8. In gulpfile.js:
```javascript
const gulp = require('gulp');
const sass = require('gulp-sass');

// SASS Compiler
gulp.task('styles', function() {
  gulp.src('sass/**/*.scss') // read all subdirectories and files in /sass that is .scss
    .pipe(sass().on('error', sass.logError)) // pass errors
    .pipe(gulp.dest('public/css/')); // compile sass to this directory
});

// SASS Watcher
gulp.task('watch', function() {
  gulp.watch('sass/**/*.scss', ['styles']); // watch this dir and run 'styles'
});

gulp.task('default', ['watch']); // set default to run 'watch'
```
9. Create `style.scss` file in /sass.
10. Save a change to this file.
11. Run `gulp` to start watcher.
12. Check `/public/css` for a new style.css file.