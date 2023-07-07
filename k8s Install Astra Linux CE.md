# Kubernetes k8s в Astra Linux CE (Орел 2.12)

Прежде чем начинать, убедимся что установлены инструменты для работы с внешними репозиториями

	sudo apt install -y apt-transport-https ca-certificates curl gnupg2 software-properties-common

**Ставим Docker**

	sudo apt install docker-compose -y
	
а лучше подключим репозиторий докера и поставим последнюю актуальную версию

	curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
	
	sudo printf "deb [arch=amd64] https://download.docker.com/linux/debian stretch stable \n" > /etc/apt/sources.list.d/docker.list
	
	sudo apt-get update
	
	sudo apt-get install docker-ce docker-ce-cli containerd.io

**Проверяем его работоспособность**

	sudo docker run hello-world

**Ставим репозиторий Kubernetes k8s**

	curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /etc/apt/kubernetes-archive-keyring.gpg

	echo "deb [signed-by=/etc/apt/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

	sudo apt-get update

**Качаем три основных инструмента для работы с кубером**

	sudo apt-get install -y kubelet kubeadm kubectl
	
получаем ошибку о неразрешимой зависимости conntrack

**Удовлетворим отсутствующие зависимости репозиторием Debian Buster'а**

	echo "deb http://ftp.ru.debian.org/debian/ buster main non-free" | sudo tee /etc/apt/sources.list.d/debianbuster.list
	
	gpg --keyserver keyserver.ubuntu.com --recv-key 648ACFD622F3D138
	
	gpg -a --export 648ACFD622F3D138 | sudo apt-key add -
	
	gpg --keyserver keyserver.ubuntu.com --recv-key 0E98404D386FA1D9
	
	gpg -a --export 0E98404D386FA1D9 | sudo apt-key add -
	
	gpg --keyserver keyserver.ubuntu.com --recv-key DCC9EFBF77E11517
	
	gpg -a --export DCC9EFBF77E11517 | sudo apt-key add -
	
	sudo apt-get update
	
пробуем еще раз, и все получается

	sudo apt-get install -y kubelet kubeadm kubectl
	
**и отключаем им обновление версий**
	
	sudo apt-mark hold kubelet kubeadm kubectl
	
[**Источник**](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

Запускаем мастерноду кластера

	sudo kubeadm init

и узнаем что у нас не запущена служба containerd

проверяем эту службу

	sudo systemctl status containerd
	
и убеждаемся что она запущена и работает. смотрим где лежит файл конфига

	sudo containerd config default

отключаем там плагин cri



[**Шпаргалка по KubeCTL**](https://kubernetes.io/ru/docs/reference/kubectl/cheatsheet/)