****
ETCD
****

Etcd is a highly-available key value store for shared configuration and service
discovery. Additionally it is used by kubernetes for it's data sharing engine.


RAFT
====

RAFT is the protocol used by etcd. We have a follower and proxy (coming soon).

RAFT writes the index and any changes that should be created in the RAFT logs.
RAFT is pushing out the changes that happen via WAL (see below). Therefore
changes can be rolled back if they go haywire. Just as in the CoreOS updates,
changes are tracked to guarantee updates run smoothly.

Everytime an update is pushed, the WAL and the DIS (Database itself) have to be
updated. On top of the logs, there are snapshots. fsync(); : Guarantees that a
process that is writing something on disk confirms that it's been written. On
every change, all nodes have to confirm the change. Therefore, the fastest we
can ever get is the slowest node in the whole etcd-cluster.

The more `IOPS`_ you can provide to etcd, the better the performance.

For tuning a DB-workflow you could change the sector size of a disk (changing
512 to 4k e.g.).


| **Therefore:**
| 1. Disk is our most important tuneable.
| 2. Network latency is the second most important tuneable.

For more information about RAFT, look at this `RAFT visualization`_ 


WAL
---

1. Write the change to the logfile
2. Make the change in database
3. Commit the change to our logfile

More information at `Wikipedia WAL`_ 


Practical ETCD
==============

.. code-block:: bash

	# Set etcdctl key via cli and curl
    etcdctl set /foo bar
    curl -X PUT http://IP-ADDR:4001/v2/keys/foo -d value=bar

    # get keys via cli and curl
    etcdctl get /foo
    curl -X GET http://IP-ADDR:4001/v2/keys/foo

    # list locksmith keys via cli
    # (locksmith is the Core OS reboot manager)
    etcdctl ls /
    etcdctl ls /coreos.com
    etcdctl ls /coreos.com/updateengine
    etcdctl --recursive ls /coreos.com/updateengine
    etcdctl ls /coreos.com/updateengine    

    # browse hidden namespace
    etcdctl --recursive ls /_coreos.com/



By default etcdctl tries the localhost address. Use --peers to avoid this.
Reason to default to localhost is a guarantee this address is available.


.. Tear down and rebuild
.. ---------------------

.. https://coreos.com/docs/distributed-configuration/etcd-api/#cluster-config

.. 1. Look up srv-srv config: curl -L http://127.0.0.1:7001/v2/admin/config



.. Resolve can not sync with cluster using peers:
.. peer is removed if heartbeat does not find it after a while

.. You could use etcdctl -C IP:4001 get /foo to get the data back.



Debugging etcd
==============

Example: Error "too many redirects"
-----------------------------------

Address is not properly advertised. Start etcd in verbose mode on all machines
and look at the output.

.. code-block:: bash

	# Look at the etcd output
    journalctl -u ectd.service # on each machine

    # Turn on verbosity
	cd /etc/systemd/system
	systemctl cat etcd.service

	# Copy and paste the first drop in to overwrite it
	sudo vim etcd.service

	# put in the first drop in
	ExedStart: etcd -vv

	systemctl daemon-reload

	# you should now see verbose debug information of etcd
	journalctl -u ectd.service






Discovery URL security concerns
-------------------------------

Machine IDs are not actually useful. 

Hardest part to get an etcd cluster running is the boostrap process. 

If you want you can run `Your Own Discovery Service`_ . But take care that the
`discovery url is not configureable atm`_




.. links
.. _discovery url is not configureable atm: https://github.com/coreos/discovery.etcd.io/issues/3
.. _IOPS: http://de.wikipedia.org/wiki/Input/Output_operations_Per_Second
.. _RAFT visualization: http://thesecretlivesofdata.com/raft/
.. _Wikipedia WAL: http://en.wikipedia.org/wiki/Write-ahead_logging
.. _Your Own Discovery Service: https://github.com/coreos/discovery.etcd.io
