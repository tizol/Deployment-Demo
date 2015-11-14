# Deploying Meteor Apps on Digital Ocean

#### Step 1: Sign up For a Digital Ocean Account
[Get Free $10 Digital Ocean with this referral link ](https://www.digitalocean.com/?refcode=2200d2dd5c1b)

Choose Ubuntu 14.04 X64
<img src="img/droplet.png">

### Step 2: Change your Domain Name Server (DNS)
    ns1.digitalocean.com
    ns2.digitalocean.com
    ns3.digitalocean.com

### Check that your DNS has changed:
    whois nameofdomain.com


### Step 3: Add Domain and Record on Digital Ocean
### Add domain
<img src="img/domain.png">

### Add record
Networking -> Domains -> Click loop icon to view records
<img src="img/record.png">

### Step 4: SFTP into your IP address
    root@11.22.33.44.55
    Entered password when asked.

### Step 5: Install [ meteor up ](https://github.com/arunoda/meteor-up)
    npm install -g mup

### Creating a Meteor Up Project

    mkdir ~/my-meteor-deployment
    cd ~/my-meteor-deployment
    mup init

This will create two files in your Meteor Up project directory:

  * mup.json - Meteor Up configuration file
  * settings.json - Settings for Meteor's [settings API](http://docs.meteor.com/#meteor_settings)

`mup.json` is commented and easy to follow (it supports JavaScript comments).

### Example File

```js
{
  // Server authentication info
  "servers": [
    {
      "host": "hostname",
      "username": "root",
      "password": "password",
      // or pem file (ssh based authentication)
      //"pem": "~/.ssh/id_rsa",
      // Also, for non-standard ssh port use this
      //"sshOptions": { "port" : 49154 },
      // server specific environment variables
      "env": {}
    }
  ],

  // Install MongoDB on the server. Does not destroy the local MongoDB on future setups
  "setupMongo": true,

  // WARNING: Node.js is required! Only skip if you already have Node.js installed on server.
  "setupNode": true,

  // WARNING: nodeVersion defaults to 0.10.36 if omitted. Do not use v, just the version number.
  "nodeVersion": "0.10.36",

  // Install PhantomJS on the server
  "setupPhantom": true,

  // Show a progress bar during the upload of the bundle to the server.
  // Might cause an error in some rare cases if set to true, for instance in Shippable CI
  "enableUploadProgressBar": true,

  // Application name (no spaces).
  "appName": "meteor",

  // Location of app (local directory). This can reference '~' as the users home directory.
  // i.e., "app": "~/Meteor/my-app",
  // This is the same as the line below.
  "app": "/Users/arunoda/Meteor/my-app",

  // Configure environment
  // ROOT_URL must be set to https://YOURDOMAIN.com when using the spiderable package & force SSL
  // your NGINX proxy or Cloudflare. When using just Meteor on SSL without spiderable this is not necessary
  "env": {
    "PORT": 80,
    "ROOT_URL": "http://myapp.com",
    "MONGO_URL": "mongodb://arunoda:fd8dsjsfh7@hanso.mongohq.com:10023/MyApp",
    "MAIL_URL": "smtp://postmaster%40myapp.mailgun.org:adj87sjhd7s@smtp.mailgun.org:587/"
  },

  // Meteor Up checks if the app comes online just after the deployment.
  // Before mup checks that, it will wait for the number of seconds configured below.
  "deployCheckWaitTime": 15
}
```

### Setting Up a Server

    mup setup

This will setup the server for the `mup` deployments. It will take around 2-5 minutes depending on the server's performance and network availability.

### Deploying an App

    mup deploy

This will bundle the Meteor project and deploy it to the server.





<h3> Follow me on twitter or visit my blog<h3>
  <li><a href="https://twitter.com/tizolj"> tizolj</a></li>
  <li><a href="http://josetizol.com/"> josetizol.com</a></li>
