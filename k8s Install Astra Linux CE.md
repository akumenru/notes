Kubernetes k8s в Astra Linux CE (Орел 2.12)
---
<b>#Ставим Docker</b>

sudo apt install docker-compose -y

#Проверяем его работоспособность

sudo docker run hello-world

#Удовлетворим отсутствующие зависимости репозиторием Debian Buster'а
---
echo "deb http://ftp.ru.debian.org/debian/ buster main non-free" | sudo tee /etc/apt/sources.list.d/debianbuster.list

gpg --keyserver keyserver.ubuntu.com --recv-key 648ACFD622F3D138

gpg -a --export 648ACFD622F3D138 | sudo apt-key add -

gpg --keyserver keyserver.ubuntu.com --recv-key 0E98404D386FA1D9

gpg -a --export 0E98404D386FA1D9 | sudo apt-key add -

gpg --keyserver keyserver.ubuntu.com --recv-key DCC9EFBF77E11517

gpg -a --export DCC9EFBF77E11517 | sudo apt-key add -

sudo apt-get update


#Ставим репозиторий Kubernetes k8s
---
sudo apt-get install -y apt-transport-https ca-certificates curl

curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /etc/apt/kubernetes-archive-keyring.gpg

echo "deb [signed-by=/etc/apt/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update


<b>#Качаем три основных инструмента для работы с кубером и отключаем им обновление версий</b>
sudo apt-get install -y kubelet kubeadm kubectl

sudo apt-mark hold kubelet kubeadm kubectl


[**Источник**](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

[**Шпаргалка по KubeCTL**](https://kubernetes.io/ru/docs/reference/kubectl/cheatsheet/)

