Introduction
============

.. toctree::
   :maxdepth: 3

   install
   config


Failover is a VRRP implementation made in Rust. Currently, it is specifically designed for Ubuntu but will soon be customized for other Linux environments. 

+++++++++++++
VRRP Overview
+++++++++++++


VRRP is a redundancy protocol defined under `RFC 3768 <https://datatracker.ietf.org/doc/html/rfc3768>`_. 
The protocol was primarily made for network routers to offer an alternative router that the network can rely on without having to change configurations. 

For example in the image shown below: 

.. image:: https://github.com/Paul-weqe/failover/blob/main/images/vrp-illustration.png?raw=true
    :width: 400
    :alt: VRRP illustration


In the above illustration, the green router(192.168.1.3) will be the virtual router. 
Between SW1(192.168.1.1) and SW2(192.168.1.2), one of them can be the owner of this virtual router. 
The owner is known as the **MASTER** and the rest of the routers are known as **BACKUP** routers. 

We will take this protocol and implement it on Ubuntu, meaning we can replace the routers with servers where we ensure redundancy for the servers.


There are two methods in which we can run Failover:


* Installling via the `snap store <https://snapcraft.io/failover>`_.
* Compiling locally using cargo.

