# Ansible Role: ansible-ipaclient

## Description

Configure host as an IPA client. Can also request and install SSL certificates from IPA

## Requirements

- Ansible >= 2.9 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `ipaclient_servers` | [ipa1.example.com] | List of IPA Servers |
| `ipaclient_domain` | ipa.example.com | IPA Realm |
| `ipaclient_enroll_user` | admin | User authorised to enrol hosts and request certs |
| `ipaclient_enroll_pass` | ChangeMe | Password for above user |
| `ipaclient_force_join` | false | Force host enrolment regardles of current state |
| `ipaclient_enable_ntp` | true | Configure IPA servers as the NTP source |
| `ipaclient_all_ip_addresses` | false | Add all IP Addresses to DNS (False adds only the primary IP) |
| `ipaclient_ip_address` | false| Update DNS with our primary IP address |
| `ipaclient_enable_dns_updates` | true| Configure sssd to update DNS when our IP changes |
| `ipaclient_mkhomedir` | true| Auto-create user home directories with oddjob on first login |
| `ipaclient_ssl_create_certs` | false| Request SSL certificate for this host |
| `ipaclient_ssl_keylen` | 4096 | SSL Key length |
| `ipaclient_ssl_key_mode` | '0600' | Permission of retrieved SSL key file |
| `ipaclient_ssl_subject_altnames` | [] | List of Subject AltNames (SAN) to include in the certificate |
| `ipaclient_krb5_dns_lookup_realm` | true | Use DNS to find the KRB5 realm |
| `ipaclient_krb5_dns_lookup_kdc` | true | Use DNS to find the KDC |
| `ipaclient_krb5_dns_canonicalize_hostname` | false |  |
| `ipaclient_krb5_extra_domains` | [] | List of additional KRB5 domains to lookup via IPA |
| `ipaclient_sssd_shortnames` | false | Force short hostname display - useful in an AD trust environment |


## Example

### Playbook

Use it in a playbook as follows:
```yaml
- hosts: all
  roles:
    - ansible-ipaclient
  vars:
    ipaclient_servers:
    - auth1.ipa.example.com
    - auth2.ipa.example.com
    ipaclient_domain: ipa.example.com
    ipaclient_enroll_user: svc-ipajoin
    ipaclient_enroll_pass: "{{ vault_idm_admin_pass }}"
```
