.. _js_lib:

Javascript Client Library
==========================

Basic Usage Example
^^^^^^^^^^^^^^^^^^^^

.. sourcecode:: javascript

    var client = new Gorealtime('<APP_KEY>')
    client.on('my_channel', function(data) {
        alert(data.message);
    });

.. js:class:: Gorealtime(app_key, verbose)

    :param string app_key: Your application key (**not** secret!)
    :param boolean verbose: Log messages to console if true (default ``false``)

    .. js:function:: on(channel, callback)

        Calls ``callback`` with message data when a message is pushed
        down ``channel``. Subscription to that channel will be added
        if it doesn't already exist.

        See :ref:`js_callbacks`

        :param string channel: The name of a channel
        :param function callback: Function to call with message data

    .. js:function:: off(channel)

        Removes callback and unsubscribes from ``channel``

        :param string channel: The name of a subscribed channel


    .. js:function:: subscribe(channel[, channel, ...])

        Subscribes to updates to these channels.
        All arguments to this function are considered to be channels

        :param string channel: The name of a channel to subscribe to

    .. js:function:: unsubscribe(channel[, channel, ...])

        Unsubscribes from updates to these channels.
        All arguments to this function are considered to be channels

        :param string channel: The name of a channel to unsubscribe from


.. _js_callbacks:

Callbacks
^^^^^^^^^^

Callbacks should accept one param, which will be an object
structured like so.

.. sourcecode:: json

    {
        "type": "message",
        "channel": "my_chan",
        "message": "Hello World!"
    }
