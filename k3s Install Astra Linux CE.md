Kubernetes k3s в Astra Linux CE (Орел 2.12)
---

#Устанавливаем k3s
---------------
curl -sfL https://get.k3s.io | sh -

#Проверяем работоспособность
------------
sudo k3s kubectl get node

#Файл конфигурации кластера находится тут
----------------------------------------
/etc/rancher/k3s/k3s.yaml

#Посмотреть его можно командой
-----------------------------
kubectl config view

#Ручной запуск кластера
-----------------------
sudo k3s server

#Проверка статуса поднятых служб
---
kubectl get po -n kube-system

#Применение конфигурации из файла
---------------------------------
sudo kubectl apply -f ./filename.yaml

#Проверка статуса запущенных подов
----------------------------------
sudo kubectl get pods

#Удаление запущенного пода
--------------------------
sudo kubectl delete -f ./filename.yaml

#Запуск команды внутри запущенного пода
---------------------------------------
sudo kubectl exec full-pod-name -- command /

#Просмотр логов внутри пода - весь stdout
-----------------------------------------
sudo kubectl logs full-pod-name

#Проброс порта с локалхоста в под
---------------------------------
sudo kubectl port-forward full-pod-name portIn:portDst # (21:21)