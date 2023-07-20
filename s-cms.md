1.Start by downloading cms, the official open source app
![1678955853200](https://user-images.githubusercontent.com/113097106/225561589-5871b982-40e3-407d-8325-0adc3353b21d.jpg)
2.Use a code audit tool to find vulnerabilities，The vulnerability path is:\WWW\admin\data.php   Line 2904
![image](https://user-images.githubusercontent.com/113097106/225562709-589ba9c4-d510-4b41-bace-b11f5954c1c6.png)
3.Find the code path to debug,First log in the background
![image](https://user-images.githubusercontent.com/113097106/225563643-2d5d0a8b-85b8-4394-b97e-44d7f6dba795.png)
4.Request through parameter combination, and open the debug tool for breakpoints,Enter the readtxt parameter.Read the database configuration file conn.php
![image](https://user-images.githubusercontent.com/113097106/225564355-26f8b151-6695-4621-98e4-807bce2f32bd.png)
![image](https://user-images.githubusercontent.com/113097106/225564648-b1d3378d-f8a1-4c18-9697-2dbc08e895b8.png)
5.It can be found that $C_dirx is the root directory of the website. Firstly, GET filter./, because there is no./, and then continue filtering., through the $C_dirx root directory and request data concatenation, finally can read any file.
![image](https://user-images.githubusercontent.com/113097106/225565911-af094bc1-79cf-4749-a193-e3aa682df6f0.png)
![image](https://user-images.githubusercontent.com/113097106/225566069-b885a769-fb20-4766-8b9f-e9d5139bef4f.png)
6.The returned value is the database configuration file information. Similarly, any file in the www directory can be read
![image](https://user-images.githubusercontent.com/113097106/225566825-9829ce42-c056-4d5b-9391-2f6a7f9aa03f.png)
7.You only need to control the folder and file parameters
![image](https://user-images.githubusercontent.com/113097106/225567129-8b2465a2-c0d8-4831-afaa-692f2b2cbc3d.png)
8.Packet request and return under burp
![image](https://user-images.githubusercontent.com/113097106/225567724-a69a5ec0-20a3-4d5d-9de3-191eff0b6688.png)
![image](https://user-images.githubusercontent.com/113097106/225567770-ed70c66a-5260-4af7-8c72-2bdea02f9d35.png)
9.Backup database file read
![image](https://user-images.githubusercontent.com/113097106/225568168-9fec4a13-1b8b-46f6-885d-c17efdfa5a6e.png)
