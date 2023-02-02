# SickOS 1.1

This is a B2R (boot-2-root) CTF with the objective to compromise the machine and gain root privileges over the system as 
it demonstrates clearly how hacking tactics may be used to infiltrate a network in a secure setting.

*Link to download VM : https://www.vulnhub.com/entry/sickos-11,132/*

**Ensure that the network adapter for both kali linux and SickOS 1.1 are set to HOST-ONLY**

Walkthrough begins....

****

1. Open terminal and scan the IP address of the attacking machine.

Command prompt: ifconfig

![image](https://user-images.githubusercontent.com/98629454/216243182-02fae104-afc3-4681-97a7-678c27d9d300.png)

2. Enter root terminal and scan for /24 range of IP address to find the IP address of SickOS 1.1.

Command prompt: sudo netdiscover -i eth0

*eth0 signifies the attacking machine. You may replace it with the machine’s IP address.

![image](https://user-images.githubusercontent.com/98629454/216243511-41d9eaba-7449-4bd7-b22b-947f55f4334f.png)

3. Port scanning the IP address of SickOS to find open port and the service running on the port.

Command prompt: sudo nmap -sC –sV <IP address of SickOS>

![image](https://user-images.githubusercontent.com/98629454/216243521-10beec21-784b-4e39-8722-4cc2301280b2.png)
  
4. Create the proxy with SickOS IP address with the port found

Ensure that proxy is not set to local host.

 ![image](https://user-images.githubusercontent.com/98629454/216243721-248bfc13-02a8-4c03-86a2-8bc84d9c4361.png)

5. Look up for the IP address via browser. Since the web page is suspicious, try adding /robots.txt at the behind the IP address in search bar.

 ![image](https://user-images.githubusercontent.com/98629454/216243808-06993f09-4e5a-4d51-9d88-bc3d50f39858.png)
  
6. Replace /robots.txt with /wolfcms. You will be redirected to a Wolf CMS site.

![image](https://user-images.githubusercontent.com/98629454/216243831-7ee7464b-2126-4890-85ee-f6bbc96300cf.png)
  
7. Try getting to the login page by adding ?/admin/login in the search bar. Login with username and password ‘admin’. 

  ![image](https://user-images.githubusercontent.com/98629454/216243837-182e8992-55ed-4783-beda-76b74ce764e5.png)

  
  ![image](https://user-images.githubusercontent.com/98629454/216243847-2cc04a87-d535-4aa1-abe0-39f0dc55876b.png)
  
  8. Go to the browser on your host, search for https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php .  Copy the coding.

  ![image](https://user-images.githubusercontent.com/98629454/216243857-c3c7bfde-5488-495b-876b-16a2165cb250.png)
  
  9. Create a document and paste the coding into the document. Ensure the coding is saved into .php format. Change the IP address with the attacking device’s and set the port.

* Port used will be the listening port
* You can save the file into a folder.

![image](https://user-images.githubusercontent.com/98629454/216243878-127baa18-0728-466f-957b-022ea550a1ca.png)
  
  
  ![image](https://user-images.githubusercontent.com/98629454/216243893-7d638c44-a711-42dd-93fe-a5e03ff94a1a.png)
  
  
  10. Upload the .php file in the file section of the website.

  ![image](https://user-images.githubusercontent.com/98629454/216243910-415f76db-c328-4050-ad75-37cff50e8563.png)

  11. Change the directory to
 <SickOS IP address>/wolfcms/public 

   ![image](https://user-images.githubusercontent.com/98629454/216243916-4c098ebc-4c2d-4b93-9bd1-9b70a243ab56.png)

   12. Open root terminal and start listening to the port (as per entered in the .php file uploaded) and click on the .php file on the index directory.

Command prompt for port listening:
nc –nlvp 4444 -vvv

   
![image](https://user-images.githubusercontent.com/98629454/216243941-105b1f14-0600-4ad8-9571-d204672f4808.png)
   
   
![image](https://user-images.githubusercontent.com/98629454/216243930-bc3e8b52-d034-4101-b8d7-1994e7a0c5e8.png)

13. List the files in wolfcms

Command prompt: 
ls /var/www/wolfcms

   ![image](https://user-images.githubusercontent.com/98629454/216243957-205d6a48-41f4-4cda-a2bb-ac5728f43ec2.png)

14. Check the content of config.php to obtain the username and password of SickOS.

Command prompt:
cat /var/www/wolfcms/config.php
   
![image](https://user-images.githubusercontent.com/98629454/216243964-cd06091b-8f9f-4eee-a1b5-f4a23561b7b8.png)

15. Enter root terminal and try to enter SickOS via  ssh

Command prompt:
ssh sickos@<sickOS IP address>

![image](https://user-images.githubusercontent.com/98629454/216243996-9291a0a3-ab8d-499d-b2c5-eb413833584c.png)
   
16. Get into the root of SickOS, go to the directory and list out possible available file.

Command prompt:
sudo su root
cd ~
ls

![image](https://user-images.githubusercontent.com/98629454/216244011-59b6c8f0-8746-4118-aa73-de2d1ad8bdc6.png)
   
17. Check the content of the .txt file displayed

Command prompt:
cat <file.txt>
   
![image](https://user-images.githubusercontent.com/98629454/216244021-f92910c8-bef3-46e8-af00-85eb9fad233c.png)
