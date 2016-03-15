CirruxCache provides a software solution to dynamically cache HTTP objects on Google Appengine (using the Datastore and the Memcache services).

This application implements several features usually provided by professional CDN solutions, such as:
  * honor Cache-Control
  * cache TTL override
  * several POP (Point Of Presence) configuration mapped on custom base-url
  * ignore query string
  * POST forwarding
  * garbage collection of expired entries
  * extensibility (develops your own WebServices on top)
  * allow object flushing from restricted IP
  * configure a POP (Point of Presence) according to a virtual host
  * several behaviors (cache, redirect, forward)
  * storage WebService (store big files <=2GB in order to be delivered)
  * admin panel (flush objects, manage big files, statistics, config helper)
  * image transformation (before caching it)

CirruxCache speeds up any HTTP based application (such as dynamic websites or web-services).

This application was used as a CDN front in production conditions at Zoomorama.

CirruxCache has been written by Samuel Alba <sam.alba 'at' gmail.com>.

**If you have any question or need help, please subscribe to the [mailing-list](http://groups.google.com/group/cirruxcache) and send your message.**

**You can follow the project [news](http://shad.cc/tag/cirruxcache), [updates](http://code.google.com/p/cirruxcache/updates/list) and [my twitter](http://twitter.com/sam_alba).**

**If you enjoy this project, you can [make a donation](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=sam%2ealba%40gmail%2ecom&lc=FR&item_name=CirruxCache&item_number=CirruxCache&currency_code=EUR&bn=PP%2dDonationsBF%3abtn_donate_LG%2egif%3aNonHosted).**

![http://code.google.com/appengine/images/appengine-silver-120x30.gif](http://code.google.com/appengine/images/appengine-silver-120x30.gif)