*****************************************
CoreOS shortcomings and Management layers
*****************************************

There are already some Management Layers for Core OS:

Kubernetes
==========

Worked on by Core OS and Google. Very early in it's development. There is not a
lot of friendly tooling in there and only very few administrator documentation.
At the moment it is a technical demo.

More information at `Kubernetes Github Repository`_ 



Deis
====

Is on top of fleet. Much smaller than kubernetes. Definitely more tested.

More information at `deis`_ 


Practical Shortcomings of Core OS
=================================

Let's say we have a cluster of applications. Things like `subgun`_ work really
well because it's very elastic. Most applications are not designed to be
elastic, e.g. Wordpress.


Wordpress
---------

* PHP
* DB
* Caching


If you are doing a workload that is very depending on files on disk you have to
find some kind of transport mechanism, e.g. `Mysql Galera Cluster`_ with etcd.
This can be solved by using more elaborate databases like cassandra or riak but
is not solvable in an optimal way without changing existing applications like
wordpress.


.. Links
.. _deis: http://deis.io/
.. _Kubernetes Github Repository: https://github.com/GoogleCloudPlatform/kubernetes/blob/master/DESIGN.md
.. _Mysql Galera Cluster: http://galeracluster.com/products/
.. _subgun: https://github.com/coreos/subgun
