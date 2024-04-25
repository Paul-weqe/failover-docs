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

    cargo build


We can now run the project:

.. code-block:: bash

    # the following will require sudo permissions
    ./target/debug/failover file-mode

Make sure that you are root as you are running the above command.

When you are done running `failover`, make sure to take it down via the following command:

.. code-block:: bash

    ./target/debug/failover file-mode --teardown


To avoid going command by command, we can run the ``run.sh`` script immediately after cloning the repository:

.. code-block:: bash

    ./run.sh


There are two command modes you can run Failover with; ``cli-mode`` and ``file-mode``.
The next section will cover how to configure and handle both.