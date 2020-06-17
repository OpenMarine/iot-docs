Public MQTT Broker
##################

.. note::
	OpenMarine Public MQTT Broker is in beta stage

.. admonition:: Public server details

	:Protocol: ``TCP``
	:Adress: ``mqtt.openmarine.net``
	:Port: ``1883``

OpenMarine public MQTT Broker is open to everyone and does not require a username or password.

Allowed topics
**************

You can only do these actions on these topics:

**Publish**

``<client ID>/signalk/delta``

``<client ID>/signalk/key/#``

You can only publish data on topics that contain your client ID at the first level. The client ID must be unique, so it is a good idea to use your Signal K UUID or your MMSI. No one but you can publish on these topics. \# is used to match all subsequent levels of hierarchy.

Examples:

:topic: vessels.urn:mrn:imo:mmsi:234567890/signalk/delta

:payload: {"context": "vessels.urn:mrn:imo:mmsi:234567890","updates": [{"source": {"label": "N2000-01","type": "NMEA2000","src": "017","pgn": 127488},"timestamp": "2010-01-07T07:18:44Z","values": [{"path": "propulsion.0.revolutions","value": 16.341667}]}]}

:topic: vessels.urn:mrn:imo:mmsi:234567890/signalk/key/propulsion/0/revolutions

:payload: 16.341667

.. caution::
	Anyone can subscribe to your topics on the public server so do not send sensitive information

**Subscribe**

``+/signalk/delta``

``+/signalk/key/#``

You can subscribe to any topic sent from any client. \+ is used to match a single level of hierarchy. \# is used to match all subsequent levels of hierarchy.

Examples:

:topic: vessels.urn:mrn:imo:mmsi:234567890/signalk/delta

:topic: vessels.urn:mrn:imo:mmsi:234567890/signalk/key/propulsion/0/revolutions

.. caution::
	Use wildcards wisely. If you subscribe to this topic: *+/signalk/delta* or to this one: *+/signalk/key/#* you will receive all messages sent by all clients in the server and you will get thousands of messages colapsing your client.
