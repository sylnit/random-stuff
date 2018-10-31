1) Create the start and stop scripts of your application.
 - Example:

  ### myapp-start.sh

  ```sh
  #!/bin/bash
  cd /home/ubuntu/myapp/
  java -jar myapp.jar --server.port=8888 &
  ```

  ### myapp-stop.sh

  ```sh
  #!/bin/bash
  sudo fuser 8888/tcp -k || true
  ```

2) Create a file named `myapp` inside /etc/init.d/

```sh
#!/bin/bash

case $1 in
    start)
        /bin/bash /home/ubuntu/scripts/myapp-start.sh
    ;;
    stop)
        /bin/bash /home/ubuntu/scripts/myapp-stop.sh  
    ;;
    restart)
        /bin/bash /home/ubuntu/scripts/myapp-stop.sh
        /bin/bash /home/ubuntu/scripts/myapp-start.sh
    ;;
esac
exit 0
```

3) Mark `myapp` as executable:

```sh
cd /etc/init.d/
sudo chmod +x myapp
```

4) Make the script start on boot:

```sh
sudo update-rc.d myapp defaults
```
