# homelab-system_setup_ansible

Homelab ansible-playbook for system setup 

Ansible role location

- [role](roles/)



## Info about roles 

[r_ipa_server](roles/r_ipa_server/)

This role setups what you need for installing freeipa.

For this role you need [ansible-freeipa](https://github.com/freeipa/ansible-freeipa)
the role have some premade ansible-playbooks and ansible task.

Also install it via ansible-galaxy
```
ansible-galaxy collection install freeipa.ansible_freeipa
```


To setup ansible.cfg  with ansible 

```
roles_path    = /home/youruser/.ansible/collections/ansible_collections/freeipa/ansible_freeipa/roles
libary        = /home/youruser/.ansible/collections/ansible_collections/freeipa/ansible_freeipa/plugins/modules/
module_utils  = /home/youruser/.ansible/collections/ansible_collections/freeipa/ansible_freeipa/plugins/module_utils
```

Or use the new default for ansible 

```
collections_paths=/home/user/collections
```

host file need to look like this if you want to user it with dns and a replica host.

```
[ipaserver]
10.1.1.26 ansible_user=root

[ipaserver:vars]
ipaadmin_password=yourpass
ipadm_password=yourpass
ipaserver_domain=test.local
ipaserver_realm=TEST.LOCAL
ipaserver_setup_dns=yes
ipaserver_auto_forwarders=yes

[ipareplicas]
10.1.1.25 ansible_user=root

[ipareplicas:vars]
ipareplica_domain=test.local
ipaadmin_principal=admin
ipaadmin_password=yourpass
ipadm_password=yourpass

```

On the ipa server host and replcia server you need to setup hostname with domainname like this. 
```
hostnamectl set-hostname yourserver.test.local
```

Then add the same on /etc/hosts with ip adress

```
yourip yourserver.test.local
```

To use the premade freeipa ansible playbooks you will find them in the [ansible-freeipa](https://github.com/freeipa/ansible-freeipa) .

```
ansible-playbook -i hosts ansible-freeipa/playbooks/install-server.yml 
ansible-playbook -i hosts ansible-freeipa/playbooks/install-replica.yml 
```

Then after setting up ipa server on your client and replica server set 
dns server as your ipa server ipaddress. 

# Thanks to 

[mariuszczyz](https://github.com/mariuszczyz)

For 

- [r_rhel_apache](role/r_rhel_apache/)
- [r_rhel_pxe](role/r_rhel_pxe/)
- [r_rhel_dhcpd](role/r_rhel_dhcpd/)
- [r_rhel_mysql](role/r_rhel_mysql/)
- [r_rhel_sshd_hardening](role/r_rhel_sshd_hardening/)



[ataha](https://github.com/ataha)

For

- [r_rhel_patching](role/r_rhel_patching/)



[aruhier](https://github.com/aruhier/ansible-role-unbound)

For

- [r_unbound](role/r_unbound/)






