#### Setting up Docker MongoDB server

starting docker
```bash
sudo systemctl start docker
```
enabling docker
```bash
sudo systemctl enable docker

Synchronizing state of docker.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable docker
Created symlink '/etc/systemd/system/multi-user.target.wants/docker.service' → '/usr/lib/systemd/system/docker.service'.
```
starting mongo server on port `27017`
```bash
sudo docker run --name mongodb -d -p 27017:27017 mongo

Unable to find image 'mongo:latest' locally
latest: Pulling from library/mongo
2726e237d1a3: Pull complete 
4113c9f6bc12: Pull complete 
6bd25e6544db: Pull complete 
114959114e76: Pull complete 
74e29de52e16: Pull complete 
a7aa415a3894: Pull complete 
b4c1b5279c53: Pull complete 
2d3498acb5d9: Pull complete 
Digest: sha256:cc62438c8ef61ce02f89b4f7c026e735df4580e8cd8857980d12e0eae73bf044
Status: Downloaded newer image for mongo:latest
17e52bc85f0ad10ac3831df6673ffc6ecd60395a77bbdf48acf376018ac3076d
```
making sure that `docker` is running
```bash
docker ps

Device "vethedab71a@if4" does not exist.
Device "vethedab71a@if4" does not exist.
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                           NAMES
17e52bc85f0a   mongo     "docker-entrypoint.s…"   35 seconds ago   Up 32 seconds   0.0.0.0:27017->27017/tcp, :::27017->27017/tcp   mongodb
```
getting a `mongodb` shell and testing it
```bash
sudo docker exec -it mongodb mongosh

Current Mongosh Log ID: 680adf5089fb120845d861df
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.5.0
Using MongoDB:          8.0.8
Using Mongosh:          2.5.0

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/


To help improve our products, anonymous usage data is collected and sent to MongoDB periodically (https://www.mongodb.com/legal/privacy-policy).
You can opt-out by running the disableTelemetry() command.

------
   The server generated these startup warnings when booting
   2025-04-25T01:02:22.303+00:00: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem
   2025-04-25T01:02:22.555+00:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
   2025-04-25T01:02:22.555+00:00: For customers running the current memory allocator, we suggest changing the contents of the following sysfsFile
   2025-04-25T01:02:22.555+00:00: We suggest setting the contents of sysfsFile to 0.
   2025-04-25T01:02:22.555+00:00: vm.max_map_count is too low
   2025-04-25T01:02:22.555+00:00: We suggest setting swappiness to 0 or 1, as swapping can cause performance problems.
------

test> db.stats()
{
  db: 'test',
  collections: Long('0'),
  views: Long('0'),
  objects: Long('0'),
  avgObjSize: 0,
  dataSize: 0,
  storageSize: 0,
  indexes: Long('0'),
  indexSize: 0,
  totalSize: 0,
  scaleFactor: Long('1'),
  fsUsedSize: 0,
  fsTotalSize: 0,
  ok: 1
}
test> exit
```

#### Setting up `mongoCLI`
URL: https://github.com/KenanBek/mongocli
`git clone`
```bash
git clone https://github.com/KenanBek/mongocli.git                                                                                                                                                                                      

Cloning into 'mongocli'...                                                                                                                                                                  
remote: Enumerating objects: 114, done.                                                                                                                                                     
remote: Counting objects: 100% (18/18), done.                                                                                                                                               
remote: Compressing objects: 100% (7/7), done.                                                                                                                                              
remote: Total 114 (delta 13), reused 11 (delta 11), pack-reused 96 (from 1)                                                                                                                 
Receiving objects: 100% (114/114), 38.74 KiB | 2.28 MiB/s, done.                                                                                                                            
Resolving deltas: 100% (47/47), done.   
```
usage
```bash
┌──(root💀gobots)-[25Apr2025 01:32:30]-[/home/kali/tools/mongocli]
└─# cat README.md  
Device "veth9b7a1c9@if4" does not exist.
Device "veth9b7a1c9@if4" does not exist.
![Gopher with MongoDB](https://cdn.cp.adobe.io/content/2/dcx/8182b7fd-7661-4b81-8a2e-276c203ecfa3/rendition/preview.jpg/version/0/format/jpg/dimension/width/size/1200)

# MongoCLI

**C**ommand **L**ine **I**nterface for **Mongo**DB. **MongoCLI**.

Status: development in progress

## Features

- `mongocli ping` - check database connection, ping
- `mongocli dbs` - list existing database names 
- `mongocli colls` or `mongocli colls -d <db name>` - list collection names
- `mongocli count <coll name>` - count documents in the collection
- `mongocli list <coll name>` - list documents in the collection
- Use configuration file for default connection settings and database name: `~/mongocli.yml` (example configuration file included)
- Use command line args for connection settings: `mongocli ping -s localhost -p 27017 -d config` or `mongocli ping --server localhost --port 27017 --database config`
```
building tool 
![[Pasted image 20250424220012.png]]

#### Testing `mongoCLI`

listing databases
![[Pasted image 20250424220128.png]]
listing `collection names` in `admin` database
![[Pasted image 20250424220212.png]]
listing `collection names`in `config` database
![[Pasted image 20250424221116.png]]
listing `count` of `system.version` collection in the `admin` database
![[Pasted image 20250424224615.png]]
listing the `contents` of the `system.version` collection of the `admin` database
![[Pasted image 20250425145226.png]]
