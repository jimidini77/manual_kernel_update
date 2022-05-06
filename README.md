# manual_kernel_update
Kernel update. Create custom box for Vagrant Clound. Packer.

# **Содержание ДЗ**

* Установка ПО `VirtualBox`, `Vagrant`, `Packer`, `Git`. 
* Клонирование репозитория: https://github.com/dmitry-lyutenko/manual_kernel_update
* Обновление ядра ВМ, развёрнутого из vagrant box `centos/7`. В результате версия ядра изменена с `3.10.0-1127.el7.x86_64` на `5.17.5-1.el7.elrepo.x86_64`
* Назначение в конфигурации загрузчика использования нового ядра по-умолчанию.
* Создание образа системы с помощью `packer`. Использован последний доступный релиз Centos 7. Выполнено обновление ядра системы до версии 5.x. Выполнено тестирование собранного образа. Образ выгружен в `Vagrant Cloud` (jimidini77/centos-7-5)

Все действия выполнялись  на ОС `Windows`

Версии инструментов, использовавшиеся при выполнении ДЗ:

- **VirtualBox** - 6.1.34;
- **Vagrant** - 2.2.19;
- **Packer** - 1.8.0;
- **Git** - 2.36.0

## **Issues**

`paker` объявил deprecated опции исходного json и потребовал выполнения `packer fix`

При провижининге получена ошибка в `/etc/sudoers.d/vagrant` для исправления в vagrant.ks конструкция
```
cat > /etc/sudoers.d/vagrant << EOF_sudoers_vagrant
vagrant        ALL=(ALL)       NOPASSWD: ALL
EOF_sudoers_vagrant

/bin/sed -i "s/^.*requiretty/#Defaults requiretty/" /etc/sudoers
```
изменена на 
```
echo "vagrant ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/vagrant
echo "Defaults:vagrant !requiretty" >> /etc/sudoers.d/vagrant
```

# **Результаты**

Полученные в ходе работы vagrant box и конфигурационные файлы помещены в публичные репозитории:
- **GitHub** - https://github.com/jimidini77/manual_kernel_update/
- **Vagrant Cloud** - https://app.vagrantup.com/jimidini77/boxes/centos-7-5


