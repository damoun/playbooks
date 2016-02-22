# ansible-miid [![Travis][travis-img]][travis-url]
The ansible playbooks used on miid.fr.

## How to test

Ansible playbooks are tested on vagrant with a development inventory.
To test the playbook of a host, put the corresponding environment variable to
'1' and run vagrant as usual.

```shell
VAGRANT_DNS01=1 vagrant up
```

[travis-img]: https://travis-ci.org/Damoun/ansible-miid.svg
[travis-url]: https://travis-ci.org/Damoun/ansible-miid/
