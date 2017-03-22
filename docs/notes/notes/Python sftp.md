# 使用Python实现无交互sftp上传、下载

----------

## 安装Paramiko

Python的Paramiko库实现了ssh和sftp协议，如果没有安装的Python中没有可以通过 `pip install paramiko` 安装一下。


## 实现
### 首先引入各种库
os来遍历文件夹，platform来判断操作系统，sys取传入的参数，paramiko来实现sftp的各种操作。

```
# coding=utf-8
import os  
import paramiko  
import platform
import sys
```

### 文件、目录上传
代码
```python
def upload(ip, port, username, password, local, remote):  
        #上传目录 or 文件
        paramiko.util.log_to_file("paramiko.log")  
        trans = paramiko.Transport((ip, int(port)))  
        trans.connect(username=username, password=password)  
        sftp = paramiko.SFTPClient.from_transport(trans)   
        try:  
                sftp.mkdir(remote)  
        except Exception, e:  
                print e,'mkdir',remote , 'fail, dir is exists'
        try:
                if os.path.isdir(local):#判断本地参数是目录还是文件
                        print 'upload dir'
                        for root, dirs, files in os.walk(local):  #遍历本地目录
                                for file_name in files:  
                                        local_file_path = os.path.join(root, file_name)
                                        # 切片：windows路径去掉盘符  
                                        if(platform.system() == 'Windows'):
                                                remote_file_path = os.path.join(  
                                            remote_dir, local_file_path[3:])      
                                        else:
                                                remote_file_path = os.path.join(  
                                            remote_dir, local_file_path)    
                                        remote_file_path = remote_file_path.replace("\\", "/")  
                                        
                                        try:  
                                                sftp.put(local_file_path, remote_file_path)  
                                        except Exception, e:  
                                                print e,'put',local_file_path,'to'
                                                        ,remote_file_path,'fail'
                                                sftp.mkdir(os.path.dirname(remote_file_path))  
                                                sftp.put(local_file_path, remote_file_path)  
                                for dir_name in dirs:  
                                        local_dir = os.path.join(root, dir_name)
                                        # 切片：windows路径去掉盘符
                                        if(platform.system() == 'Windows'):
                                                remote_path = os.path.join(remote, local_dir[3:])  
                                        else:
                                                remote_path = os.path.join(remote, local_dir) 
                                        remote_path = remote_path.replace("\\", "/")  
                                        
                                        try:  
                                                sftp.mkdir(os.path.dirname(remote_path))  
                                                sftp.mkdir(remote_path)  
                                        except Exception, e:  
                                                print e,'mkdir',remote_path,'on remote fail'  
                else:
                        print 'upload file'
                        try:
                                remote_dir,remote_filename  =  os.path.split(remote)
                                local_dir,local_filename = os.path.split(local)
                                # remote中没有目标文件名,使用local_filename
                                if remote_filename == ''  or remote_filename == '.': 
                                        remote_filename = local_filename
                                # remote 中没有目标目录,使用默认目录
                                if remote_dir == '': 
                                        remote_dir = '.'
                                try:
                                        sftp.chdir(remote_dir) # 切换到目标目录
                                        sftp.put(local,remote_filename) 
                                except Exception, e:  
                                        print e,remote_dir,'is not exists'              
                        except Exception, e:  
                                print e,'put',local,'to',remote,'fail'  
                trans.close()
        except Exception, e:  
                print e   
                trans.close()
```

### 文件、目录下载
```python
def download(host,port,username,password,remote,local):
        # 下载文件 or 目录
        paramiko.util.log_to_file("paramiko.log")  
        sf = paramiko.Transport((host,port))
        sf.connect(username = username,password = password)
        sftp = paramiko.SFTPClient.from_transport(sf)
        print local,remote   
        def getall(remote,local):
                print 'prarms',remote,local
                if stat.S_ISREG(sftp.stat(remote).st_mode):
                        print remote,'is file,get to',os.path.join(local,remote)
                        sftp.get(remote,os.path.join(local,remote))
                        return
                else:
                        print remote,'is dir,mkdir at',os.path.join(local,remote)
                        os.mkdir(os.path.join(local,remote))
                        for f in sftp.listdir_attr(remote):
                                getall(os.path.join(remote,f.filename),local) 
                                                
        try:
                #1.local is file or dir, remote is file
                if stat.S_ISREG(sftp.stat(remote).st_mode): # remote is file
                        local_dir,local_filename = os.path.split(local) 
                        print local_dir,local_filename 
                        remote_dir,remote_filename = os.path.split(remote)
                        print remote_dir,remote_filename
                        # 如果没有输入文件名使用remote的文件名  
                        if local_filename == '' and local_filename != '.': 
                                print 'without a filename'                      
                                sftp.get(remote,os.path.join(local,remote_filename))
                        else:
                                print 'have a filename'
                                sftp.get(remote,local)
                else: #remote is dir
                        getall(remote,local)            
                trans.close()
        except Exception, e:
                print e
                trans.close()
```
### 例子
1. 下载目录testdir1到testdir2下
```python
download('ip', 'port', 'username', 'password', 'testdir1', 'testdir2')
```
2. 下载文件testfile1到当前目录
```python
download('ip', 'port', 'username', 'password', 'testdir6/testfile1', '')
```
3. 上传文件到默认目录
```python
upload('ip', 'port', 'username', 'password', 'file1', '.')
```
4. 上传目录到指定目录
```python
upload('ip', 'port', 'username', 'password', 'testdir1', 'testdir2')
```

### 打包成命令
 保存到`sftp.py`在，然后在shell脚本中通过  `python sftp.py get username/password@ip:port remote local`、
`python sftp.py put username/password@ip:port loacl remote` 就可以无交互上传、下载了。
```python
if __name__ == '__main__':
        #python sftp.py username/password@ip:port get remote local
        #python sftp.py username/password@ip:port upload remote local
            
        if len(sys.argv) < 5 :
                print 'sftp.py takes 4 argument (',(len(sys.argv)-1), 'given)'
                print 'get file or dir: get username/password@ip:port remote local'
                print 'put file or dir: put username/password@ip:port loacl remote'
        else:
                op = sys.argv[1]
                un,pw = sys.argv[2].split('/')
                pw,ip = pw.split('@')
                if ip.rfind(':') != -1:
                        ip,port = ip.split(':')
                else:
                        port = 22
                print op,ip,port,un,pw
        
                if sys.argv[1] == 'get' 
                        download(ip,port,un,pwd,sys.argv[3],sys.argv[4])
                elif sys.argv[1] != 'put':
                        upload(ip,port,un,pwd,sys.argv[4],sys.argv[3])
                else:
                    print 'invlid type:' ,sys.argv[1]
                    print 'get file or dir: get username/password@ip:port remote local'
                    print 'put file or dir: put username/password@ip:port loacl remote'
```