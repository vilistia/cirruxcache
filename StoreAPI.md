# Introduction #

This page describes how to add big files on the Store WebService exactly in the same way of the admin panel.

This WebService has been developed to bypass the 1MB limit of appengine. It is not possible to dynamically cache objects with a size greater than 1MB, in this case, you need to store explicitly such an object using this WebService. It uses [the Blobstore service](http://code.google.com/appengine/docs/python/blobstore/overview.html), so file size cannot exceed 2GB.


# Details #

_We assuming that the store WebService is mapped on /**store/, which is the default value. So if you make your mapping on a different base URL, beware of the doc below.**_

| **Method** | **Request URI** | **Return** | **Description** |
|:-----------|:----------------|:-----------|:----------------|
| GET        | /`_`store/_<new path>_/new | /`_`ah/upload/_<unique id>_ | Allocate a new upload point |
| POST | PUT | /`_`ah/upload/_<unique id>_ | None       | Post the file to the previous allocated POST point |
| GET        | /`_`store/_<new path>_ | The file   | Fetch the uploaded file. |
| DELETE     | /`_`store/_<new path>_ | None       | Delete the uploaded file. |

A request succeed if it returns a success HTTP code (2xx or 3xx).

# Example #

This example is real trace made on the development server.

**Request**

```
GET /_store/my/new/remote/file/new HTTP/1.1
Host: localhost:8080
Cookie: dev_appserver_login="test@example.com:True:185804764220139124118"
```

**Response**

```
HTTP/1.0 200 OK
Server: Development/1.0
Content-Length: 63

/_ah/upload/agdhcHBuYW1lchsLEhVfX0Jsb2JVcGxvYWRTZXNzaW9uX18YAQw
```

**Request**

```
POST /_ah/upload/agdhcHBuYW1lchsLEhVfX0Jsb2JVcGxvYWRTZXNzaW9uX18YAQw HTTP/1.1
Host: localhost:8080
Cookie: dev_appserver_login="test@example.com:True:185804764220139124118"
Content-Type: multipart/form-data; boundary=---------------------------567950583882997196254290631
Content-Length: 6963

<data multipart encoded>
```

**Response**

```
HTTP/1.0 302 
Server: Development/1.0
Content-Length: 0
```

_I know this 302 response without "Location" is crappy, but this is mandatory to follow the Blobstore API._