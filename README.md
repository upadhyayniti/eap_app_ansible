## Setup Ansible

Install ansible-core if not installed already

```
dnf install ansible-core
```

Install Ansible Collections 

```
ansible-galaxy collection install -r ./requirements.yml
```

Get offline token from [automation hub](https://console.redhat.com/ansible/automation-hub/token)

Update ansible.cfg with acquired token

Create service account from [Red Hat Console](https://console.redhat.com/application-services/service-accounts)

Save ID and Secret into new files for future

## Run the playbook

Create creds.yml in local directory with information saved above after creating service account

```
---
rhn_username: <Service Account ID>  
rhn_password: <Service Account Secret>
```

Run playbook

```
ansible-playbook -e @creds.yml eap_app.yml -e eap_enable=true 

# ansible-playbook -e @creds.yml eap_app.yml -e eap_enable=true -vvv (if you need verbose output)
```

Test to confirm EAP Server is running

```
curl localhost:8080/
```

Test to confirm App is deployed

```
curl localhost:8080/helloworld/
```
