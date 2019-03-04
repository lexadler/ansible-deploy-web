# ansible-web-deploy

Ansible playbooks that allow you to deploy a simple web app with apache2 web servers and haproxy load balancer.
Based on this article: https://habr.com/ru/post/305400/

Reqired:
1) Ansible installed on the control host.
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt-get install ansible
2) Python 2.7 installed on target hosts (or you can use install-python2.yml).
3) SSH key-based authentication to the target hosts has been configured.
4) Edit hosts file to specify your web servers and load balancer hosts. Replace IP addresses and usernames with your own and/or add more hosts if necessary.

Now you can deploy your basic infrastructure with simple web app from the project folder using command:
ansible-playbook -i hosts step-02/site.yml
Use another playbook to roll back:
ansible-playbook -i hosts step-03/site.yml

You can also specify another web app by editing step-02/roles/apache/tasks/main.yml. The app repo defined with this string:
git: repo=https://github.com/leucos/ansible-tuto-demosite.git dest=/var/www/awesome-app
