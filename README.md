Nginx for Cloudera Hadoop services
=========

Dependencies:
--------------

* Docker 1.13+
* Ansible 2.4+

Dependencies for local run:

* Vagrant 1.9.1+
* Oracle VirtaulBox 5.1.30+

Run local in Vagrant:
--------------

```
vagrant up --no-provision
vagrant provision
```

Test local:
```
vagrant ssh
curl http://localhost
```
