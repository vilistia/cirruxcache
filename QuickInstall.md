# Introduction #

First of all, it is important to understand why CirruxCache does not have a configuration file. This problem is due to the AppEngine platform: an application running on AppEngine is a kind of a simple CGI script called each time your application need to handle a request. For a better performance, your files are cached according to the location, so each first request can be slower if it is the first time that your application is accessed from a location.

In conclusion, AppEngine does not keep a running instance of your application. It is critical for each application on AppEngine to start as quick as possible, so parsing of a configuration file each time your app execute a request is a bad point if you need to keep a low cpu time quota.


# AppEgnine #

## Get an account ##

If you don't own an appengine account, the first thing to do is to open one. Go to https://appengine.google.com/ and log in with your google account credentials. Then, click on "create an application" and follow the steps.

"Application Identifier" is the name of your application. In this example, I'll take "appname".


## Get the SDK ##

Then, you need the AppEngine SDK for Python to deploy the CirruxCache application. Get it for your operating system at http://code.google.com/appengine/downloads.html#Google_App_Engine_SDK_for_Python

Now make sure you can execute the script appcfg.py (or the User Interface). That's the only one script you need to deploy CirruxCache.


# CirruxCache #

## Download ##

First of all, you need to [download the latest package](http://code.google.com/p/cirruxcache/downloads/list).


## First configuration ##

Edit the file "app.yaml" as follow:

```
application: appname
```

Replace "appname" by the name of your appengine application (**appname**.appspot.com).

You don't need to modify any other lines in this file. Do it only if you know what you do.

**You can skip this step by overriding the appname with the "-A" option of appcfg.py during the deployment.**

## Configuring a PoP (Point Of Presence) ##

Edit the file "config.py", and considers the part below:

```
# POP definition
# You can define and configure your Point Of Presence

class Static(cache.Service):
        origin = 'http://static.mydomain.tld'
        maxTTL = 2592000 # 1 month
        ignoreQueryString = True

class Www(cache.Service):
        origin = 'http://www.mydomain.tld'
        forceTTL = 3600 # 1 hour
        ignoreQueryString = True
        forwardPost = False

# !POP
```

You can configure as many [PoPs](PoP.md) as you need. In this example, we have two [PoPs](PoP.md) named respectively "Static" and "Www".

There are several service types for each PoP.

**To better understand the PoP configuration, I invite you to read [the reference doc for the PoP configuration variables](PoP.md).**


## URL mapping ##

Once your Points Of Presence has been configured, you have to bind them on base URLs.

Edit the file "config.py", and considers the part below:

```
urls['default'] = (
        '(/data/.*)', 'config.Static',
        '/www(/.*)', 'config.Www'
  )
```

In this example, "Static" and "Www" PoPs are mapped respectively to "/static/" and "/www/". It means that a request on http:// **appname**.appspot.com/**www**/ will be handled by the "Www" PoP, etc...

**It is important to take into account the URL matching**, for example:
  * In the case of "Static", the request will be done to the URL `http://static.mydomain.tld/data/...`
  * In the case of "Www", the request will be done to the URL `http://www.mydomain.tld/...`

_Notice: If you need only one PoP, you can map it on the root URL by replacing the Root PoP in the configuration above._

### Virtual Hosting ###

All of this urls are mapped to the "default" virtual host. It is a kind of catch-all. But you can specify other mapping such as:

```
urls['cdn.domain.tld'] = {
  '(/.*)', 'config.Blog'
}
```

This settings will bind the PoP named "Blog" to all url which are accessed through the "cdn.domain.tld" virtual host.


## Test your configuration ##

The AppEngine SDK contains a script named "dev\_appserver.py". This script is a test web server that can run the CirruxCache application in a test environnement. It is useful to test if your configuration matches your requirements.

To run it, go to the CirruxCache directory, where you made your configuration and run:

```
dev_appserver.py .
```

The trailing dot indicates to the script where to find the app.yaml file.

Then, open your web browser and go to http://localhost:8080/

_Notice: You could find more documentation at http://code.google.com/appengine/docs/python/tools/devserver.html_


## Deploy CirruxCache on your AppEngine account ##

Once you finished the configuration, following the steps above, it is the moment to deploy the app.

It is very simple, go to the CirruxCache directory and run:

```
appcfg.py update .
```

The trailing dot indicates to the script where to find the app.yaml file.

The script will ask for your appengine credentials (google account).

_Notice: You could find more documentation at http://code.google.com/appengine/docs/python/tools/uploadinganapp.html_


## Need help? ##

If you have any questions about the configuration and/or deployment of the CirruxCache application, do not hesitate to subscribe and post to http://groups.google.com/group/cirruxcache.