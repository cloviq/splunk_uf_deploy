splunk_uf_deploy
=========

This role is intended to install the Splunk Universal Forwarder on Windows and Redhat hosts. It also enables boot start and points to the deployment server. The control server copies the installer files to the Splunk Forwarders. There is a download handler for Windows, but it is not used in current state. This can also remove the forwarder by setting a variable.

Requirements
------------

This requires pywinrm on the Ansible control server to interface with Windows. This leverages become, so it requires sudoer credentials for Linux.

Role Variables
--------------

Variables that should always be set:

    splunk_ds: Deployment Server Hostname or IP
    splunk_ds_port: Deployment Server Port (if not set - default 8089)
    win_splunk_user: Windows User that Splunk will run as
    win_splunk_password: Windows User Password
    splunk_admin_user: Splunk Application Admin Account (if not set - default admin)
    splunk_admin_password: Splunk Application Admin Password (if not set - default UnsecureDefault1!)
    splunk_org: This value will be prepended to the *_all_deploymentclient app

Redhat defaults:

    splunk_user: splunk
    splunk_group: splunk
    splunk_ds: deployment_server
    splunk_ds_port: deployment_server_port
    splunk_home_path: /opt/splunkforwarder
    splunk_apps_path: "{{ splunk_home_path }}/etc/apps"
    splunk_bin_path: "{{ splunk_home_path }}/bin"
    splunk_enable_boot_start: yes
    splunk_rpm: 'splunkforwarder-8.0.1-6db836e2fb9e-linux-2.6-x86_64.rpm'
    nix_uf_state: present

Windows defaults:

    win_splunk_user: domain\splunk
    win_splunk_password: UnsecureDefault1!
    win_wget: 'https://www.splunk.com/bin/splunk/DownloadActivityServlet?architecture=x86_64&platform=windows&version=8.0.1&product=universalforwarder&filename=splunkforwarder-8.0.1-6db836e2fb9e-x64-release.msi&wget=true'
    splunk_msi: 'splunkforwarder-8.0.1-6db836e2fb9e-x64-release.msi'
    win_uf_state: present
    win_splunk_home: C:\Program Files\SplunkUniversalForwarder
    win_splunk_apps_path: "{{ win_splunk_home }}\\etc\\apps"
    win_splunk_bin_path: "{{ win_splunk_home}}\\bin"

Dependencies
------------

Not Applicable

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - name: Install Splunk UF
      hosts: all
      vars:
        ansible_become_password: SuperSecurePass12!
        splunk_ds: splunkds.localdomain.org
        splunk_ds_port: 8089
        win_splunk_user: domain\splunk
        win_splunk_password: SuperSecurePass12$
        splunk_admin_user: admin
        splunk_admin_password: SuperSecurePass21!
      roles:
        - name: splunk-uf

License
-------

Not Applicable

Author Information
------------------

Written by Carlo Viqueira from Splunk Professional Services
