# Домашнее задание - Управление пакетами. Дистрибьюция софта
<ol>
  <li>Создать виртуальную машину</li>
  <li>Установить дополнительные пакеты</li>
  <li></li>
  <li></li>
</ol>

# 1.Создать виртуальную машину
Для создания VM использовал Vagrantfile https://github.com/sergeyorb/RPM/blob/main/Vagrantfile%20(1)

# 2.Установил дополнительные пакеты
<ul>
<p> Установил пакеты следующей командой</p>
<p> yum install -y \redhat-lsb-core \wget \rpmdevtools \rpm-build \createrepo \yum-utils
<p> yum group install "Development Tools"
<p> yum install perl-IPC-Cmd
<p> Вывод терминала представлен в файле "Terminal.txt" https://github.com/sergeyorb/RPM/blob/main/Terminal.txt    
</ul>  
