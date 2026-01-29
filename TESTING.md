Testing locally with Ansible 2.x
================================

```bash
git clone git@github.com:ansistrano/deploy.git
cd test
ansible-playbook main.yml -i hosts.yml
```
You can use ``ansible-playbook main.yml -i hosts.yml 2>&1 | tee deploy.log`` if you want a log file