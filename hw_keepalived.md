# Домашнее задание к занятию 10.1 «Keepalived/vrrp» - Семикова Т.В. FOPS-9
### Задание 1

Разверните топологию из лекции и выполните установку и настройку сервиса Keepalived. 
*В качестве решения предоставьте:*   
*- рабочую конфигурацию обеих нод, оформленную как блок кода в вашем md-файле;*   
*- скриншоты статуса сервисов, на которых видно, что одна нода перешла в MASTER, а вторая в BACKUP state.*   

### MASTER

```
vrrp_instance failover_test {
state MASTER
interface enp0s3
virtual_router_id 10
priority 110
advert_int 4
authentication {
auth_type AH
auth_pass 1111
}
unicast_peer {
192.168.0.1
}
        virtual_ipaddress {
        192.168.0.50 dev enp0s3 label enp0s3:vip
}
}
```
### BACKUP STATE
```
vrrp_instance failover_test {
state BACKUP
interface enp0s3
virtual_router_id 10
priority 110
advert_int 4
authentication {
auth_type AH
auth_pass 1111
}
unicast_peer {
192.168.0.2
}
        virtual_ipaddress {
        192.168.0.50 dev enp0s3 label enp0s3:vip
}
}
```
![alt text](https://github.com/SemikovaTV/hw_keepalived/blob/main/1.jpg)
![alt text](https://github.com/SemikovaTV/hw_keepalived/blob/main/2.jpg)

### Задание 2*

Проведите тестирование работы ноды, когда один из интерфейсов выключен. Для этого:
- добавьте ещё одну виртуальную машину и включите её в сеть;
- на машине установите Wireshark и запустите процесс прослеживания интерфейса;
- запустите процесс ping на виртуальный хост;
- выключите интерфейс на одной ноде (мастер), остановите Wireshark;
- найдите пакеты ICMP, в которых будет отображён процесс изменения MAC-адреса одной ноды на другой. 

 *В качестве решения пришлите скриншот до и после выключения интерфейса из Wireshark.*
![alt text](https://github.com/SemikovaTV/hw_keepalived/blob/main/3.jpg)
