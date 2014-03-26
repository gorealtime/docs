.. _api latest:

API version 1
==============

Version 1 of the API is still in development and subject to
changes.


.. _authentication:

Authentication
---------------

Authenticating the push endpoint is simple once you know how.

You take the application's secret key and compute a hmac-sha256
signature of the payload's message. If you've never done that
before, don't worry, it sounds more complicated than it is.
Chances are there is a library to do it for you in your language
of choice, if it's not already in the standard library!

Here's an example of what I mean::

    >>> from hashlib import sha256
    >>> import hmac
    >>> secret = 'ssshh'
    >>> message = 'Hello World!'
    >>> signature = hmac.new(secret, message, sha256).hexdigest()
    >>> print signature
    8650decb780ea45364e7a6f9f8cbb3c87f75777910366359ae0c4aeca1db763a


Endpoints
----------

All API requests are made over HTTPS, to a base URL of https://api.gorealti.me

Data must be sent as JSON, with a ``Content-Type: application/json`` header.


Push
^^^^^

.. http:post:: /v1/push

    :statuscode 202: Ok
    :statuscode 400: Request data incorrect or missing
    :statuscode 401: Invalid signature


    **Request data**

    :json string app: app key
    :json string message: data to push to client
    :json string signature: signature created with app secret, see :ref:`authentication`
    :json list channels: list of channels to push message to

    **Response**

    .. sourcecode:: http

        HTTP/1.1 202 OK
        Vary: Accept
        Content-Type: application/json

        {
            "accepted": true
        }


