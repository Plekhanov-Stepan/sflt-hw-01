# Домашнее задание к занятию 1 «Disaster recovery и Keepalived» - Плеханов Степан
## Задание 1

<img src = "img/Screenshot_1_1.png" width=100%>
<img src = "img/Screenshot_1_2.png" width=100%>
<img src = "img/Screenshot_1_3.png" width=100%>

## Задание 2

````bash
global_defs {
    enable_script_security
}

vrrp_script nginx_check {
    script /etc/keepalived/nginx_check.sh
    interval 3
    user plekhas
}

vrrp_instance VI_1 {
        state MASTER
        interface enp0s8
        virtual_router_id 200
        priority 255
        advert_int 1

        virtual_ipaddress {
              192.168.0.200/24
        }
        track_script {
              nginx_check
        }

}
````

````bash
#!/bin/bash
if [ ! -e /var/www/html/index.html ]
then
        exit 1
fi

curl -Is http://localhost
````

<img src = "img/Screenshot_2_1.png" width=100%>
<img src = "img/Screenshot_2_2.png" width=100%>
<img src = "img/Screenshot_2_3.png" width=100%>
<img src = "img/Screenshot_2_4.png" width=100%>
<img src = "img/Screenshot_2_5.png" width=100%>
<img src = "img/Screenshot_2_6.png" width=100%>

