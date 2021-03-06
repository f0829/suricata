Generic App Layer Keywords
==========================

app-layer-protocol
------------------

Match on the detected app-layer protocol.

Syntax::

    app-layer-protocol:[!]<protocol>;

Examples::

    app-layer-protocol:ssh;
    app-layer-protocol:!tls;
    app-layer-protocol:failed;

A special value 'failed' can be used for matching on flows in which
protocol detection failed. This can happen if Suricata doesn't know
the protocol or when certain 'bail out' conditions happen.

.. _proto-detect-bail-out:

Bail out conditions
~~~~~~~~~~~~~~~~~~~

Protocol detection gives up in several cases:

* both sides are inspected and no match was found
* side A detection failed, side B has no traffic at all (e.g. FTP data channel)
* side A detection failed, side B has so little data detection is inconclusive

In these last 2 cases the ``app-layer-event:applayer_proto_detection_skipped``
is set.


app-layer-event
---------------

Match on events generated by the App Layer Parsers and the protocol detection
engine.

Syntax::

  app-layer-event:<event name>;

Examples::

    app-layer-event:applayer_mismatch_protocol_both_directions;
    app-layer-event:http.gzip_decompression_failed;

Protocol Detection
~~~~~~~~~~~~~~~~~~

applayer_mismatch_protocol_both_directions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The toserver and toclient directions have different protocols. For example a
client talking HTTP to a SSH server.

applayer_wrong_direction_first_data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Some protocol implementations in Suricata have a requirement with regards to
the first data direction. The HTTP parser is an example of this.

https://redmine.openinfosecfoundation.org/issues/993

applayer_detect_protocol_only_one_direction
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Protocol detection only succeeded in one direction. For FTP and SMTP this is
expected.

applayer_proto_detection_skipped
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Protocol detection was skipped because of :ref:`proto-detect-bail-out`.

