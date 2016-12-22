freeradius-deb
==============

An ansible role to build DEB packages for the FreeRadius radius server.

Tested versions:

3.0.8
3.0.9
3.0.10
3.0.11
3.0.12

Requirements
------------

Ansible 2+

Role Variables
--------------

'defaults/main.yml' sets default variables 'version' and 'shared_folder'. The default version is '3.0.12'

Example Playbook
----------------

    - hosts: all
      become: true
      roles:
         - { role: freeradius-build-deb, version: "3.0.12", shared_folder: '/usr/local/src' }

How to build
------------

Use Vagrant or Docker to run the ansible role and build the deb packages. CD into the root directory. Both options will result in the FreeRadius DEB packages being copied into the local 'debs' folder.

Vagrant:

```
vagrant up
```

Docker:

Two environment variables can be set when running the playbook in this way.
'version' specifies which version of FreeRadius to download and build.
'shared_folder' specifies where the .deb files will be copied to.

```
docker run -i --rm \
-v=$(pwd):/etc/ansible/roles/:ro \
-v=$(pwd)/debs:/usr/local/src/:rw \
--privileged \
geerlingguy/docker-ubuntu1604-ansible:latest \
ansible-playbook \
-e version="3.0.12"  
-e shared_folder="/usr/local/src" \
/etc/ansible/roles/deb_builder.yml
```
