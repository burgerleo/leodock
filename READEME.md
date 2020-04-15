# 資料結構
```
leodock
├── apache2
│   ├── apache2.conf
│   ├── sites-available
├── crontabs
│   └── root-example
├── logs
│   └── apache2
├── mysql
│   ├── Dockerfile
├── php
│   ├── Dockerfile
│   ├── supervisor
├── redis
│   └── Dockerfile
├── docker-compose.yml
└── READEME.md
```

# 設定環境

```
cp .env.example .env

cp apache2/ports.conf.example apache2/ports.conf

cp crontabs/root-example crontabs/root
```

# 啟動
```
docker-compose up -d 
```