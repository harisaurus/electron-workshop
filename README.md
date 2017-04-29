# Desktop Apps Workshop

## Introduction
Hello and welcome to the Desktop Apps Workshop!

### Native Desktop Applications
Developing native desktop applications is quite challenging. Packaging, installation, and update management are huge points of frustration that deter many developers from pursing desktop apps. Each operating system also requires its own specific language to be used to develop native apps, which further adds to the build complexity, build time, and the managing of multiple os-specific applications that at the end of the day are supposed to be the *same app*. Traditional developers would not only need to learn additional programming languages to build desktop applications for Windows, OSX and Linux, but also dive into each OS's APIs, patterns, file structures and requirements.

Desktop applications do have multiple advantages over their web counterparts. Native features like notifications and menus can be leveraged along with building browser-independent experiences that can further add to your user's experience.

### Web Applications
Web applications, however, are far more approachable. The languages required to build web applications are far more approachable - in fact, all of us here are already familiar with the three most common/required ones (HTML, CSS, JavaScript). These languages are universal and cross platform, allowing us to build once for *every* browser/user. Browsers also exist on pretty much everyone's OS in one form or another. This makes web applications a lot easier to adopt as no additional tooling/software is required to access/use them. Newer browsers also provide fantastic development tooling. Devtools, Page Inspectors, Firebug (lol), and an incredible list of browser plugins really speed up and simplify the development process for building web applications. There's also a huge selection of libraries and frameworks developers can leverage to further assist in building bigger, faster applications more efficiently. Some of the most popular ones today include React, Angular, and good ol' jQuery.

Things aren't entirely magical in the world of web applications. Developers are required to handle browser-specific requirements, fallbacks, and conditional rules which can prevent the usage of newer/faster browser features. Browsers are also quite rubbish at interacting with the file system and are hugely dependent on the network quality and strength.

### The Ideal Scenario
An ideal scenario would entail the flexibility and accessibility of web technology, the cross-platform flexibility of browsers, and the native experience and features of a desktop application. All this would be wrapped into a simple executible. All the advantages from both worlds, with non of the disadvantages, barriers, and limitations!

## Electron Framework

