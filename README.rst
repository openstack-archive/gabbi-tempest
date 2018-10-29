===============
Gabbi + Tempest
===============

Gabbi-tempest is a Tempest_ plugin_ that enables testing the APIs of running
OpenStack services, integrated with tempest but without needing to write
Python. Instead the YAML format_ provided by gabbi_ is used to write and
evaluate HTTP requests and responses.

Tests are placed in YAML files in one or more directories. Those directories
are added to a ``GABBI_TEMPEST_PATH`` environment variable. When that variable
is passed into a tempest test runner that is aware of the gabbi plugin, the
files on that path will be used to create tempests tests.

The test harness sets a series of enviornment variables that can be used in
the YAML to reach the available services. The available variables may be
extended in two ways:

* Adding them to the environment that calls tempest if the values are
  known.
* Setting them in a subclass of the plugin if the values need to
  be calculated from what tempest knows.

For each service in the service catalog there are
``<SERVICE_TYPE>_SERVICE`` and ``<SERVICE_TYPE>_BASE`` variables
(e.g., ``PLACEMENT_SERVICE`` and ``PLACEMENT_BASE``). A useful
``SERVICE_TOKEN``, ``IMAGE_REF``, ``FLAVOR_REF`` and ``FLAVOR_REF_ALT``
are also available.

Read the docs at https://gabbi-tempest.readthedocs.io/
