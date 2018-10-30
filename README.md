# portworx-etcd

### To install
* git clone https://github.com/satchpx/portworx-etcd.git
* Create a file called `inventory`. Refer to `inventory.sample` and update it to match your environment
* Update vars.yaml with ansible_user and ansible_password.
* Run the following
```
export ANSIBLE_HOST_KEY_CHECKING=False
cd portworx-etcd
cp inventory.sample ansible/inventory/inventory
cp vars.yml ansible/inventory/group_vars/all.yml
cd ./ansible/scripts
./deploy-etcd.sh

```

[^1]: Credits: https://github.com/kubernetes/contrib/tree/master/ansible
