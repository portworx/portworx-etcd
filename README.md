# portworx-etcd

## Set up an etcd cluster with TLS for portworx

#### Before you begin
1. git clone https://github.com/satchpx/portworx-etcd.git
2. Create a file called `inventory`. Refer to `inventory.sample` and update it to match your environment
3. Update vars.yaml with ansible_user and ansible_password.

#### Run the install
Run the docker container that sets up, bootstraps and starts the etcd cluster with TLS
```
cd ./portworx-etcd && \
docker run -t --rm --net=host \
  -v /path/to/inventory.sample:/ansible/inventory/inventory \
  -v /path/to/vars.yml:/ansible/inventory/group_vars/all.yml \
  -e ANSIBLE_HOST_KEY_CHECKING=False \
  satchpx/px-etcd:latest
```


## Optionally, you could skip the section above and install px-etcd using ansible installed on the host directly
### Prerequisites
This playbook requires ansible 2.7
To install/ upgrade ansible, execute
```
sudo apt-get install python-pip python-dev build-essential
sudo pip install --upgrade pip
sudo pip install --upgrade ansible
```

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


Credits: https://github.com/kubernetes/contrib/tree/master/ansible
