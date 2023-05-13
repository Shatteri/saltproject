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

# Part 2
The ultimate goal was to display the first part of this .md file on the nginx website.
<br>To achieve this, I started off by installing markdown.

    $ sudo apt install markdown

This will help me later when converting the markdown file to HTML.
<br>Next, I cloned the git repository onto the machine.

    $ mkdir repo
    $ cd repo
    $ git clone https://github.com/Shatter/saltproject.git

Next, it was time to move this markdown file into the nginx html directory.

    $ cd saltproject
    $ sudo mv miniproject.md /var/www/html
After moving the file into the correct directory, it was time to delete the original index html page.

    $ cd /var/www/html
    $ sudo rm index.nginx-debian.html
Now that the original file was deleted, I had to change the permissions of the directory in order to create a new index html file.

    $ sudo chmod 777 /var/www/html
Now I could turn the markdown file into a HTML file using the following command:

    $ sudo markdown miniproject.md > index.nginx-debian.html
So far so good...
<br>![image](https://github.com/Shatteri/saltproject/assets/103279302/c9a4a1ec-e9e6-4faf-8dce-b9eb9fa897a0)

I then restarted the service and re-applied the salt state.

    $ sudo service nginx restart
    $ sudo salt '*' state.apply project
I was running into some issues where minion did not respond, so I restarted the salt service on both machines.
<br>Master:
    
    $ sudo service salt-master restart
Slave:
    
    $ sudo service salt-minion restart
I applied the salt state again. This time it was a success.
<br>![image](https://github.com/Shatteri/saltproject/assets/103279302/e7f9c7ed-dae9-4b6d-8f3d-df7594fd023b)

Now it was time to see whether it displayed the .md file on the hope page or not.
<br>![image](https://github.com/Shatteri/saltproject/assets/103279302/de6d2f5d-4a62-44eb-8c5c-ceef0fcfc9d3)
<br>Sure enough it did! (I am aware that I couldve checked this before also, but I wanted to keep up the tension.)

I count this as an absolute win.
