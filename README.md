## 23.6 Ansible roles

## Задача 

1. Создайте Ansible-роль, устанавливающую и запускающую FTP-сервер vsftpd.

## Решение

### 0 - centos_initial

    hosts:
    [skfCentos]
    192.168.5.101 ansible_user=anton

Установил Centos 8 minimal вручную.  
Создал роль centos_initial для первоначальной настройки.

`ansible-playbook m23-6.yml -k --ask-become-pass -t ssh_key`

При первом запуске необходимо ввести пароль (и такой же для sudo).  
Благодаря тэгу `ssh_key` выполнится блок, настраивающий аутентификацию по сертификату.  
Последующие запуски этого не требуют.

`ansible-playbook m23-6.yml`

### 1 - vsftpd

Роли в текущей директории. В /etc/ansible/roles пусть будет "настоящая" с кучей параметров :)

`ansible-playbook m23-6.yml`

    PLAY [skfCentos] ********************************************************************************

    TASK [vsftpd : Install required system packages] ************************************************
    ok: [192.168.5.101]

    TASK [vsftpd : Enable vsftpd service] ***********************************************************
    changed: [192.168.5.101]

    PLAY RECAP **************************************************************************************
    192.168.5.101  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0



    anton@arazumov-5410s:~/Ansible/m23-6-roles$ ftp 192.168.5.101
    Connected to 192.168.5.101.
    220 (vsFTPd 3.0.3)
    Name (192.168.5.101:anton):
    331 Please specify the password.
    Password:
    230 Login successful.
    Remote system type is UNIX.
    Using binary mode to transfer files.
