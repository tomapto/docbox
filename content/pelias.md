# pelias 环境配置

## pelias下载
### 依赖
1. Node.js4.0版本以上
2. Elasticsearch 2.3



### 创建脚本 install.sh
### 打开脚本粘贴代码到脚本中

```html
#!/bin/sh
for repository in schema api whosonfirst geonames openaddresses openstreetmap polylines; do
    git clone https://github.com/pelias/${repository}.git    # clone from Github
    pushd $repository > /dev/null                        # switch into importer directory
    git checkout production                              # or remove this line to stay with master
    npm install                                          # install npm dependencies
    popd > /dev/null                                     # return to code directory
done
```
### 运行脚本 

```html
$ sh install.sh
```

## pelias配置
创建并且配置~/pelias.json
打开文件并且将json配置写入

```json
{
    "esclient": {
        "apiVersion": "2.3",
        "keepAlive": true,
        "requestTimeout": "120000",
        "hosts": [
            {
                "env": "development",
                "protocol": "http",
                "host": "t0.map.design",
                "port": 9200
            }
        ],
        "log": [
            {
                "type": "stdio",
                "level": [
                    "error",
                    "warning"
                ]
            }
        ]
    },
    "elasticsearch": {
        "settings": {
            "index": {
                "number_of_replicas": "0",
                "number_of_shards": "5",
                "refresh_interval": "1m"
            }
        }
    },
    "interpolation": {
        "client": {
            "adapter": "null"
        }
    },
    "dbclient": {
        "statFrequency": 10000
    },
    "api": {
        "accessLog": "common",
        "host": "http://t0.map.design/",
        "indexName": "pelias",
        "version": "1.0",
        "textAnalyzer": "addressit"
    },
    "schema": {
        "indexName": "pelias"
    },
    "logger": {
        "level": "debug",
        "timestamp": true,
        "colorize": true
    },
    "acceptance-tests": {
        "endpoints": {
            "local": "http://t0.map.design:3100/v1/",
            "dev-cached": "http://pelias.dev.mapzen.com.global.prod.fastly.net/v1/",
            "dev": "http://pelias.dev.mapzen.com/v1/",
            "prod": "http://search.mapzen.com/v1/",
            "prod-uncached": "http://pelias.mapzen.com/v1/",
            "prodbuild": "http://pelias.prodbuild.mapzen.com/v1/"
        }
    },
    "imports": {
       "adminLookup": {
            "enabled": false 
        },
        "openstreetmap": {
            "datapath": "/mnt1/pelias/openstreetmap",
            "leveldbpath": "/tmp",
            "import": [
                {
                    "filename": "beijing.osm.pbf"
                }
            ]
        }
    }
}
```
## 安装elasticsearch 及插件
