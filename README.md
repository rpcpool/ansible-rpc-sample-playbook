# Sample Ansible Solana RPC playbook

This repository holds a sample deploy for a Solana RPC node.

To run these you'll need [Ansible](https://www.ansible.com/) installed, and you'll need a sufficiently speced hardware node. This is designed for Ubuntu 18.04 or 20.04. Probably works on Debian as well. 

First make sure you have installed the two required roles, for example in the `roles/` dir:

```
ansible-galaxy install --roles-path roles/ git+https://github.com/rpcpool/solana-rpc-ansible.git
ansible-galaxy install --roles-path roles/ git+https://github.com/rpcpool/solana-rpc-haproxy-ansible.git
```

Before you run the deploy, edit the `inventory` file. If you do not have `root` access on your host, you can specify a user here as well:

```
[rpc_nodes]
mainnet.rpc.example.com ansible_host=127.0.0.1 ansible_user=ubuntu solana_network=mainnet cpu_governor=bios
```

Your next step is to review the system optimisation sysctl settings. These are drawn from `solana-sys-tuner` and `tuned` settings, but should be adjusted as per your system settings. You can find them in `group_vars/rpc_nodes.yml`.

Finally you can run the deploy `ansible-playbook -i inventory playbook.yml`. This will take some time, so in the meanwhile look at the [README for solana-rpc-ansible](https://github.com/rpcpool/solana-rpc-ansible/blob/main/README.md) to learn more about what it is you are actually deploying.

