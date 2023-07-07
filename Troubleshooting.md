# Смотрим железо в нашем распоряжении

**Общая картина**

	sudo lshw -short

**Операционная система**

	cat /proc/version

**Процессор**

	lscpu
или

	cat /proc/cpuinfo


**ОЗУ**

	top
или

	cat /proc/meminfo

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