# Building landing page with webpack.
## 01 step "this step1 to step14 help you configure webpack"

**First let's create a directory, initialize npm, install webpack locally, and install the webpack-cli**

`mkdir webpack-demo
cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev`
---
## 02 step

**Throughout the Guides we will use diff blocks to show you what changes we're making to directories, files, and code. For instance:**

`+ this is a new line you shall copy into your code
- and this is a line to be removed from your code
  and this is a line not to touch.`
---
## 03 step

**Now we'll create the following directory structure, files and their contents:**

`webpack-demo
|- package.json
+ |- index.html
+ |- /src
+   |- index.js`
---
## 04 step

**src/index.js**

`function component() {
  const element = document.createElement('div');

  // Lodash, currently included via a script, is required for this line to work
  element.innerHTML = _.join(['Hello', 'webpack'], ' ');

  return element;
}

document.body.appendChild(component());`
---
## 05 step

**index.html**

`<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Getting Started</title>
    <script src="https://unpkg.com/lodash@4.17.20"></script>
  </head>
  <body>
    <script src="./src/index.js"></script>
  </body>
</html>`

---
## 06 step

**We also need to adjust our package.json file in order to make sure we mark our package as private, as well as removing the main entry. This is to prevent an accidental publish of your code.**

`{
   "name": "webpack-demo",
   "version": "1.0.0",
   "description": "",
-  "main": "index.js",
+  "private": true,
   "scripts": {
     "test": "echo \"Error: no test specified\" && exit 1"
   },
   "keywords": [],
   "author": "",
   "license": "MIT",
   "devDependencies": {
     "webpack": "^5.38.1",
     "webpack-cli": "^4.7.2",
   }
 }`
---
## 07 step

**First we'll tweak our directory structure slightly, separating the "source" code (./src) from our "distribution" code (./dist). The "source" code is the code that we'll write and edit. The "distribution" code is the minimized and optimized output of our build process that will eventually be loaded in the browser. Tweak the directory structure as follows:**

`webpack-demo
|- package.json
+ |- /dist
+   |- index.html
- |- index.html
|- /src
  |- index.js`
---
## 08 step

**To bundle the lodash dependency with index.js, we'll need to install the library locally:**

`npm install --save lodash`

---
## 09 step

**Now, let's import lodash in our script: src/index.js**

`+import _ from 'lodash';
+
 function component() {
   const element = document.createElement('div');

-  // Lodash, currently included via a script, is required for this line to work
+  // Lodash, now imported by this script
   element.innerHTML = _.join(['Hello', 'webpack'], ' ');

   return element;
 }

 document.body.appendChild(component());`

---
## 10 step

**Now, since we'll be bundling our scripts, we have to update our index.html file. Let's remove the lodash <script>, as we now import it, and modify the other <script> tag to load the bundle, instead of the raw ./src file: dist/index.html**

` <!DOCTYPE html>
 <html>
   <head>
     <meta charset="utf-8" />
     <title>Getting Started</title>
-    <script src="https://unpkg.com/lodash@4.17.20"></script>
   </head>
   <body>
-    <script src="./src/index.js"></script>
+    <script src="main.js"></script>
   </body>
 </html>`
---
## 11 step

**let's run npx webpack, which will take our script at src/index.js as the entry point, and will generate dist/main.js as the output. The npx command, which ships with Node 8.2/npm 5.2.0 or higher, runs the webpack binary (./node_modules/.bin/webpack) of the webpack package we installed in the beginning:**

`$ npx webpack
[webpack-cli] Compilation finished
asset main.js 69.3 KiB [emitted] [minimized] (name: main) 1 related asset
runtime modules 1000 bytes 5 modules
cacheable modules 530 KiB
  ./src/index.js 257 bytes [built] [code generated]
  ./node_modules/lodash/lodash.js 530 KiB [built] [code generated]
webpack 5.4.0 compiled successfully in 1851 ms
`
---
## 12 step

**Open index.html from the dist directory in your browser and, if everything went right, you should see the following text: 'Hello webpack'.**


## 13 step

**Given it's not particularly fun to run a local copy of webpack from the CLI, we can set up a little shortcut. Let's adjust our package.json by adding an npm script:**

`{
   "name": "webpack-demo",
   "version": "1.0.0",
   "description": "",
   "private": true,
   "scripts": {
-    "test": "echo \"Error: no test specified\" && exit 1"
+    "test": "echo \"Error: no test specified\" && exit 1",
+    "build": "webpack"
   },
   "keywords": [],
   "author": "",
   "license": "ISC",
   "devDependencies": {
     "webpack": "^5.4.0",
     "webpack-cli": "^4.2.0"
   },
   "dependencies": {
     "lodash": "^4.17.20"
   }
 }`

## 14 step "end of configuration. if you have not understood, you could always vist the webpack documentation site."

**Now the npm run build command can be used in place of the npx command we used earlier. Note that within scripts we can reference locally installed npm packages by name the same way we did with npx. This convention is the standard in most npm-based projects because it allows all contributors to use the same set of common scripts. Now run the following command and see if your script alias works:**

`$ npm run build`

# Starting our landing page
