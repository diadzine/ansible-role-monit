Ansible Role: Monit
===================

[![Build Status](https://travis-ci.org/diadzine/ansible-role-monit.svg?branch=master)](https://travis-ci.org/diadzine/ansible-role-monit)

An Ansible Role that installs Monit on CentOS.

Requirements
------------

None

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

    monit_poll_period: 30
    monit_poll_start_delay: 240

Monit will poll every `monit_poll_period` seconds. Defining `monit_poll_start_delay`, Monit will wait `monit_poll_start_delay` seconds before to start to poll.

    monit_log: syslog

Monit will send logs to `monit_log`.

    monit_email_enable: no

Define if Monit will send notification emails.

    monit_notify_email: "root@localhost"

Email address which Monit will send notification emails.

    monit_mailserver_host: "localhost"
    monit_mailserver_port:
    monit_mailserver_username:
    monit_mailserver_password:
    monit_mailserver_encryption:
    monit_mailserver_timeout: 60

Monit settings for mail server to use for notification emails.

    monit_eventqueue_enable: yes
    monit_eventqueue_directory: "/var/lib/monit/events"
    monit_eventqueue_slots: 100

Monit settings for event queue.

    monit_mailformat_from: "Monit <monit@{{ inventory_hostname }}>"
    monit_mailformat_subject: "monit alert -- $SERVICE $EVENT"
    monit_mailformat_message: |
      $EVENT Service $SERVICE
      Date:        $DATE
      Action:      $ACTION
      Host:        $HOST
      Description: $DESCRIPTION

      Your faithful employee,
      Monit

Notification email format (sender, subject and message).

    monit_port: 2812
    monit_address: "localhost"
    monit_allow: ["localhost"]
    monit_ssl: no
    monit_cert: "/etc/monit/monit.pem"

Monit settings for web GUI.

    monit_process_list:
      - pid: '/var/run/foo.pid'
        process: 'foo'
        timeout: 60
        start: '/etc/init.d/process start'
        stop: '/etc/init.d/process stop'
        group: 'bar'
        address: '1.2.3.4'
        port: '123'
        protocol: 'sip'
        type: 'udp'
        passive: no

Monit process list to be monitored. `pid` parameter is mandatory.

    monit_host_list:
      - host: 'foo'
        address: '1.2.3.4'
        checks:
          - port: '123'
            type: 'tcp'
          - port: '456'
            protocol: 'sip'
            type:'udp'
        ping: yes
        restarts: 5
        cycles: 5
        passive: yes

Monit host list to be monitored. `host` and `address` parameters are mandatory.

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - { role: monit }

License
-------

BSD

Author Information
------------------

This role was created in 2018 by [Aymeric Bringard](https://github.com/diadzine).
