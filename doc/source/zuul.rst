
===============
Using With Zuul
===============

gabbi-tempest is designed to work well with OpenStack `infrastructure`_.
A base zuul job, named 'gabbi-tempest', is provided. Children of this job need
to only define the path of where their gabbi YAML files are located and then
request that the job run. For example a job for nova where the YAML files live
in a directory named ``gate/gabbits`` from the root of the repository would
look like this::

    - job:
      name: nova-gabbi-tempest
      parent: gabbi-tempest
      timeout: 10800
      description: |
          Test live nova using gabbi.
      vars:
        gabbi_tempest_path: "{{ devstack_base_dir|default('/opt/stack') }}/nova/gate/gabbits"

Once that job is in place, further tests are added by adding more YAML files to
the ``gate/gabbits`` directory.

More Detail
===========

The ``gabbi-tempest`` zuul job defines a small number of required settings, but
has its parent, ``devstack-tempest``, do most of the work. The settings:

* Add ``openstack/gabbi-tempest`` to ``required-projects``, making sure the
  latest version of the plugin is available.
* Chooses the ``all`` tox environment when running tempest.
* Passes ``gabbi`` as the test regular expression.
* Sets concurrency to 1 to make sure the gabbi tests run in order (otherwise
  duplicate tests can run).
* Sets ``TEMPEST_PLUGINS``.
* Turns on Python 3..

.. _infrastructure: https://docs.openstack.org/infra/manual/zuulv3.html
