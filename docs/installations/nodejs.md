## What is Nodejs?

>Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world. 
>(Source: [https://nodejs.org/en/](https://nodejs.org/en/), 2016-02-15)

##### Linux

* For **Ubuntu** add the following link to you package-list:
```bash
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
```
* Install nodejs with the following command:
```
sudo apt-get install -y nodejs
```
* For **other distributions** go to [https://nodejs.org/en/download/package-manager/](https://nodejs.org/en/download/package-manager/) and install the latest stable version (LTS-verion is recommend))
* Open the commandline and update the node-package-manager:

```bash
sudo npm install npm -g
```

##### MacOS

* Go to [https://nodejs.org/en/](https://nodejs.org/en/) and download the latest stable version (LTS-verion is recommend)
* Install the package
* Open the terminal and update the node-package-manager:
 
```bash
sudo npm install npm -g
```


##### Windows

* Go to [https://nodejs.org/en/](https://nodejs.org/en/) and install 
* Open the Windows-Shell (cmd) and update the node-package-manager:

```bash
npm install npm -g
```

### Install packages

Install all dependecies (node-packages) of a `package.json`-file.

### Init

Create a `package.json`:

To-Do