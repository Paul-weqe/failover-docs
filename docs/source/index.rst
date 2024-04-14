FAILOVER
========

Failover is a VRRP implementation made in Rust. Currently, it is specifically designed for Ubuntu but will soon be customized for other Linux environments. 

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


+++++++++++++++++++++++++
Installing via snap store
+++++++++++++++++++++++++

Failover is available in the `snap store <https://snapcraft.io/failover>`_. 
Due to restrictions from the snap store, it is currently available only from the ``edge`` restriction. 

Therefore, you can install Failover by running the following command:

.. code-block:: bash
    
    snap install failover --edge --devmode

When Failover is installed, it automatically runs as a daemon. 
You can check on the status of the service via ``systemctl`` using the following command:

.. code-block:: bash
    
    sudo systemctl status snap.failover.main.service

You should see the application running successfully if everything is okay, you should have an output such as the following:

.. image:: https://github.com/Paul-weqe/failover/blob/main/images/failover.png?raw=true
    :width: 400

When installed via `snap`, the Failover configs will be stored at ``/var/snap/failover/common/vrrp-config.json``. 
Look at the 

++++++++++++++++++++++++++
Installing via local build
++++++++++++++++++++++++++

Some may choose to install the project via a manual build using `cargo <https://doc.rust-lang.org/cargo/>`_

For this, we will first need to download the repository from Github and navigate to the directory:

.. code-block:: bash

    git clone https://github.com/Paul-weqe/failover
    cd failover


If you already have cargo installed in your system, build the project:

.. code-block:: bash

    cargo run

Note that running this command will require sudo permisions. 

Make sure that once your are done running, you run the following command:

.. code-block::bash

    cargo run --teardown



To avoid going command by command, we can run the ``run.sh`` script:

.. code-block::bash

    ./run.sh

