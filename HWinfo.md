# Смотрим железо в нашем распоряжении

**Общая картина**

sudo lshw -short

**Процессор**

lscpu

**ОЗУ**

top

**Диски**

sudo fdisk -l

**Смонтированные разделы**

df -h

**Видеокарта**

lspci | grep VGA

**Звук**

lspci | grep Audio

**Сеть**

lspci | grep Ethernet

**Сетевые интерфейсы**

ip a