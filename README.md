add_check_pm2_proc_monitoring
=========

自用check_pm2的nagios客户端安装脚本。由于存在sudo提权，安全性上有一定的风险，需要小心使用，保护普通账户的安全。

Requirements
------------

请使用ansible-2.2.00其他版本未进行测试。另外需要已经安装有npm和nrpe客户端。过低版本的npm会无法安装check_pm2。

Role Variables
--------------

＃npm代理源配置（国外需建议改为官方源）
npm_registry: registry.npm.taobao.org
＃pm2的运行用户，一台上只能有一个。因为本脚本会建立该用户到root主目录下的软连接。
pm2_run_username: nginx
＃nrpe的配置文件模版路径。（默认）
nrpe_files_path: templates/nrpe.d_config_check_pm2_process.j2
＃客户端的nrpe配置文件路径。（默认）
nrpe_files_dest_path: "{{'/etc/nrpe.d/check_pm2_process' if ansible_os_family == 'RedHat' else '/etc/nagios/nrpe.d/check_pm2_process'}}"
nrpe_files_dest_path_ubuntu: /etc/nagios/nrpe.d/check_pm2_process
＃sudoers配置模版路径。（默认）
nrpe_sudoers_files_path: templates/sudoers.d_config_nrpe_check_pm2_process.j2
nrpe_sudoers_files_tmp: /tmp/nrpe_check_pm2_process
＃客户端的sudoers配置文件存放路径（默认）
nrpe_sudoers_files_dest_path: /etc/sudoers.d/nrpe_check_pm2_process


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      become: yes
      become_method: sudo
      vars:
        npm_registry: registry.npm.taobao.org
        pm2_run_username: nginx
        ＃nrpe_files_path: templates/nrpe.d_config_check_pm2_process.j2
        ＃nrpe_files_dest_path: "{{'/etc/nrpe.d/check_pm2_process' if ansible_os_family == 'RedHat' else '/etc/nagios/nrpe.d/check_pm2_process'}}"
        ＃nrpe_files_dest_path_ubuntu: /etc/nagios/nrpe.d/check_pm2_process
        ＃nrpe_sudoers_files_path: templates/sudoers.d_config_nrpe_check_pm2_process.j2
        ＃nrpe_sudoers_files_tmp: /tmp/nrpe_check_pm2_process
        ＃nrpe_sudoers_files_dest_path: /etc/sudoers.d/nrpe_check_pm2_process
      roles:
         - add_check_pm2_proc_monitoring

License
-------

BSD

Author Information
------------------

Kevin Zhou