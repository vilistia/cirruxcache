# Introduction #

The Image service (or [PoP](PoP.md)) is based on the Cache service. It should only used to cache images. It supports image transformation in order to serve transformed images (resize, crop, rotate, ...).

Really useful for embedded images in a website, it avoids the use of several images (preview, medium sized, full size). You only need to store the original image on your origin server, and delegate transformations to CirruxCache. On top of that, transformed images are cached in the same way than any other objects.


# Details #

Let's take an example where you mapped an Image [PoP](PoP.md) on http://cdn.mydomain.tld/images/ and you put the file "my\_image.png" on your origin server.

| **Request** | **Description** |
|:------------|:----------------|
| `http://cdn.mydomain.tld/images/my_image.png` | Get the original image. |
| `http://cdn.mydomain.tld/images/my_image.png?width=100&height=200` | Resize the image, keeping the aspect ratio. Only one parameter can be set. |
| `http://cdn.mydomain.tld/images/my_image.png?rotate=90` | Rotate the image. Takes degrees which must be multiple of 90. |
| `http://cdn.mydomain.tld/images/my_image.png?horizontal_flip` | Flip image horizontally. |
| `http://cdn.mydomain.tld/images/my_image.png?vertical_flip` | Flip image vertically. |
| `http://cdn.mydomain.tld/images/my_image.png?crop=1.0-0.4-0.3-1.0` | Crop image. Parameters are separated with a '-' and are respectically: left, top, right, bottom. |
| `http://cdn.mydomain.tld/images/my_image.png?enhance` | Adjust color and contrast. |

Each request can be combined: `my_image.png?enhance&width=50&rotate=90`

For more information, check out the [Appengine Images API overview.](http://code.google.com/appengine/docs/python/images/overview.html)