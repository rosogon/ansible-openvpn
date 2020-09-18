# ansible-openvpn #

An Ansible playbook+role for installing an OpenVPN server on an Ubuntu 18 (cloud image)
in the scope of the www.sodalite.eu project.

## Configuration

List of variables and default values:

    openvpn_server_config_tpl: templates/server.conf.j2
    openvpn_port: "1194"
    openvpn_network: "10.8.0.0"

    openvpn_ca_crt: files/ca.crt
    openvpn_server_key: files/server.key
    openvpn_server_crt: files/server.crt

## Usage

Create the inventory. E.g.:

    all:
        hosts:
            192.168.2.2:
                ansible_ssh_user: ubuntu


Copy CA certificate, OpenVPN server key and certificate into `/files/` as:

* `ca.crt`
* `server.key`
* `server.crt`

And then run the playbook:

    $ ansible-playbook -i hosts site.yml

## Creation of CA and certificates

[`easy-rsa`](https://github.com/OpenVPN/easy-rsa/blob/master/README.quickstart.md) makes it very easy. Just follow the steps.

## License 

Apache License v2.0