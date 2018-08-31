OpenStack-Ansible Searchlight
#############################

Ansible role which installs and configures OpenStack Searchlight.


Default Variables
=================

.. literalinclude:: ../../defaults/main.yml
   :language: yaml
   :start-after: under the License.

Required Variables
==================

This list is not considered exhaustive at present. See role internals for
further details.

.. code-block:: yaml

    elasticsearch_apt_java_package: "openjdk-8-jre"
    searchlight_rabbitmq_userid: searchlight
    searchlight_rabbitmq_vhost: /searchlight
    searchlight_rabbitmq_servers: "{{ rabbitmq_servers }}"
    searchlight_rabbitmq_port: "{{ rabbitmq_port }}"
    searchlight_rabbitmq_use_ssl: "{{ rabbitmq_use_ssl }}"

Example Playbook
================

..  code-block:: yaml

    - name: Installation and setup of Searchlight
      hosts: keystone_all
      user: root
      roles:
        - role: elasticsearch
        - role: "os_searchlight"
          searchlight_venv_tag: "{{ openstack_release }}"
          searchlight_venv_download_url: "{{ openstack_repo_url }}/venvs/{{ openstack_release }}/{{ ansible_distribution | lower }}/searchlight-{{ openstack_release }}-{{ ansible_architecture | lower }}.tgz"
          pip_lock_to_internal_repo: "{{ (pip_links | length) >= 1 }}"
          tags:
            - "os-searchlight"
          vars:
            elasticsearch_apt_java_package: "openjdk-8-jre"
            searchlight_rabbitmq_userid: searchlight
            searchlight_rabbitmq_vhost: /searchlight
            searchlight_rabbitmq_servers: "{{ rabbitmq_servers }}"
            searchlight_rabbitmq_port: "{{ rabbitmq_port }}"
            searchlight_rabbitmq_use_ssl: "{{ rabbitmq_use_ssl }}"

Tags
====

This role supports two tags: ``searchlight-install`` and ``searchlight-config``

The ``searchlight-install`` tag can be used to install and upgrade.

The ``searchlight-config`` tag can be used to maintain configuration of the
service.

=============================
OpenStack-Ansible Searchlight
=============================

Ansible role to install OpenStack Searchlight.

Documentation for the project can be found at:
  https://docs.openstack.org/openstack-ansible-os_searchlight/latest/

Release notes for the project can be found at:
  https://docs.openstack.org/releasenotes/openstack-ansible-os_searchlight

The project source code repository is located at:
  https://git.openstack.org/cgit/openstack/openstack-ansible-os_searchlight

The project home is at:
  https://launchpad.net/openstack-ansible

The bugs can be found at:
  https://bugs.launchpad.net/openstack-ansible
