*****
Fleet
*****

* ssh needed only on instances that have the ssh agents

* https://www.digitalocean.com/community/tutorials/how-to-use-fleet-and-fleetctl-to-manage-your-coreos-cluster

fleet units
===========

units loaded by fleet are stored in etc

.. code-block:: bash

    etcdctl get /_coreos.com/fleet/unit


@
=

.. epigraph::

   Optionally, units may be instantiated from a template file at runtime. This allows creation of multiple units from a single configuration file. If systemd looks for a unit configuration file, it will first search for the literal unit name in the file system. If that yields no success and the unit name contains an "@" character, systemd will look for a unit template that shares the same name but with the instance string (i.e. the part between the "@" character and the suffix) removed. Example: if a service getty@tty3.service is requested and no file by that name is found, systemd will look for getty@.service and instantiate a service from that configuration file if it is found.

   -- http://www.freedesktop.org/software/systemd/man/systemd.unit.html

Read more: http://0pointer.de/blog/projects/instances.html



Fleet-specific Options
======================
.. code-block:: bash

    ##############################
    #   fleet-specific options   #
    ##############################
    
    ; MachineID:
    ; Require the unit be scheduled to the machine identified by the given string.
    ; MachineOf:
    ; Limit eligible machines to the one that hosts a specific unit.
    ; MachineMetadata:
    ; Limit eligible machines to those with this specific metadata.
    ; Conflicts:
    ; Prevent a unit from being collocated with other units using glob-matching on the other unit names.
    ; Global:
    ; Schedule this unit on all agents in the cluster. A unit is considered invalid if options other than MachineMetadata are provided alongside Global=true.
