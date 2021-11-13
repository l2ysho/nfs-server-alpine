# nfs-server-alpine

Fork of [nfs-server-alpine](https://github.com/sjiveson/nfs-server-alpine) with new ENV variable for full exports file modification and default value suitable for mac clients.

All options of export file is able to setup with env variable OPTIONS, default value is: 

`OPTIONS=rw,fsid=0,async,no_subtree_check,no_auth_nlm,insecure,anonuid=1000,anongid=1000,all_squash`

## basic setup

docker-compose.yml

```
version: '3.8'

services:
  nfs:
    image: l2ysho/nfs-server-alpine
    container_name: nfs
    restart: unless-stopped
    privileged: true
    environment:
      # path to mounted directory (required)
      - SHARED_DIRECTORY=/data
      # permit to ip range (optional)
      - PERMITTED=192.168.1.* 
      # custom exports options (optional)
     - OPTIONS=rw,fsid=0,sync,no_subtree_check,no_auth_nlm,insecure,no_root_squash
    volumes:
      - /path/to/shared/data/folder:/data
    ports:
      - 2049:2049
```
