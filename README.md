# ansible-openvpn #

An Ansible playbook+role for installing an OpenVPN server or client on an Ubuntu 18 (cloud image)
in the scope of the www.sodalite.eu project.

## Configuration

List of defaults:

    openvpn_server_config_tpl: templates/server.conf.j2
    openvpn_client_config_tpl: templates/client.conf.j2
    openvpn_port: "1194"
    openvpn_network: "10.8.0.0"

    openvpn_ca_crt: files/ca.crt
    openvpn_server_key: files/server.key
    openvpn_server_crt: files/server.crt
    openvpn_client_key: files/client.key
    openvpn_client_crt: files/client.crt

    openvpn_routes: {}


The behaviour of the openvpn role depends on the variable `openvpn_mode` ( = `server | client`).
This variable is set in the client.yml and server.yml playbooks.

## Usage

Create the inventory. E.g.:

    all:
        hosts:

        children:
            servers:
                hosts:
                    192.168.2.55:
                        ansible_ssh_user: ubuntu
            clients:
                hosts:
                    192.168.1.239:
                        ansible_ssh_user: ubuntu


### Server

Copy CA certificate, OpenVPN server key and certificate into `/files/` as:

* `ca.crt`
* `server.key`
* `server.crt`

And then run the playbook:

    $ ansible-playbook -i hosts server.yml -e vars.yml

**NOTE**: Adding NAT is a TODO. 
**NOTE2**: `vars.yml` contains the extra configuration to setup/connect_to the SODALITE VPN server.

### Client

Copy CA certificate, OpenVPN client key and certificate into `/files/` as:

* `ca.crt`
* `client.key`
* `client.crt`

And then run the playbook:

    $ ansible-playbook -i hosts client.yml -e vars.yml

## Creation of CA and certificates

[`easy-rsa`](https://github.com/OpenVPN/easy-rsa/blob/master/README.quickstart.md) makes it very easy. Just follow the steps.

## License 

Apache License v2.0