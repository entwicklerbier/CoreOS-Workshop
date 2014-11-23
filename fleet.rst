`Distributed init system using systemd and etcd`

Cluster
-------

::

    fleetctl list-machines


Unit lifecycle
--------------

https://github.com/coreos/fleet/blob/master/Documentation/states.md#unit-states

::

    fleetctl submit
    fleetctl load
    fleetctl start
    fleetctl stop
    fleetctl unload
    fleetctl destroy


Unit info
---------

::

    fleetctl list-unit-files
    fleetctl list-units
    fleetctl status hello.service
    fleetctl ssh hello.service
    fleetctl journal hello.service

The local machine must be authorized to connect with its SSH key to the machine
running the unit.
https://github.com/coreos/fleet/blob/master/Documentation/deployment-and-configuration.md#ssh-keys
