# Shardeum Скрипт

# Скрипт для перезапуску зупиненої ноди без встановлення бота 

### Скрипти, бот і техпідтримка Shardeum у групі https://t.me/shardeumrus

### 1.виконати в консолі
```
docker exec -it shardeum-dashboard /bin/bash
```

### 2.ввести в консоль

```
sudo tee restart.sh > /dev/null <<EOF
#!/bin/sh

check_status() {
 while :
 do 
     if operator-cli status | grep "stopped"; then
         echo "---Trying to restart---"
         operator-cli start
     elif operator-cli status | grep "standby"; then
         echo "Waiting for active status"
     fi
 sleep 30
 done
}

main() {
  echo "start main"
  check_status
}
main
EOF
```

### 3. sudo chmod +x restart.sh
### 4. ./restart.sh &

Закрити консоль, зупинити ноду і перевірити що через 30 сек вона знову запустилася

### Якщо з якоїсь причини зупиниться сам контейнер, то щоб запустити скрипт заново, потрібно зробити
```
docker start shardeum-dashboard
```

### а потім пункти 1, 2, 5
