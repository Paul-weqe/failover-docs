Installation
============

+++++++++++++++++++++++++++++++
Failover Installation(via snap)
+++++++++++++++++++++++++++++++

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

+++++++++++++++++++++++++++
Running via cargo build
+++++++++++++++++++++++++++

Some may choose to install the project via a manual build using `cargo <https://doc.rust-lang.org/cargo/>`_.
This will need us to have cargo and rust both installed in our system.

For this, we will first need to download the repository from Github and navigate to the directory:

.. code-block:: bash

    git clone https://github.com/Paul-weqe/failover


If you already have cargo installed in your system, build the project:

.. code-block:: bash

    cargo run --bin failover

Note that running this command will require sudo permisions.

Make sure that once your are done running, you run the following command:

.. code-block:: bash

    cargo run --bin failover --teardown


To avoid going command by command, we can run the ``run.sh`` script immediately after cloning the repository:

.. code-block:: bash

    ./run.sh
