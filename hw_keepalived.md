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
