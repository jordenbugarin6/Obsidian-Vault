![[Pasted image 20240907132256.png]]

#### Docker Setup

Downloading and unzipping `lostpyramid.zip`
```bash
┌──(root💀gobots)-[07Sep2024 16:58:54]-[/home/kali/SUT/CSAW]
└─# ls
lostpyramid.zip

┌──(root💀gobots)-[07Sep2024 16:58:54]-[/home/kali/SUT/CSAW]
└─# unzip lostpyramid.zip 
```
`cd` to `lostpyramid`
```bash
┌──(root💀gobots)-[07Sep2024 16:58:58]-[/home/kali/SUT/CSAW]
└─# ls
__MACOSX  lostpyramid  lostpyramid.zip

┌──(root💀gobots)-[07Sep2024 16:58:59]-[/home/kali/SUT/CSAW]
└─# cd lostpyramid 
```
start `docker` and build
```bash
┌──(root💀gobots)-[07Sep2024 17:00:00]-[/home/kali/SUT/CSAW/lostpyramid]
└─# systemctl start docker 

┌──(root💀gobots)-[07Sep2024 17:11:52]-[/home/kali/SUT/CSAW/lostpyramid]
└─# docker build -t lostpyramid_image .
Sending build context to Docker daemon  4.188MB
Step 1/12 : FROM python:3.8-slim-buster
 ---> addd6962740a
Step 2/12 : RUN useradd -r ctf
 ---> Using cache
 ---> 860392152e14
Step 3/12 : WORKDIR /app
 ---> Using cache
 ---> 14049178dde4
Step 4/12 : COPY requirements.txt ./
 ---> Using cache
 ---> 36742e7e6e9b
Step 5/12 : RUN pip3 install -r requirements.txt
 ---> Using cache
 ---> 26df55c02e24
Step 6/12 : COPY ./ ./
 ---> Using cache
 ---> 5bbab795317a
Step 7/12 : RUN chown -R ctf /app
 ---> Using cache
 ---> facdde6bb581
Step 8/12 : USER ctf
 ---> Using cache
 ---> 94c38bab1cde
Step 9/12 : ENV KINGSDAY="TESTINGDATE"
 ---> Using cache
 ---> bab3b1ec6b0c
Step 10/12 : ENV FLASK_APP="app.py"
 ---> Using cache
 ---> f8f09d584f64
Step 11/12 : EXPOSE 8050
 ---> Using cache
 ---> b0a78d42821f
Step 12/12 : CMD ["gunicorn", "-b", "0.0.0.0:8050", "-w 1", "app:app"]
 ---> Using cache
 ---> f21faad9aa7b
Successfully built f21faad9aa7b
Successfully tagged lostpyramid_image:latest
```
running `docker` `lostpyramid_container`
```bash
┌──(root💀gobots)-[07Sep2024 17:12:40]-[/home/kali/SUT/CSAW/lostpyramid]
└─# docker run -d -p 1337:1337 --name lostpyramid_container lostpyramid_image
6094de136256b2a1b63dfdf9bb401caf797725eaf6da5da7fe69baaff490ff3f

┌──(root💀gobots)-[07Sep2024 17:13:08]-[/home/kali/SUT/CSAW/lostpyramid]
└─# docker ls                                                                                         
Device "vetheef998a@if23" does not exist.
Device "vetheef998a@if23" does not exist.
docker: 'ls' is not a docker command.
See 'docker --help'
```
check if it was running - was still unable to connect to the web server locally
```bash
┌──(root💀gobots)-[07Sep2024 17:13:23]-[/home/kali/SUT/CSAW/lostpyramid]
└─# docker ps
Device "vetheef998a@if23" does not exist.
Device "vetheef998a@if23" does not exist.
CONTAINER ID   IMAGE               COMMAND                  CREATED          STATUS          PORTS                                                 NAMES
6094de136256   lostpyramid_image   "gunicorn -b 0.0.0.0…"   19 seconds ago   Up 18 seconds   0.0.0.0:1337->1337/tcp, :::1337->1337/tcp, 8050/tcp   lostpyramid_container
```
 was still unable to connect to the web server locally

Connected to the `lostpyramid_container` with the `/bin/bash`
```bash
┌──(root💀gobots)-[07Sep2024 17:18:59]-[/home/kali/SUT/CSAW/lostpyramid]
└─# docker exec -it lostpyramid_container /bin/bash
```
Once on with a shell run the `gunicorn` command to enable the application on `0.0.0.0`
```bash
ctf@6094de136256:/app$ gunicorn -b 0.0.0.0:1337 app:app
[2024-09-07 17:19:51 +0000] [16] [INFO] Starting gunicorn 23.0.0
[2024-09-07 17:19:51 +0000] [16] [INFO] Listening at: http://0.0.0.0:1337 (16)
[2024-09-07 17:19:51 +0000] [16] [INFO] Using worker: sync
[2024-09-07 17:19:51 +0000] [18] [INFO] Booting worker with pid: 18
```
navigate to `0.0.0.0:1337`
![[Pasted image 20240907134550.png]]
stopping docker because flag was gained
```bash
┌──(root💀gobots)-[07Sep2024 17:46:25]-[/home/kali/SUT/CSAW/lostpyramid]
└─# docker stop 6094de136256
Device "vetheef998a@if23" does not exist.
Device "vetheef998a@if23" does not exist.
6094de136256
```