![Electron Logo](https://camo.githubusercontent.com/11e7cfd04eceb1ea7464e99edda0e7000487f343/68747470733a2f2f656c656374726f6e2e61746f6d2e696f2f696d616765732f656c656374726f6e2d6c6f676f2e737667)

The Electron framework allows us to create cross-platform native applications that rely on web technology, HTML, CSS and JavaScript. Electron provides a robust set of JavaScript APIs that interface with various operating systems and their particular nuances. It uses web pages to create user interfaces, just like a web application.

You can look at it as a simplified, watered-down browser capable of interacting with the native operating system. This 'browser' becomes part of your application's packaging and is distributed to whoever installs it. You code it once, and create distributions for Windows, Mac OSX, and Linux in one go.

Electron also allows you to focus on building your application and what it does, rather than how it does it. When calling functions that interact with the operating system, you can be confident knowing that Electron handles the OS specifics itself, allowing you to speed on ahead instead of worrying about the differences between each operating system's requirements.

Electron includes Chromium's APIs allowing you to leverage browser technology to its fullest, Node JS's modules, and supports including third party modules too.

## Who's Using Electron?
Although Electron is entirely open source, its most definitely used for a lot of production grade applications by developers around the world. Slack, the Atom Text Editor, Nylas's N1 Mail Client, WordPress.com's Desktop App, and Microsoft's Visual Studio Code are all excellent examples of large complex applications built using Electron. [Additional examples](https://electron.atom.io/apps/)

## Requirements
### OS Requirements
- Windows
  - Windows 7 or later. Older Windows versions are not supported and will not work.
  - x86 and x64 binaries are provided for Windows.
- Mac
  - OS X 10.9 or later. Older macOS versions are not supported and will not work.
  - Only 64bit binaries are provided.
- Linux
  - Ubuntu 12.04 is the most stable and guaranteed to work.
  - Versions later than Ubuntu 12.04, Fedora 21, or Debian 8 are verified but not guaranteed.

### Software/Tooling Requirements
- Node.js - A JavaScript runtime built on Chrome's V8 engine. Node.js also provides a massive package ecosystem, npm, which we will be leveraging to bring in third party libraries.

## Project Setup
A standard Electron app begins with a structure as follows:
```
gif-app/
├── package.json
├── main.js
└── index.html
```

The `package.json` file will include a few simple items to get the ball moving.

```json
{
  "name"    : "the-app",
  "version" : "0.1.0",
  "main"    : "main.js"
}
```

The script specified for the `main` field is our startup script. If no value is present, Electron will attempt to load `index.js`.

The first package required to get going is the Electron package itself. `npm install electron --save-dev` will install the Electron package as a development dependency.

## Our First App
### Startup Script
Start the `main.js` file by importing a few basic utilities from Electron along with a few other dependencies.

```js
const {app, BrowserWindow} = require('electron');
const path = require('path');
const url = require('url');
```

Next, we need to write a function that creates a new `BrowserWindow` instance. We can pass in some options to specify the size of the window created. We also want this window instance to load the `index.html` file that's in the project directory.

```js
let win;
// a global reference to our windows. this can be a single window or an array of windows.

function createWindow() {
 win = new BrowserWindow({
    width: 800,
    height: 500
  });
  
  win.loadURL(url.format({
    pathname: path.join(__dirname, 'index.html'),
    protocol: 'file:',
    slashes: true
  }));
}
```

We then tell Electron to run this `createWindow` when the application's state is ready to execute commands. Think of this as jQuery's `.ready`.

```js
app.on('ready', createWindow);
```

To properly handle closing of windows, we need to set our window `win` variable back to null in the `createWindow()` function. The `main.js` file should now look as follows:

```js
const {app, BrowserWindow} = require('electron');
const path = require('path');
const url = require('url');

let win;

function createWindow() {
  win = new BrowserWindow({
    width: 800,
    height: 500
  });

  win.loadURL(url.format({
    pathname: path.join(__dirname, 'index.html'),
    protocol: 'file:',
    slashes: true
  }));

  win.on('closed', () => {
    win = null;
  });
}

app.on('ready', createWindow);
```

### HTML Scaffold

Add a tiny bit of basic markup in the `index.html` file. The following code will do for now.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>GIF!</title>
  </head>
  <body>
    <h1>hello world!</h1>
  </body>
</html>
```

### Run It!

To run an Electron app, call Electron along with the path to our app. We didn't install the Electron package globally, as we can utilize the version sitting in our `node_modules` folder. 

```bash
# macOS
./node_modules/.bin/electron .

# Windows
.\node_modules\.bin\electron .
```

Where `.` represents the current folder directory (our app).

Success! Let's add an npm script to our `package.json` file to handle running our Electron app.

```json
{
  "name": "the-app",
  "version": "0.1.0",
  "main": "main.js",
  "scripts": {
    "start": "./node_modules/.bin/electron ."
  },
  "devDependencies": {
    "electron": "^1.6.6"
  }
}
```

## The Main and Renderer Process
A core feature in Electron is its ability to run two or more operating system level processes concurrently. These are referred to as the 'main' and 'renderer' processes. 

### What is a process?
A process is an instance of a computer program being executed. If we run an Electron application and check the Activity Monitor in MacOS we'd see the following:

![Activity Monitor](https://cdn-images-1.medium.com/max/800/1*VAlIY8iCR_Tb78lMQrIz2w.png)

The 'Electron' process is the main process, one of the helpers is a GPU process, and the remaining helpers are various renderer processes.

The main thing to remember here is that they run concurrently and completely isolated from one another. This is extremely valuable as it keeps any issues/errors isolated from the other renderer instances preventing the entire app from crashing if one particular renderer instance falls apart. 

Any low-level system related functionality should exist in the main process. Everything else goes in a (or many) renderer process(es). Keep the main process as light as possible to prevent constant "beach ball"-ing. 

### Creating a Renderer
A renderer is fairly straightforward to create. Its essentially a JavaScript file linked up to an HTML file that loads up into an Electron `BrowserWindow` instance.

Let's create a `renderer.js` file in our folder and hook it up to our `index.html` file.

```js
// renderer.js
console.log('Renderer Process');
```
```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>GIF!</title>
  </head>
  <body>
    <h1>hello world</h1>
  </body>

  <script>
    require('./renderer.js')
  </script>
</html>

```

## Beginning the GIF App
We'll continue building on top of our starter app. Our end goal is to create a desktop app that allows us to search through and share GIFs. We'll be utilizing [GIPHY.com](https://giphy.com/)'s API service to request for GIFs that pertain to a particular search query. 

### GIPHY
![GIPHY Header](https://raw.githubusercontent.com/Giphy/GiphyAPI/master/api_giphy_header.gif)

The [GIPHY API](https://github.com/Giphy/GiphyAPI) has a public beta key that we can use when developing applications. You'll need a production key if and when you decide to publish and distribute your app. [Request a public key details](https://github.com/Giphy/GiphyAPI#request-a-production-key).

Thanks to the awesomesness of developer culture, someone also created a JavaScript module to help make API calls to GIPHY that supports promises and callbacks. This further simplifies our application's development. Let's install this npm package now. 
```bash
npm install giphy-api --save
```

### Rendering GIFs
To get a list of GIFs rendering in our application we need to create a wrapper in our HTML where we can dump our GIF list. 
```html
<div id="gif-list"></div>
```

In `renderer.js`, we first create a `giphy` variable and initialize a `giphy-api` instance.

```js
const giphy = require('giphy-api')();
```

This creates a `giphy-api` instance using the development key. The same initialization with a production key would look as follows:

```js
const giphy = require('giphy-api')('API KEY HERE');
```

Next, we make the GIPHY api call with testing data (I'll be using the query `pokemon`), and calling additional functions when the request returns data and resolves the promise.

```js
const gifContainer = document.getElementById('gif-list');

giphy.search({
  q: 'pokemon'
}).then(function (res) {
    // Res contains gif data!
    updateGIFList(res.data);
});

function updateGIFList(data) {
  gifContainer.innerHTML = buildList(data);
}

function buildList(data) {
  return data.map((gif) => {
    return `<button data-url="${gif.images.original.url}" class="gif-item">
        <img class="gif-image" src="${gif.images.original.url}">
      </button>`;
  }).join('');
}
```

We'll also take this time to add a bit of CSS to the application. The following will suffice for the time being.

```css
body {
  margin: 0;
  padding: 0 10px;
  background-color: black;
  color: white;
  font-family: sans-serif;
}

h1 {
  margin: 0;
  padding: 10px 15px;
  font-size: 16px;
}

.gif-item {
  display: block;
  padding: 0;
  outline: 0;
  border: 0;
  width: 100%;
  cursor: pointer;
  position: relative;
}

.gif-item ~ .gif-item {
  margin-top: 10px;
}

.gif-image {
  width: 100%;
  display: block;
}
```

## Working with Clipboards
As users, we'd like to click on one of the GIFs and have the GIF's URL copy to our clipboard. Clipboard management is normally quite tedious when development web applications, or native applications, but Electron does all the heavy lifting for us. <3 you Electron.

First, require clipboard from the `electron` package.

```js
const {clipboard} = require('electron');
// or
const clipboard = require('electron').clipboard;

```

Since the GIF list is built dynamically, we need to add event listeners to the gif container to listen for clicks on any `img` element.

```js
gifContainer.addEventListener('click', clickHandler, true);

function clickHandler(e) {
  if (e.target.classList.contains('gif-image')) {
    console.log('click on a gif!');
    console.log(e.target.src);
  }
}
```

And finally, we can use the `writeText` method on the `clipboard` instance to write the image's `src` value to the clipboard.

```js
clipboard.writeText(e.target.src);
```

Give it a shot! Hashtag Magical.

## Let's Be Obnoxious - The Notifications API
So, lets be a little crazy by utilizing Electron's notifications API to notify the user every time they copy a GIF to their clipboard. Because why the heck not.

```js
let notif = new window.Notification('GIF Copied!', {
  body: `You copied a GIF!`,
  silent: true
});
```

## Adding in Search
As hilarious as the current GIFs are, our application will be far more useful if we can serach for particular queries. Let's update the markup to add a text input with some corresponding styles.

```html
<input type="text" id="gif-search" placeholder="search...">
```

```css
#gif-search {
  display: block;
  width: 100%;
  padding: 10px 15px;
  font-size: 16px;
  margin-bottom: 20px;
  background: none;
  border: 0;
  color: white;
  border-bottom: 3px solid rgba(255, 255, 255, 0.5);
  transition: all 0.1s ease-in-out;
}

