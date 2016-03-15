# Introduction #

A PoP stands for Point Of Presence. Each PoP has its own configuration and is mapped to a specific URL. URL mapping is not handled by the PoP itself, read QuickInstall for more details.


# Reference configuration variables #

This is all the PoP types available for the moment, with their configuration. The first line of each table contains the name of the service with its descriptions, followed by its configuration key and description.

| **Cache** | **This service implements the content delivering caching mechanism. All requests handled by this service produces cache manipulation on the Google Datastore (with a Memcache top layer).** |
|:----------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| - origin  | Set the origin url (type: String; mandatory)                                                                                                                                                |
| - forceTTL | Does not honor CacheControl value, replacing cache TTL by this value (type: Integer)                                                                                                        |
| - maxTTL  | When the Cache-Control value is honored (forceTTL not set), the cache TTL value cannot be greater than this value (otherwise, it is overriden). (type: Integer)                             |
| - ignoreQueryString | Tell if the trailing HTTP query string is not taken into account to generate the cache object key in Datastore. In other terms, if this value is set to True, /url/path/obj.js?v=42 and /url/path/obj.js referer to the same object. (type: Boolean; default: False) |
| - forwardPost | If it is True, POST requests will be forwarded, instead of being redirected (type: Boolean; default: True)                                                                                  |
| - allowFlushFrom | Specify a list of client IPs which are allowed to make DELETE requests to flush cache object explicitly. (type: List)                                                                       |
| - disableIfModifiedSince | Disable IMS request during object refresh. (type: Boolean; default: False)                                                                                                                  |
| - prefetch | (EXPERIMENTAL) Prefetch content from HTML or other pages. Takes a list of ContentType to prefetch. (type: Boolean; default: False)                                                          |
| - headerBlacklist | Set list of origin headers to remove. (type: List)                                                                                                                                          |

| **Forward** | **All requests handled by this service will be forwarded to the origin.** |
|:------------|:--------------------------------------------------------------------------|
| - origin    | Set the origin url (type: String; mandatory)                              |

| **Redirect** | **All requests handled by this service will be redirected to the origin.** |
|:-------------|:---------------------------------------------------------------------------|
| - origin     | Set the origin url (type: String; mandatory)                               |
| - code       | Set the redirection code (type: Integer; default: 301)                     |

| **Image** | **Base on Cache service. Support image transformation.** |
|:----------|:---------------------------------------------------------|
| - origin  | Set the origin url (type: String; mandatory)             |
| - forceTTL | Does not honor Cache-Control value, replacing cache TTL by this value (type: Integer)  |
| - maxTTL  | When the Cache-Control value is honored (forceTTL not set), the cache TTL value cannot be greater than this value (otherwise, it is overriden). (type: Integer) |
| - allowFlushFrom | Specify a list of client IPs which are allowed to make DELETE requests to flush cache object explicitly. (type: List) |
| - disableIfModifiedSince | Disable IMS request during object refresh. (type: Boolean; default: False) |
| - headerBlacklist | Set list of origin headers to remove. (type: List)       |

_[Here you can find more information about the Image service here.](Image.md)_