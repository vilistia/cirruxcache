# Introduction #

CirruxCache uses a garbage collecting cron task to flush expired entries.


# Details #

When CirruxCache make a request through the a Cache PoP, the fetched object is stored with a TTL. Once the TTL is reached, if the object is fetched again, its meta information are refreshed, with its content if needed.

But a lot of objects remain on the Datastore without being refreshed. For instance, if the resource is removed from the origin.

That's why a garbage collector needs to be called from a cron task.

**Keep in mind that the delay of the garbage collector iteration influences your [resource quota](http://code.google.com/appengine/docs/quotas.html) usage.**

For instance, I use a refresh delay of:
  * 1 week on my personal blog (because static almost never change).
  * 15 minutes on big production servers (to keep storage as clean as possible).

**To change the garbage collector delay, edit the file "cron.yaml" and change the "schedule" property.**