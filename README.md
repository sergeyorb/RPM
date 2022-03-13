# Домашнее задание - Управление пакетами. Дистрибьюция софта
<ol>
  <li>Создать виртуальную машину</li>
  <li>Установить пакеты</li>
  <li>Исправить spec файл</li>
  <li>Сборка RPM пакета</li>
  <li></li>
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

# 4.Сборка RPM пакета
<ul>
  
</ul>  