#gif-search:focus {
  outline: none;
  border-color: rgba(255, 255, 255, 1);
}
```

Great! Now lets add some functionality to this input field. An event listener on the `gif-search` element looking for the `keyup` event will allow us to continuously run new giphy API queries.

```js
document.getElementById('gif-search').addEventListener('keyup', (e) => {
  giphy.search({
    q: e.target.value
  }).then(function (res) {
    updateGIFList(res.data);
  });
});
```

This isn't super smart as the `keyup` event fires when we use shortcuts to select text, etc, so lets add in some checking to only make the API calls if and when the query is different from the last `keyup` event.

```js
let currentSearch = '';
document.getElementById('gif-search').addEventListener('keyup', (e) => {
  if ((e.target.value !== currentSearch) && e.target.value !== '') {
    giphy.search({
      q: e.target.value
    }).then(function (res) {
      currentSearch = e.target.value;
      updateGIFList(res.data);
    });
  } else if (e.target.value === '') {
    giphy.trending().then((res) => {
      updateGIFList(res.data);
    });
    currentSearch = e.target.value;
  }
});
```

## Tray Icon
Tray icons are a great way for users to quickly access their most used applications. Our GIF application is a great candidate for this use case, as we'll be GIF-ying it up all day.

Firstly, create a `Tray` variable and require it from the `electron` package.

```js
const {app, BrowserWindow, Tray} = require('electron');
```

Then, build out a new function that initializes a new Tray instance. A `Tray` instance requires a path to the icon we wish to use. We need to make sure that appIcon is declared outside of the makeTray function, otherwise our icon will get garbage collected by JavaScript and disappear from our tray!

```js
let appIcon;
function makeTray() {
  appIcon = new Tray('./app-icon.png');
  appIcon.setToolTip('Electron.js App');
}
```

We can then set the icon's tooltip text so a user always knows which application the icon is for.

```js
appIcon.setToolTip('GIF All The Things!');
```

Add a click handler to run `createWindow` if a window instance doesn't already exist.

```js
appIcon.on('click', function() {
  if (!win) {
    createWindow();
  }
});
```

Our function should look like this:

```js
let appIcon;
function makeTray() {
  appIcon = new Tray('./app-icon.png');
  appIcon.setToolTip('Electron.js App');
  appIcon.on('click', function() {
    if (!win) {
      createWindow();
    }
  });
}
```

And finally, update the application's `ready` callback to run `createWindow()` and our newly created `makeTray()`;

```js
app.on('ready', function() {
  createWindow();
  makeTray();
});
```


## Application Polish
### GIF Listing Janky-ness
The application looks a little choppy, but a tiny bit of CSS animations can address some of the flickering/janky issues when updating the GIF listing.

```css
.gif-item {
  ...
  -webkit-animation: fadein 0.5s;
  animation: fadein 0.5s;
}

