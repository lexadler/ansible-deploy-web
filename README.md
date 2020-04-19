# ansible-web-deploy

Ansible playbooks that allow you to deploy a simple web app with apache2 web servers and haproxy load balancer.

## Deploy:
1) Edit hosts_template file to specify your web servers and load balancer hosts. Replace <IP address> field with your own addresses and/or add more hosts if necessary. Then run `sudo mv hosts_template hosts`.
2) There must be an user with NOPASSWD option in sudoers file on the hosts.
2) Build an lightweight Ansible docker image: `docker build -t ansible .`
3) Run provisioning tasks with command `docker run --rm --network=host -it -v $(pwd)/log:/log ansible install-site.yml -e '{"username":<username>,"userpass":<password>}'`

## Rollback:
1) Run purge tasks with command `docker run --rm --network=host -it -v $(pwd)/log:/log ansible purge-site.yml -e '{"username":<username>,"userpass":<password>}'`

*Notes*:
You can specify modified `hosts` file without rebuilding docker image by adding mount with `-v $(pwd)/hosts:/ansible/hosts` to `docker run` command.
You can also specify another web app by editing `roles/apache/tasks/install.yml`. The app repo defined with the string: `git: repo=<some repo URL> dest=/var/www/awesome-app`
