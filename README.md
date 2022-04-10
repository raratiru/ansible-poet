Poet Template
=============

An ansible template to manage poet django projects.
"Poet" is the name of my custom django setup.

Requirements
------------


Variables
---------

In `inventory/host_vars/<hostname>/plain.yml`:
* ansible_user
* ansible_become_password = "{{ vault_ansible_become_password }}"

In `inventory/host_vars/<hostname>/vault.yml`:
* vault_ansible_become_password

In `inventory/<inventory>.yml` for each host:
* ansible_host

Sample Inventory setup results in the following:
```
$ ansible-inventory --list
{
    "_meta": {
        "hostvars": {
            "manavis": {
                "ansible_become_password": "{{ vault_ansible_become_password }}",
                "ansible_host": "127.0.0.1",
                "ansible_user": "thanos",
                "vault_ansible_become_password": "Yea."
            },
            "marulita": {
                "ansible_become_password": "{{ vault_ansible_become_password }}",
                "ansible_host": "x.x.x.x",
                "ansible_user": "stardust",
                "vault_ansible_become_password": "Oh!"
            }
        }
    },
    "all": {
        "children": [
            "cloud",
            "self",
            "ungrouped"
        ]
    },
    "cloud": {
        "hosts": [
            "manavis",
            "marulita"
        ]
    },
    "self": {
        "hosts": [
            "manavis"
        ]
    }
}
```

Dependencies
------------


License
-------

BSD-3-Clause

Setup
-------
* Create an inventory according to sample_inventory
* Rename `sample_100_self.yml` to `100_self.yml` which is ignored by git and use it at will
* `ansible-playbook -l <hostname> poet.yml --tags test`
