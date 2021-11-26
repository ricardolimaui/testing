## What is Continuous Deployment/Delivery?

>Continuous delivery (CD) is a software engineering approach in which teams produce software in short cycles, ensuring that the software can be reliably released at any time.[1] It aims at building, testing, and releasing software faster and more frequently. The approach helps reduce the cost, time, and risk of delivering changes by allowing for more incremental updates to applications in production. A straightforward and repeatable deployment process is important for continuous delivery.
>(Source: [Wikipedia](https://en.wikipedia.org/wiki/Continuous_delivery), 2016-03-21)

### Where can we use it?

We use CD for building automatically our documentation on our Main-Server. The following steps shows how we used it for MkDocs, but you can use the same technique also for your application, service or program.

### Installation

* First create a Webhook on GitHub in the repository-settings with the following URL: `http://giv-oct.uni-muenster.de:61440/github`
* Login on the Main-Server and clone the repository of **node-cd**

**ATTENTION:** There is already **GEO-C-Version** of the original **node-cd**-repository, so you can skip the steps which are marked with an `[*]`!
  
**GEO-C-Version**:
```
git clone https://github.com/geo-c/node-cd.git
```

`[*]` **Original version**:
```
git clone https://github.com/A21z/node-cd.git
```

* Install all dependencies with the following command:
```
sudo npm install
```

* `[*]` Update the file `/home/webteam/node-cd/github.sh` with the commands, which should run after a webhook-detection. For MkDocs we make a simple pull-request to download the latest files from our GitHub-repository and build the documentation:

github.sh:
```
cd /home/webteam/Dev-Corner/ && git pull && sudo mkdocs build --clean
```

* Make the file `/home/webteam/node-cd/github.sh` excecutable, and also excecutable by root-user! This is an important step, otherwise the commands can not be run:
```
chmod u+s github.sh
```

* `[*]` Update the file `/home/webteam/node-cd/config.js` with the correct folder-path, so it should look like this:

```javascript
action: {
  exec: {
    github: '/home/webteam/node-cd/github.sh',
    bitbucket: './bitbucket.sh',
    contentful: './contentful.sh'
  }
}
```

* Add a cron-job for automatic start, when the Main-Server reboots with the command `sudo nano /etc/crontab` and add the following lines:

```
# Automatic-Deployment-Server
@reboot root node /home/webteam/node-cd/src/index.js
```

* Finally restart the Main-Server, so that the Continuous Delivery System starts listening for commits on GitHub.

```
sudo shutdown -r 0
```

### Second Listener

* If you want to checkout more than 1 repository, create in your new repository a new Webhook with a new portnumber, e.g. `http://giv-oct.uni-muenster.de:61441/github`
* Clone the **node-cd**-repository again on the Main-Server
* Follow the same steps like above, but before starting the server, change the portnumber in the `/home/webteam/node-cd_2/config.js`-file: 

```javascript
var Private = {
  server: {port: '61441'},
  ...
}
```
* Add a second cron-job and reboot again
