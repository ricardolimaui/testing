## What is Bower?

>A package manager for the web
>(Source: [http://bower.io](http://bower.io), 2016-02-15)

##### Linux/MacOS

* You need [Nodejs](nodejs.md#nodejs) to install Bower.
* Install Bower globally with the following command:

```bash
sudo npm install bower -g
```

##### Windows

* You need [Nodejs](nodejs.md#nodejs) to install Bower.
* Install Bower globally with the following command:

```bash
npm install bower -g
```

### Install packages

Install all dependecies (bower-packages) of a `bower.json`-file.


### Init

```bash
bower init
```

 -> bower.json

```bash
mkdir lib
```
-> /public/lib

```bash
nano .bowerrc
```

Bowerrc-File:

```javascript
{
	"directory":"lib"
}
```

```bash
bower install jquery --save
bower install bootstrap --save
```
