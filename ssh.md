## Shh access to linux server
### From your local machine
#### 1. Connect to srever:
```
sftp martin@example.com
```
martin@example.com's password:\
Connected to martin@example.com.
#### 2. Create folder in userfolder\
```
mkdir .ssh
```
#### 3. Move to folder ssh
```
cd .ssh
```
#### 4. Copy from id_rsa.pub to authorized_keys
```
put id_rsa.pub authorized_keys
```
Uploading id_rsa.pub to /C:/Users/martin/.ssh/authorized_keys\
id_rsa.pub                                   100%  401   197.5KB/s   00:00
#### 5. Close connection
```
bye 
```