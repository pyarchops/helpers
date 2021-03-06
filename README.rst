=====================
pyArchOps/helpers
=====================


.. image:: https://badge.fury.io/py/pyarchops-helpers.svg
        :target: https://pypi.python.org/pypi/pyarchops-helpers

.. image:: https://img.shields.io/gitlab/pipeline/pyarchops/helpers/next-release.svg
        :target: https://gitlab.com/pyarchops/helpers/pipelines

.. image:: https://readthedocs.org/projects/pyarchops-helpers/badge/?version=latest
        :target: https://pyarchops-helpers.readthedocs.io/en/latest/?badge=latest
        :alt: Documentation Status

.. image:: https://pyup.io/repos/github/pyarchops/helpers/shield.svg
     :target: https://pyup.io/repos/github/pyarchops/helpers/
          :alt: Updates


Helpers for pyArchOps


* Free software: MIT license
* Documentation: https://pyarchops-helpers.readthedocs.io.


Features
--------

* docker based test helpers


Instalation
--------------

.. code-block:: console

    $ pip install pyarchops-helpers


Usage
--------

.. code-block:: python

    from suitable import Api
    from pyarchops_helpers import helpers

    with helpers.ephemeral_docker_container(
            image='registry.gitlab.com/pyarchops/pyarchops-base'
    ) as container:
        connection_string = "{}:{}".format(
            container['ip'], container['port']
        )
        print('connection strings is ' + connection_string)
        api = Api(connection_string,
                  connection='smart',
                  remote_user=container['user'],
                  private_key_file=container['pkey'],
                  become=True,
                  become_user='root',
                  sudo=True,
                  ssh_extra_args='-o StrictHostKeyChecking=no')

        try:
            result = api.setup()['contacted'][connection_string]
        except Exception as error:
            raise error

        assert result['ansible_facts']


Development
-----------

Install requirements:

.. code-block:: console

    $ sudo pacman -S tmux python-virtualenv python-pip libjpeg-turbo gcc make vim git tk tcl

Git clone this repository

.. code-block:: console

    $ git clone https://github.com/pyarchops/helpers.git pyarchops.helpers
    $ cd pyarchops.helpers


2. See the `Makefile`, to get started simply execute:

.. code-block:: console

    $ make up


Credits
-------

* TODO

