# portworx-etcd

## Set up an etcd cluster with TLS for portworx

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

## Optionally, you could skip the section above and install px-etcd using the docker container
#### Before you begin
```
git clone https://github.com/satchpx/portworx-etcd.git
Create a file called `inventory`. Refer to `inventory.sample` and update it to match your environment
Update vars.yaml with ansible_user and ansible_password.
```

#### Run the install
Run the docker container that sets up, bootstraps and starts the etcd cluster with TLS
```
cd ./portworx-etcd && \
docker run --rm \
  -v ./inventory.sample:/ansible/inventory/inventory \
  -v ./vars.yml:/ansible/inventory/group_vars/all.yml \
  -e ANSIBLE_HOST_KEY_CHECKING=False \
  satchpx/px-etcd:latest
```


Credits: https://github.com/kubernetes/contrib/tree/master/ansible
