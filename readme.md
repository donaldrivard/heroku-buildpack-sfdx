# Heroku-Buildpack-SFDX

Deploy SFDX apps to Salesforce scratch orgs via Heroku.

These instructions walk through local sfdx CLI setup and
Heroku-based deployment of the Salesforce Dreamhouse demo app.

## Join the Salesforce SFDX Pilot

[Sign up here](http://go.pardot.com/l/27572/2017-01-23/6gh89x).

Throughout these instructions we'll use *your@pilot.email*.

## Install SFDX locally

1. Check the [manifest](https://developer.salesforce.com/media/salesforce-cli/manifest.json).
2. Download the file for your operating system.
3. Run `sfdx/install` to install the sfdx CLI.

Check to be sure it's installed and up-to-date in your terminal:

```
$ sfdx update
```

## Log in to the Developer Hub

Use your SFDX Pilot email:

```
$ sfdx force:auth:web:login -d -a 'Hub Org'
```

When prompted, authorize the SFDX "Global Connected App."

## Clone the Dreamhouse Demo

```
$ git clone https://github.com/hunterloftis/sfdx-dreamhouse
$ cd sfdx-dreamhouse
```

## Create a new Heroku App

```
$ heroku create --buildpack https://github.com/hunterloftis/heroku-buildpack-sfdx
```

## Configure the app

```
$ heroku config:set SFDX_DESCRIPTION="$(sfdx force:org:describe --verbose --json -u your@pilot.email)"
```

This stores metadata (like your pilot username and Dev Hub auth url) as config on the Heroku app.

## Deploy

```
$ git push heroku master
$ heroku open
```

Scratch orgs have DNS entries on salesforce sub-domains,
so sometimes it takes a few minutes before the url is available.

Your Heroku app will automatically redirect you to and log you into your new SFDX Scratch Org.
Now you can check out the Dreamhouse app you deployed:

### 1. Click setup
![setup](https://user-images.githubusercontent.com/364501/27246563-496b3a56-52a7-11e7-85aa-94b92920e993.png)


### 2. Open the Dreamhouse app
![dreamhouse](https://user-images.githubusercontent.com/364501/27246561-4967df32-52a7-11e7-87d1-a2a9875b594b.png)

### 3. Lovely!
![app](https://user-images.githubusercontent.com/364501/27246562-496accb0-52a7-11e7-8340-19c234cf21c3.png)

