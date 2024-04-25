VRRP Configuration
==================

Failover has two methods of configuration:

#. File Configuration
#. Cli Configuration


If Failover was installed via ``snap``, we will only have the File Configuration option available to us. However,
when running from the cli, we can use either a config file or the CLI.


++++++++++++++++++
File Configuration
++++++++++++++++++

File configuration in Failover is carried out via JSON files.

First things first, let us start with where the files are stored.
If you installed Failover via ``snap``, Failover is run by default via ``file-mode`` and your json configuration
is stored in: ``/var/snap/failover/common/vrrp-config.json``. If you are running Fialover via cargo,
your json configurations are stored in: ``/etc/failover/vrrp-config.json``.

However, when running via the cargo install, you can customize which json configuration file the it should use by the
``--filename`` subcommand. So you will run the command:
``./target/debug/failover file-mode --filename /custom/path/custom-file.json``.

Now that JSON file location is out of the way, the following is a sample of how the
JSON configuration files should look like:

.. code-block:: json

    {
        "name": "VR_1",
        "vrid": 51,
        "interface_name": "wlo1",
        "ip_addresses": [
            "192.168.100.100/24"
        ],
        "priority": 101,
        "advert_interval": 1,
        "preempt_mode": true
    }


This is the configuration for a single Virtual Router instance. The ``VRID``, ``interface_name`` and ``ip_addresses``
are compulsory fields in this configuration. The rest of the fields either have default values, as described
`here <https://www.rfc-editor.org/rfc/rfc3768.html#section-5.3>`_ in the official RFC or as in the case of ``name`` field,
can be automatically generated.

We advice setting the value for ``name`` as opposed to letting the system generate one for you.
This will help immensely when you are troubleshooting any issues.

You may be worried "what if I need to configure more than one Virtual Router"?
Worry not, we also support configuration of ``multiple virtual routers``. The following is a sample configuration:

.. code-block:: json

    [
        {
            "name": "VR_1",
            "vrid": 51,
            "interface_name": "wlo1",
            "ip_addresses": [
                "192.168.100.100/24"
            ],
            "priority": 101,
            "advert_interval": 1,
            "preempt_mode": true
        },
        {
            "name": "VR_2",
            "vrid": 53,
            "interface_name": "wlo1",
            "ip_addresses": [
                "192.168.100.120/24"
            ],
            "priority": 25,
            "advert_interval": 1,
            "preempt_mode": true
        }
    ]


Restart Failover (via systemctl or stopping and starting the running cli instance) there we have it,
two Virtual Router instances running.

Note that the `name` and each of the `ip_addresses` must be unique and not being used by any other Virtual Router instance.



+++++++++++++++++
CLI configuration
+++++++++++++++++

On the `CLI configuration`, we can make the configurations for the same fields as on the the `File Configuration`.

The main differences are:

#. The place where its run(`CLI` vs `JSON file`)
#. On CLI, we can only configure one Virtual Router, on the file we can configure multiple Virtual Router instances.

The following are the configuration options on CLI:

.. code-block:: bash

    Usage: failover cli-mode [OPTIONS] --vrid <VRID> --interface-name <INTERFACE_NAME>

    Options:
          --name <NAME>
              The name of the Virtual Router Instance. e.g `VR_1`
          --vrid <VRID>
              Virtual Router ID of the Virtual router instance.
          --ip-address <IP_ADDRESS>...
              The IP Address(es) of that will the Virtual router will be assigned. Can be more than one.
          --interface-name <INTERFACE_NAME>
              name of the network interface where the Virtual Router instance will be attached.
          --priority <PRIORITY>
              The priority of this instance of the Virtual Router, maximum of 255. The higher priority is chosen to be MASTER. [default: 100]
          --advert-interval <ADVERT_INTERVAL>
              [default: 1]
          --preempt-mode
              (highly adviced to be called). When true, the higher priority will always preempt the lower priority.
          --action
                Specifies the action we are trying to run on the Virtual Router ('run' or 'teardown').
                'run' is when we are setting up the Virtual router for VRRP. 'teardown' is when we are finished with it.
      -h, --help
              Print help


As specified before, ``VRID``, ``interface_name`` and ``ip_addresses`` fields are the only compulsory fields, although
we highly recommend that you also have the ``name`` field specified for troubleshooting purposes.

The following is a cli configuration does the exact thing as the first JSON file configuration we had above:

.. code-block:: bash

    ./target/debug/failover cli-mode --preempt-mode --name VR_1 --vrid 51 --interface-name wlo1 --ip-address 192.168.100.100/24 --priority 101 --advert-interval 1


There is more to come, but for now:

.. image:: https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExZWJiZHNtYWtvNG53bHYwNnR5dHN5NjdlcGtnaTJ3YmN2dXh3czdteCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/lTpme2Po0hkqI/giphy.gif
     :width: 400
     :alt: That's all folks

Feel free to `contribute <https://github.com/Paul-weqe/failover>`_ in this project's codebase and also in the `docs <https://github.com/failover-docs>`_.

