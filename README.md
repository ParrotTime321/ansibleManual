# ansibleManual

// ansible install ob ubuntu

=========================

python3 --version
sudo apt update
sudo apt -y install python3-pip
sudo apt -y install ansible
sudo apt update

=========================

// Переміщюємо/створюємо ssh ключ від підключених linux-сів та даємо права
cd .ssh/
sudo chmod 400 Key.pem

// Створення директорії для Ansible, там створюємо .txt file з хостами та параметри з підключенням до хостів
sudo mkdir Ansible
cd Ansible/

=========================

sudo nano Hosts.txt
    [linux_server]
    UserUbuntu1 ansible_host="ip-address"
    [windows_server]
    UserWindows1 ansible_host="ip-address"

=========================

sudo mkdir group_vars

=========================

sudo nano windows_server
    ansible_user : Administrator // Логін
    ansible_password : password // пароль
    ansible_port : 5986 // порт
    ansible_connection : winrm
    ansible_winrm_server_cert_validation : ignore

=========================

sudo nano linux_server
    ansible_user : ubuntu
    ansible_private_key_file : /home/ubuntu/.ssh/Key.pem

=========================

// Пінгування хостів
ansible -i Hosts.txt linux_server -m ping
ansible -i Hosts.txt windows_server -m win_ping
