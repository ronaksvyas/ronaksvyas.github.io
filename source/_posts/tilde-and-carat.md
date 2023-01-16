---
title : Tilde(~) and Carat(^) usage in package.json
description : Tilde(~) and Carat(^) usage in package.json
tags : [internet,npm,tech,technology,javascript,node]
date : 2022-01-01
categories : [Technology, Javascript]
menu : main
---


In `package.json` file, we define all the packages that our project needs. Any version that we mention in the package.json file, we do it in the following format. 

							                    MAJOR.MINOR.PATCH

For example, say the version is `2.3.4`. In this, `2` is major, `3` is minor and `4` is patch version. If you look closely in your existing project, you'd see that there is usually ~ or ^ before the version like `~2.3.4` or `^2.3.4`. We will try to understand what these two characters mean. 

`npm i` installs dependencies based on ~ or ^ in the `package.json` file and overwrites the `package-lock.json` and `node_modules` folder. If `package-lock.json` doesn't exist then it generates one. When we use `npm i` to install the dependencies of the project, the difference between Tilde(~) and Carat(^) is simple. 

Carat(^) versioned dependencies are installed till their latest MINOR version. Tilde(~) versioned dependencies are installed till the latest PATCH version. This is only true when we install using `npm i` 

`npm ci` installs the exact versions of dependencies and ignores the Carat(^) and Tilde(~) in the `package.json` file. It requires a `package-lock.json` file to be present.  

Using `npm i` or `npm ci` is totally dependent on your needs and environment. Hope this article was helpful. 



