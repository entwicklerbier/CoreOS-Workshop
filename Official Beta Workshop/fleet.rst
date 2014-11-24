*****
Fleet
*****

Fleet is a systemd unit manager and offers the possibilities of the `Systemd
unit options`_ and many more systemd features. Best to start with looking at
`Deploying a Service using fleet`_


Starting units
--------------

.. code-block:: bash

	# start unit
    fleetctl start <service>


Fleet unit files
----------------

Fleet offers functionality of systemd unit files and `fleet specific unit options`_ 

| **For Example**
| X.Conflicts=hello*.servce: Unit can not run anywhere else where there is an
| existing hello*.service

.. code-block:: bash

    fleetctl start hello* # * starts it on every machine


Unit file arguments
-------------------
template-unit: Units you can give arguments with.

.. code-block:: bash

    fleetctl list-units -a # show inactive units as well


Push unit changes to all servers
--------------------------------

You would have a presence service that understands how to do the handling with a
load balancer, see `Deploying a Service using fleet`_ for a deployment using AWS
load balancer.


.. links
.. _Deploying a Service using fleet: https://coreos.com/docs/launching-containers/launching/fleet-example-deployment/
.. _fleet specific unit options: https://coreos.com/docs/launching-containers/launching/fleet-unit-files/
.. _Systemd unit options: http://www.freedesktop.org/software/systemd/man/systemd.service.html#Options
