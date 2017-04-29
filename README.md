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
  - OS X 10.9 or later. Older OS X versions are not supported and will not work.
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

```
{
  "name"    : "your-app",
  "version" : "0.1.0",
  "main"    : "main.js"
}
```
