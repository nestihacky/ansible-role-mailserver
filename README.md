mailserver
==========

Email server for individuals and small groups. Works on RHEL/CentOS 7.

Please note that this role installs and configures postgres and mysql and
combining it with other roles that use them may not work very well.

Role Variables
--------------

See also `defaults/main.yml`.

You need to set a couple of database credentials first.

    mailserver_db_admin_username: postgres
    mailserver_db_admin_password: hunter2 #required
    mailserver_db_username: mailuser
    mailserver_db_password: hunter2 #required
    mailserver_db_database: mailserver
    mailserver_opendmarc_db_username: opendmarc
    mailserver_opendmarc_db_password: hunter2 #required
    mailserver_opendmarc_db_database: opendmarc

Server identity.

    mailserver_hostname: mail.example.org #required
    mailserver_domain: example.org # required
    mailserver_admin_email: postmaster@example.org #required

And the domains, mailboxes and aliases (all keys required).

    mailserver_domains:
      - name: example.org
        pk_id: 1
      - name: example.com
        pk_id: 2
    mailserver_users:
      - account: root
        domain: example.org
        password_hash: $6$6YpaGm0xB2/jIdyO$hd4a.fdwrdTi5m2y5hRFe8wymqoHdr.2Xiep1xSDOMhSGJ7fJU3g.r8zjC8jiGX0zQO1WQrEd81Ua7TdyoTGA1
        domain_pk_id: 1
      - account: alice
        domain: example.com
        password_hash: $6$KkGEeh3UDzRRNsl1$TNQJpvUyArYY1WVnMzI51cNpcEj61V1ycpXom/79pe6QY08eFlcdJDFj.q.D7lNpCOsFMvut85gGgSvllC0xK0
        domain_pk_id: 2
    mailserver_aliases:
      - source: info@example.com
        destination: alice@example.com
        domain_pk_id: 2

Other variables (optional):

    mailserver_friendly_networks: []
    mailserver_header_privacy: true
    mailserver_data_dir: /opt/mailserver
    mailserver_ssl_cert: /etc/pki/tls/certs/wildcard_combined.pem
    mailserver_ssl_key: /etc/pki/tls/private/wildcard_private.key
    mailserver_ssl_ca: /etc/pki/tls/certs/ca-bundle.crt

Dependencies
------------

None so far.

Example Playbook
----------------

TODO

License
-------

This role is based on the Sovereign playbooks (https://github.com/sovereign/sovereign) which are
under GPLv3 except files and templates based on third-party software which should be considered
under their respective licenses.

Author Information
------------------

* http://base48.cz
* https://github.com/nestihacky/ansible-role-mailserver

Links
-----

* https://github.com/sovereign/sovereign
* http://sealedabstract.com/code/nsa-proof-your-e-mail-in-2-hours/
* https://www.owlfish.com/thoughts/dovecot-antispam-2011-03-21.html
* https://scaron.info/blog/debian-mail-postfix-dovecot.html
* https://scaron.info/blog/debian-mail-spf-dkim.html
* https://blog.filippo.io/the-sad-state-of-smtp-encryption/
* https://www.mail-tester.com/
* https://www.port25.com/support/authentication-center/email-verification/
