Ansible is a Configeration mamangemnet Tool 
install , unstall or update 

<img width="1066" height="554" alt="Screenshot_14-5-2026_12743_www frontlinesedutech com" src="https://github.com/user-attachments/assets/167cda18-f371-45ba-966b-4e3032fdf895" />


<img width="1079" height="577" alt="image" src="https://github.com/user-attachments/assets/9d20c57d-329a-40ca-9312-71a13a359332" />

Install ansible matser server
cmd : yum install ansible -y

We have to set password root user master & slace
     passwd root   --> to set password 
     vi /etc/ssh/sshd_config     ----> 
    line 65  1) PasswordAuthentication no  replace  PasswordAuthentication yes
    line 40   2) #PermitRootLogin prohibit-password   replace PermitRootLogin yes 
    systemctl restart sshd   for restart service
    
  password authentication update  in master & slave
 
restart sshd in master and slave
generate ssh-key-gen in master  
ssh-keygen
ll .ssh
copy gen key for every slave server
 ssh-copy-id root@172.31.21.114   (ip private address of slave server)
   we have to enter slave server password 

add inventary 
ansible default path : cd /etc/ansible/
in this path we have to add inventary 
  create a file
  vim hosts   (file should same)
      [dev]
      172.31.21.114

      [prod]
      172.31.25.23

 to check master server conencted with all slave servers or not 
 
  ansible all -m ping
  ansible dev -m ping  to check particular server ( dev is server name it what we created )
  
write play book
        1. target [dev, test, prod]
        2. tasks [install/ uninstall/ update]
        3. variable
 install = present
uninstall = absent
update = latest
start = started
stop = stopped
restart = restarted

vim myplaybok.yml      ---> filename anything fine extenstion should be .yml/.yaml  (yet another markup langage)
 ---
#target section
- hosts: dev    or test (particular server)  or all  ( install in all server )
  connection: ssh

#task section
  tasks:
  - name: i am installing git on dev env
      yum: name=git state=present
...

Its should start wit h  --- & end with ...

excute play book
ansible-playbook myplaybok.yml

will noticed git installed in dev server

Inventories 
  1) static     --> present 
  2) Dynamic    --> short & sweet




        



