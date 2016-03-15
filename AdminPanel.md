# Introduction #

CirruxCache now provides an admin panel in order to:
  * Flush objects
  * Upload static object on the Store service
  * Get some statistics on the Resource use
  * Generate or edit configuration files

To load the admin panel, go to your CirruxCache domain at: http:// **appname**.appspot.com/`_`admin/

# Details #

## Flush panel ##

Here you can purge a list of URL (one per line) following this form:
  * http://www.mysite.tld/my_file.ext
  * /my\_file.ext
  * http://www.mysite.tld/
  * /

[http://cdn.zaphod.eu/cirruxcache/flush.png?width=600](http://cdn.zaphod.eu/cirruxcache/flush.png)

## Store panel ##

Here you can add files to the store service. To add a file, you need to map it on a URL.
The URL mapping is totally virtual, it does not correspond to a physical path, so you can create any file mapping you want.

This panel uses the [StoreAPI](StoreAPI.md), so you can do exactly the same thing from your code.

[http://cdn.zaphod.eu/cirruxcache/store.png?width=600](http://cdn.zaphod.eu/cirruxcache/store.png)

## Stats panel ##

This page gives you some stats from your Appengine account.
_This panel will be completed in future releases._

[http://cdn.zaphod.eu/cirruxcache/stats.png?width=600](http://cdn.zaphod.eu/cirruxcache/stats.png)

## Config panel ##

This panel helps you to generate config files (config.py). The config file is written in Python and can be disappointing for people who are not familiar with programming.

On this panel, you are able to add [PoP (services)](PoP.md), and map them on different URLs.

An interesting thing is that you can access documentation for each [PoP](PoP.md) variable by moving your cursor over the "?" character.

[http://cdn.zaphod.eu/cirruxcache/config.png?width=600](http://cdn.zaphod.eu/cirruxcache/config.png)