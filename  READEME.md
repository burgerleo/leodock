# 資料結構
```
leodock
├── docker-compose.yml
├── logs
├── apache2
│   ├── apache2.conf
│   └── sites
│       └── sample.conf.example
├── mysql
│   ├── Dockerfile
│   └── my.cnf
└── php
    ├── Dockerfile
    ├── php.ini
    └── vhost.conf
```

# 設定環境

```
cp .env.example .env
```

# 啟動
```
docker-composer up -d 
```