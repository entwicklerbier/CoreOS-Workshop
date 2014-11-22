Cluster
-------

::

    fleetctl list-machines


Unit lifecycle
--------------

::

    fleetctl submit hello.service
    fleetctl list-unit-files

    fleetctl start hello.service
    fleetctl list-units

    fleetctl stop hello.service
    fleetctl list-units

    fleetctl destroy hello.service
    fleetctl list-unit-files


Unit info
---------

::

    fleetctl status hello.service
    fleetctl ssh hello.service
    fleetctl journal hello.service

The local machine must be authorized to connect with its SSH key to the machine
running the unit.
