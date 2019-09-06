

## Getting Started
Login as root user for ubuntu or linux machine.

### Dependancies.


```
sudo apt-get install ssh 
sudo apt-get install sshpass
```

### Run script.

Create txt file with IP address you want as line by line.
```
#ip 1
#ip 2
#
#....any number of ip's.

```
Create new script using below code.


```
#!/bin/sh
apt-get install sshpass -y #will install sshpass for your ubuntu
while read line; do

ip="$(grep -oE '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' <<< "$line")"
ping -c1 $ip  #will ping every ip once and cehck whether they are  online
if [ $? -eq 1 ] #will cechk return value 1=offline and 0=online
then
echo "****************Host Offline*********************"
else
#ssh command
  sshpass -p "YOUR PASSWORD" ssh -o StrictHostKeyChecking=no root@$ip "your command" < /dev/null
fi

done < "your path for txt" #add path with ip address saved in txt without .txt extension
```


And run it with root privilage in terminal by following command.

```
bash -x "your script path"
```

Output will be like this.

```
+ read line
++ grep -oE '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}'
+ ip=192.168.2.95
+ ping -c1 192.168.2.95
PING 192.168.2.95 (192.168.2.95) 56(84) bytes of data.
64 bytes from 192.168.2.95: icmp_seq=1 ttl=128 time=4.10 ms

--- 192.168.2.95 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 4.107/4.107/4.107/0.000 ms
+ '[' 0 -eq 1 ']'
+ sshpass -p 'password' ssh -o StrictHostKeyChecking=no root@192.168.2.95 pwd 
/root


```





## Author

* **Neruka Lakshitha**  - [nerukaadmin](https://github.com/nerukaadmin)