@keyframes fadein {
  from { opacity: 0; }
  to   { opacity: 1; }
}
```

### Application Load Flicker
The application initially loads a white browser shell followed by the HTML and CSS loading up. This causes a brief white flicker when first loading the application. This can be avoided by providing a `backgroundColor` value when initializing the `BrowserWindow`.

```js
win = new BrowserWindow({
  width: 800,
  height: 500,
  backgroundColor: "#000"
});
```

### Prevent Resizing
Simple applications such as ours normally don't allow a user to resize the application frame. Let's restrict resizing by setting the `resizable` flag when creating the `BrowserWindow` instance.

```js
win = new BrowserWindow({
  ..
  resizable: false,
  ..
});
```

### Unique macOS  Closing
On macOS, its common and very normal for applications and menu bars to stay active until a user explicitly quits the application through the menu bar, or with `Cmd + Q`.  Adding in some additional code in the main process will only quit the application on non-mac operating systems unless explicitly asked.

```js
app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit();
  }
});

app.on('activate', () => {
  if (win === null) {
    createWindow();
  }
});
```

## Packaging
### A Basic Package
Packaging an Electron application allows us to create an executable file for users. We accomplish this by first including the  `electron-packager` npm package.

```js
npm install electron-packager --save-dev
```

Similar to running the application, we'll add a new npm script to use `electron-package` to package the application.

```json
"build": "electron-packager . GIFApp
```

Note: `GIFApp` is the name you decide for the packaged application.

The `electron-packager` will by default produce a package for your current platform and architecture type. For example, on macOS it produces a package for the 'darwin' platform for the '64bit' architecture type. You can use the `--all` flag to build bundles for all valid combinations for platforms and architectures.

### Application Icon
You'll notice that the icon representing our running application is the Electron logo. Right click the packaged application and select `Show Package Contents` and navigate to `Contents>Resources`. Here you'll see the `.icns` file that the application uses.

At build time, we need to copy our own `.icns` file in the above mentioned folder to use a different icon. The `build` script should now look as follows:

```json
"build": "electron-packager . GIFApp && cp Icon.icns GIFApp-darwin-x64/GIFApp.app/Contents/Resources/electron.icns"
```

Note: This snippet shows the required path for macOS. Windows users will have a slightly different path, but the concept should remain the same.

Making to first delete the previously built package (`rm -rf [foldername]`) running the build script again gives us a packaged application with the correct icon in use!

### Archiving Sensitive Files
You may have noticed that the `Contents/Resources/app` folder essentially gives a user full access to the application's files and functionality. Another node package by the name of `asar` helps address this issue by creating an archive of the `app` folder.

Once again, we first need to bring in this new dependency.

```js
npm install asar --save-dev
```

Then, add a new npm script to update a built app's packaging.

```json
"package": "asar pack GIFApp-darwin-x64/GIFApp.app/Contents/Resources/app GIFApp-darwin-x64/GIFApp.app/Contents/Resources/app.asar"
```

Running the `package` script after the `build` script should create an unaccessible archive of the app itself, allowing us to delete the `app` folder from `Contents/Resources`. 

## TODO
There's a wide range of improvements we could make to our application. A list of a few of those are as follows

 - **Favourites**: Leveraging Local Storage could allow a user to 'favourite' their most used/liked GIFs for future reuse in a dedicated separate listing.
 - **Positioning**: Our application currently doesn't have properly defined positioning. Using packages such as [electron-positioner](https://github.com/jenslind/electron-positioner) would allow us to ensure our application opens up centered perfectly underneath the tray icon on macOS and centered perfectly above the tray section on Windows/Linux.

## Wrapping Up
I'd recommend installing the `Electron API Demos` app from the Electron website that further explains the various APIs Electron has to offer. 

Electron is still quite a young framework and has incredibly huge potential, and I'm incredibly excited to see where and how it continues to progress.

I hope this workshop has been valuable, educational and most of all, motivational to get you building some super cool cross platform desktop applications!
