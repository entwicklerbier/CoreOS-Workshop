******************
CoreOS information
******************

Cloud Config
============
Every coreos instance is configured with the provided user-data.yml. When running coreOs install, cloud-config is placed as user-data.yml in /var/lib/coreos-install/user_data

This file is evaluated at boot time.

Config can be in /usr/share/oem/.


Variables
=========
* https://coreos.com/docs/cluster-management/setup/cloudinit-cloud-config/


Namespaces
==========
Docker takes advantage of a technology called namespaces to provide the isolated workspace we call the container. When you run a container, Docker creates a set of namespaces for that container.

This provides a layer of isolation: each aspect of a container runs in its own namespace and does not have access outside it.

Some of the namespaces that Docker uses are:

The pid namespace: Used for process isolation (PID: Process ID).
The net namespace: Used for managing network interfaces (NET: Networking).
The ipc namespace: Used for managing access to IPC resources (IPC: InterProcess Communication).
The mnt namespace: Used for managing mount-points (MNT: Mount).
The uts namespace: Used for isolating kernel and version identifiers. (UTS: Unix Timesharing System).


Control groups
==============
Docker also makes use of another technology called cgroups or control groups. A key to running applications in isolation is to have them only use the resources you want. This ensures containers are good multi-tenant citizens on a host. Control groups allow Docker to share available hardware resources to containers and, if required, set up limits and constraints. For example, limiting the memory available to a specific container.


etcd
====

Changing leader all the times...
etcd treats the name as the identifier for a node.


Remove all data and create new cluster
--------------------------------------

::

	URL=https://discovery.etcd.io/...

	systemctl stop etcd
	rm -r /var/lib/etcd/*

	bash <<EOF
	sed -i 's|discovery: .*|discovery: ${URL}|' /var/lib/coreos-install/user_data
	sed -i 's|ETCD_DISCOVERY=.*|ETCD_DISCOVERY=${URL}"|' /run/systemd/system/etcd.service.d/20-cloudinit.conf
	EOF

	systemctl daemon-reload
	systemctl start etcd

	journalctl -fu etcd
