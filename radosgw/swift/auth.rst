======
 认证
======

需要认证的 Swift API 请求必须在请求头里带上 ``X-Storage-Token`` 认证令牌。\
此令牌可以从 RADOS 网关、或别的认证器获取，要从 RADOS 网关获取的话需创建用\
户，例如： ::

	sudo radosgw-admin user create --uid="{username}" --display-name="{Display Name}"

For details on RADOS Gateway administration, see `radosgw-admin`_. 

.. _radosgw-admin: ../../../man/8/radosgw-admin/ 

Auth Get
--------

To authenticate a user, make a request containing an ``X-Auth-User`` and a
``X-Auth-Key`` in the header.

Syntax
~~~~~~

::

    GET /auth HTTP/1.1
    Host: swift.radosgwhost.com
    X-Auth-User: johndoe
    X-Auth-Key: R7UUOLFDI2ZI9PRCQ53K

Request Headers
~~~~~~~~~~~~~~~

``X-Auth-User`` 

:Description: The key RADOS GW username to authenticate.
:Type: String
:Required: Yes

``X-Auth-Key`` 

:Description: The key associated to a RADOS GW username.
:Type: String
:Required: Yes


Response Headers
~~~~~~~~~~~~~~~~

The response from the server should include an ``X-Auth-Token`` value. The 
response may also contain a ``X-Storage-Url`` that provides the 
``{api version}/{account}`` prefix that is specified in other requests
throughout the API documentation.


``X-Storage-Token`` 

:Description: The authorization token for the ``X-Auth-User`` specified in the request.
:Type: String


``X-Storage-Url`` 

:Description: The URL and ``{api version}/{account}`` path for the user.
:Type: String

A typical response looks like this:: 

	HTTP/1.1 204 No Content
	Date: Mon, 16 Jul 2012 11:05:33 GMT
  	Server: swift
  	X-Storage-Url: https://swift.radosgwhost.com/v1/ACCT-12345
	X-Auth-Token: UOlCCC8TahFKlWuv9DB09TWHF0nDjpPElha0kAa
	Content-Length: 0
	Content-Type: text/plain; charset=UTF-8
