# Static-Boilerplate

static site boilerplate with gulp server/build/ftp 

## Requirements

NPM, Gulp, and dependencies 

## How to Use

Load up depdencies with *npm install*. 
Type *gulp init* to set up symlinks from build to deploy for static assets.
*gulp* to start browsersync which will update on any saved change. 

```
npm install
gulp init
gulp
```

Deploy created minified version of everything and smushes images.

```
gulp deploy
```

If you want to take a look at deploy to make sure everything is kosher run:

```
gulp serve-deploy
```

If you want to FTP the deploy folder somewhere, update the *data/secret.json* and remove that from git and add it to *.gitignore*. You also need to update *data/gulp-config.json* to specify where on your server you want the files to go in *FTP_DEST*.

```
gulp upload
```

## What Happens 

Use jade templates for HTML, modify *Gulpfile.js* to pass in relevant variables, it is watched for changes and browsersync will update when a template is saved.

Browserify will bundle components in src/js and lint. Put vendor scripts in deploy/js/vendor, it will be symlinked from build/.

SCSS will be parsed into src/css, normalize appended, autoprefixed, then concat into build/main.css then minified to deploy/main.min.css when you run deploy. Browsersync will update when file is saved.

## Where to Put Things

Almost all your work goes in *src/*, except static accepts such as third party Javascript which goes in *deploy/js/vendor* and font faces which go in */deploy/fonts*. You can also put images in *deploy/img/* if you don't need them to be minimized. The server runs from *build/* which symlinks font and img assets in *deploy/*. 




## Boilerplate Structure

```
build/
--- js/
------ base.js
------ *vendor/
--- css/
------ main.css
--- *img/
--- *fonts/

deploy/
--- js/
------ base.min.js
------ vendor/
--- css/
------ main.min.css
--- img/
--- fonts/

src/
--- js/
------ base.js
------ component1.js
------ component2.js
--- sass/
------ base.scss
------ partials
--------- _var.scss
--------- _font.scss
--------- _sprite.scss
--- css/
------ main.css
--- img/

data/
--- secret.json
--- gconfig.json

Gulpfile.js
.gitignore
```