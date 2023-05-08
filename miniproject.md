# Miniproject
The goal is to create a salt state which installs a nginx web-server to the minion.

>The following exercise was done on 2 Virtual machines (Ubuntu server 22.04.2).
The machines are called "saltmachine" (master) and "saltmachine2" (slave).

## Installing nginx
I started off by creating a new directory containing an init.sls file under /srv/salt path.

    $ cd /srv/salt
    $ sudo mkdir project
    $ cd project/
    $ sudo nano init.sls
I gave the .sls file the following contents:
<br>![image](https://user-images.githubusercontent.com/103279302/236855081-a39dca6a-51ae-4c97-b0fe-029c674207c2.png)
<br>After saving the file, it was time to apply the salt state.

    $ sudo salt '*' state.apply project
![image](https://user-images.githubusercontent.com/103279302/236849062-8a61ec5a-d6ea-4fae-9e5c-bbf4f27af4d7.png)
<br>I then checked whether the service was up and running.

    $ service nginx status
![image](https://user-images.githubusercontent.com/103279302/236849819-85fe0364-fd09-4b60-b59b-dfc301019966.png)
<br>I decided to double check through my browser, so I typed the IP-address of the slave into the search bar:

    $ ip address
![image](https://user-images.githubusercontent.com/103279302/236853385-ea265326-cc4b-47f7-b9ef-52f518dcef5c.png)
<br>![image](https://user-images.githubusercontent.com/103279302/236853174-9240fe22-28ac-435a-94a7-809bcc37ec54.png)

It turned out to be a success.
