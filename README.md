# Opensearch Workshop

## System Config

### Windows

- ใช้ Docker Desktop + WSL
- ตั้งค่า vm.max_map_count (ถ้า start opensearch docekr ไม่ได้)

```
wsl -d docker-desktop

# echo "vm.max_map_count=262144" >> /etc/sysctl.conf

# sysctl -p
```

### Linux

- ตั้งค่า vm.max_map_count

```
$ echo  "vm.max_map_count=262144"| sudo tee -a  /etc/sysctl.conf

$ sudo sysctl -p
```
### macOS

ถ้า Start opensearch docker ไม่ได้ค่อยว่ากัน :p


## Config & ENV

### ตรวจสอบ config เบื้องต้น

```
$ docker-compose config
```
### ตั้งค่า .env

หากต้องการปรับแต่ง IP / PORT และอื่น ๆ สามารถตั้งค่าใน .env ให้สัมพันธ์กับ `docker-compose.yml`

`cp default.env .env`

```bash
OS_MEM=1512M
LOG_LEVEL=ERROR
OS_LIMIT_CPU=2
OS_LIMIT_MEM=3G
OS_IP=127.0.0.1
OS_PORT=9200
OS_DASHBOARD_IP=127.0.0.1
OS_DASHBOARD_PORT=5601
```
** ตรวจสอบทุกครั้งที่มีการแก้ไข

```
$ docker-compose config
```

## Start Services

```
$ docker-compose up -d
```

รอ build สักครู่ 

### ตรวจสอบ

```
$ docker-compose ps
```

### log

```
$ docker-compose logs -f --tail 50
```

## Test Opensearch & Dashboard 

### Opensearch

```
$ curl http://localhost:9200
```
** ผลหน้าตาประมาณนี้

```
{
  "name" : "os",
  "cluster_name" : "os-cluster",
  "cluster_uuid" : "o34IrepUQi-SBcrX0N5IVQ",
  "version" : {
    "distribution" : "opensearch",
    "number" : "2.0.1",
    "build_type" : "tar",
    "build_hash" : "6462a546240f6d7a158519499729bce12dc1058b",
    "build_date" : "2022-06-15T08:47:29.411959067Z",
    "build_snapshot" : false,
    "lucene_version" : "9.1.0",
    "minimum_wire_compatibility_version" : "7.10.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "The OpenSearch Project: https://opensearch.org/"
}

```

### Dashboard

เปิดด้วย Web browser
```
http://localhost:5601
```
---