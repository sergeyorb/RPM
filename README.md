# Домашнее задание - Управление пакетами. Дистрибьюция софта
<ol>
  <li>Создать виртуальную машину</li>
  <li>Установить пакеты</li>
  <li>Исправить spec файл</li>
  <li>RPM пакет</li>
  <li>Установка созданного RPM пакета</li>
  <li>Создание репозитория</li>
  <li>Тестирование репозитория</li>
</ol>

# 1.Создать виртуальную машину
Для создания VM использовал Vagrantfile https://github.com/sergeyorb/RPM/blob/main/Vagrantfile%20(1)

# 2.Установить пакеты
<ul>
<li>Установил дополнительные пакеты</li>
  <p> Установил пакеты следующей командой</p>
  <p> yum install -y \redhat-lsb-core \wget \rpmdevtools \rpm-build \createrepo \yum-utils
  <p> yum group install "Development Tools"
  <p> yum install perl-IPC-Cmd
  <p> Вывод терминала представлен в файле "Terminal.txt" https://github.com/sergeyorb/RPM/blob/main/Terminal.txt    
  
<li>Загрузить пакет nginx</li>
  <p> Пакет загрузил командой</p>
  <p> wget https://nginx.org/packages/centos/7/SRPMS/nginx-1.14.1-1.el7_4.ngx.src.rpm
  <p> rpm -i nginx-1.14.1-1.el7_4.ngx.src.rpm
  
<li>Скачал и зазорхивировал исходник для openssl</li>
  <p> wget https://www.openssl.org/source/openssl-1.1.1m.tar.gz</p>  
  <p> tar -xvf openssl-1.1.1m.tar.gz
<li> Поставил все зависимости</li>
  <p> yum-builddep rpmbuild/SPECS/nginx.spec</p>  
</ul> 

# 3.Исправить spec файл
<ul>
  <p> Файл скопировал от сюда https://gist.github.com/lalbrekht/6c4a989758fccf903729fc55531d3a50
  <p> Проверил что бы путь до openssl был --with-openssl=/root/openssl-1.1.1a  
</ul>

# 4.RPM пакет
<ul>
<li>Сборка RPM пакета</li>
 <p> Собрал RPM пакет командой</p> 
 <p> rpmbuild -bb rpmbuild/SPECS/nginx.spec
 <p> Вывод терминала представлен в файле "Terminal.txt" https://github.com/sergeyorb/RPM/blob/main/Terminal.txt  
<li>Проверил что пакеты созданы</li>
 <p> ll rpmbuild/RPMS/x86_64/ 
</ul>  

# 5.Установка созданного RPM пакета
<ul>
<li>Установил пает командой</li>
  <p> yum localinstall -y \rpmbuild/RPMS/x86_64/nginx-1.14.1-1.el7_4.ngx.x86_64.rpm   
<li>Ставтовал nginx командой</li>
  <p> systemctl start nginx   
<li>Проверил работу nginx командой</li> 
  <p> systemctl status nginx
  <p> Вывод терминала представлен в файле "Terminal.txt" https://github.com/sergeyorb/RPM/blob/main/Terminal.txt 
</ul>

# 6.Создание репозитория
<ul>
<li>Создал каталог repo в директории /usr/share/nginx/html.</li>
  <p> mkdir /usr/share/nginx/html/repo  
<li>Скопировал туда созданный RPM пакет и RPM пакет из https://repo.percona.com/yum/release/7/RPMS/noarch/percona-release-1.0-22.noarch.rpm</li>
  <p> cp /root/rpmbuild/RPMS/x86_64/nginx-1.14.1-1.el7_4.ngx.x86_64.rpm /usr/share/nginx/html/repo/
  <p> wget https://repo.percona.com/yum/release/7/RPMS/noarch/percona-release-1.0-22.noarch.rpm -O /usr/share/nginx/html/repo/percona-release-0.1-6.noarch.rpm  
<li>Инициализировал репозиторий</li>
  <p> createrepo /usr/share/nginx/html/repo/  
<li>Отредактировал default.conf в директории /etc/nginx/conf.d/</li>
  <p> Добавил autoindex on;  
<li>Проверил синтаксис nginx</li>
  <p> nginx -t
<li>Перезапустил nginx</li>
  <p> nginx -s reload
<li>Проверил работу репозитория</li>
  <p> lynx http://localhost/repo/
</ul>

# 7.Тестирование репозитория
<ul>
<li>Добавил репозиторий в /etc/yum.repos.d</li>
  <p> cat >> /etc/yum.repos.d/otus.repo << EOF 
  <p> [otus]
  <p> name=otus-linux
  <p> baseurl=http://localhost/repo
  <p> gpgcheck=0
  <p> enabled=1
  <p> EOF 
<li>Убедился что репозиторий подключился</li>
  <p> yum repolist enabled | grep otus 
  <p> yum list | grep otus   
</ul>  
