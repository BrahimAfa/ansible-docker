## install ansible
 - Ubuntu
 *use sudo if you're a non-root user*

```bash
$ apt update
$ apt install software-properties-common
$ apt-add-repository --yes --update ppa:ansible/ansible
$ apt install ansible
```

## checking is the server reachable.

in this repo, you will find a file named *ansible_hosts*.
this file contains the hosts on which you want to execute the Tasks (commands) in the YAML playbook.

the **ansible_hosts** file:

```conf
[server]
111.22.33.44  ansible_user=root
```

the **[server]** refers to a group that may contain one..many hosts
hosts can be a domain or FQDNs or just IPV4 addresses

to ensure that ansible is connected to this machine run a ping test (or ping: pong ^^);
```bash
$ ansible server -m ping -i ansible_hosts --ask-pass
```

this commands checks if this machine responds on port 22 (SSH).
the ***--ask-pass*** prompts to enter the server passwords (not recommended use ssh-keys).

the ***-m ping*** stats that ansible will use a ping module to perform this operation.

NOTE: To be able to run --ask-pass seamlessly you have to install  **sshpass**

```bash
$ apt install sshpass -y
```
if the machin is reachable you'll get a sucessful result as follows :

```
111.22.33.44 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

## run playbook

and finally, if everything is setup you can execute the playbook ***palybook.yml*** with the following command :
```bash
$ ansible-playbook playbook.yml -i ansible_hosts --limit server --ask-pass
```

the ***--limit*** used to limit where to execute this playbook in case if you have different host groups.
