# コマンドリファレンス / proxy-lb

## コマンド一覧

- Basic Commands
    - [list](#list)
    - [create](#create)
    - [read](#read)
    - [update](#update)
    - [delete](#delete)
- Operation Commands
    - [health-status](#health-status)
    - [renew-lets-encrypt-cert](#renew-lets-encrypt-cert)
- Monitoring Commands
    - [monitor-connection](#monitor-connection)


## list {: #list }

##### Usage
```console
Usage:
  list [flags]

Aliases:
  list, ls, find, select

Flags:

  === Filter options ===

      --names strings   
      --tags strings    

  === Limit/Offset options ===

      --count int   (aliases: --max, --limit)
      --from int    (aliases: --offset)

  === Input options ===

      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Output options ===

      --format string        Output format in Go templates (aliases: --fmt)
  -o, --output-type string   Output format: one of the following [table/json/yaml] (aliases: --out)
      --query string         JMESPath query
  -q, --quiet                Output IDs only

  === Parameter example ===

      --example   Output example parameters with JSON format

```


## create {: #create }

##### Usage
```console
Usage:
  create [flags]

Flags:

  === Common options ===

      --name string          (*required) 
      --description string   
      --tags strings         
      --icon-id int          

  === Proxy-Lb-specific options ===

      --bind-ports string                 
      --health-check-delay-loop int       (*required)  (default 10)
      --health-check-host string          
      --health-check-path string           (default "/")
      --health-check-protocol string      (*required)  (default "http")
      --inactive-sec int                   (default 10)
      --lets-encrypt-accept-tos           The flag to accept the current Let's Encrypt terms of service(see: https://letsencrypt.org/repository/)
      --lets-encrypt-common-name string   
      --lets-encrypt-enabled              
      --plan string                       (*required) options: [100/500/1000/5000/10000/50000/100000] (default "100")
      --region string                     (*required) options: [tk1/is1/anycast] (default "is1")
      --rules string                      
      --servers string                    
      --sorry-server-ip-address string    (aliases: --ipaddress)
      --sorry-server-port int             
      --sticky-session-enabled            
      --sticky-session-method string      
      --vip-fail-over                     

  === Input options ===

  -y, --assumeyes           Assume that the answer to any question which would be asked is yes
      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Output options ===

      --format string        Output format in Go templates (aliases: --fmt)
  -o, --output-type string   Output format: one of the following [table/json/yaml] (aliases: --out)
      --query string         JMESPath query
  -q, --quiet                Output IDs only

  === Parameter example ===

      --example   Output example parameters with JSON format

```

##### Parameter Examples
```console
{
    "Name": "example",
    "Description": "example",
    "Tags": [
        "tag1=example1",
        "tag2=example2"
    ],
    "IconID": 123456789012,
    "Plan": "100 | 500 | 1000 | 5000 | 10000 | 50000 | 100000",
    "HealthCheck": {
        "Protocol": "http | tcp",
        "Path": "/healthz",
        "Host": "www.example.com",
        "DelayLoop": 10
    },
    "SorryServer": {
        "IPAddress": "192.0.2.11",
        "Port": 80
    },
    "LetsEncrypt": {
        "CommonName": "www.example.com",
        "Enabled": true,
        "AcceptTOS": false
    },
    "StickySession": {
        "Method": "cookie",
        "Enabled": true
    },
    "Timeout": {
        "InactiveSec": 10
    },
    "UseVIPFailover": true,
    "Region": "tk1 | is1 | anycast",
    "BindPorts": [
        {
            "ProxyMode": "http | https | tcp",
            "Port": 80,
            "RedirectToHTTPS": true,
            "SupportHTTP2": true,
            "AddResponseHeader": [
                {
                    "Header": "Cache-Control",
                    "Value": "public, max-age=900"
                }
            ]
        }
    ],
    "Servers": [
        {
            "IPAddress": "192.0.2.11",
            "Port": 80,
            "ServerGroup": "group1",
            "Enabled": true
        }
    ],
    "Rules": [
        {
            "Host": "www2.example.com",
            "Path": "/foo",
            "ServerGroup": "group1"
        }
    ]
}
```


## read {: #read }

##### Usage
```console
Usage:
  read { ID | NAME | TAG } [flags]

Aliases:
  read, show

Flags:

  === Input options ===

      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Output options ===

      --format string        Output format in Go templates (aliases: --fmt)
  -o, --output-type string   Output format: one of the following [table/json/yaml] (aliases: --out)
      --query string         JMESPath query
  -q, --quiet                Output IDs only

  === Parameter example ===

      --example   Output example parameters with JSON format

```


## update {: #update }

##### Usage
```console
Usage:
  update { ID | NAME | TAG }... [flags]

Flags:

  === Common options ===

      --name string          
      --description string   
      --tags strings         
      --icon-id int          

  === Proxy-Lb-specific options ===

      --bind-ports string                 
      --health-check-delay-loop int       
      --health-check-host string          
      --health-check-path string          
      --health-check-protocol string      
      --inactive-sec int                  
      --lets-encrypt-accept-tos           The flag to accept the current Let's Encrypt terms of service(see: https://letsencrypt.org/repository/)
      --lets-encrypt-common-name string   
      --lets-encrypt-enabled              
      --plan string                       options: [100/500/1000/5000/10000/50000/100000]
      --rules string                      
      --servers string                    
      --sorry-server-ip-address string    (aliases: --ipaddress)
      --sorry-server-port int             
      --sticky-session-enabled            
      --sticky-session-method string      

  === Input options ===

  -y, --assumeyes           Assume that the answer to any question which would be asked is yes
      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Output options ===

      --format string        Output format in Go templates (aliases: --fmt)
  -o, --output-type string   Output format: one of the following [table/json/yaml] (aliases: --out)
      --query string         JMESPath query
  -q, --quiet                Output IDs only

  === Parameter example ===

      --example   Output example parameters with JSON format

```

##### Parameter Examples
```console
{
    "Name": "example",
    "Description": "example",
    "Tags": [
        "tag1=example1",
        "tag2=example2"
    ],
    "IconID": 123456789012,
    "Plan": "100 | 500 | 1000 | 5000 | 10000 | 50000 | 100000",
    "HealthCheck": {
        "Protocol": "http | tcp",
        "Path": "/healthz",
        "Host": "www.example.com",
        "DelayLoop": 10
    },
    "SorryServer": {
        "IPAddress": "192.0.2.11",
        "Port": 80
    },
    "LetsEncrypt": {
        "CommonName": "www.example.com",
        "Enabled": true,
        "AcceptTOS": false
    },
    "StickySession": {
        "Method": "cookie",
        "Enabled": true
    },
    "Timeout": {
        "InactiveSec": 10
    },
    "BindPortsData": null,
    "BindPorts": [
        {
            "ProxyMode": "http | https | tcp",
            "Port": 80,
            "RedirectToHTTPS": true,
            "SupportHTTP2": true,
            "AddResponseHeader": [
                {
                    "Header": "Cache-Control",
                    "Value": "public, max-age=900"
                }
            ]
        }
    ],
    "ServersData": null,
    "Servers": [
        {
            "IPAddress": "192.0.2.11",
            "Port": 80,
            "ServerGroup": "group1",
            "Enabled": true
        }
    ],
    "RulesData": null,
    "Rules": [
        {
            "Host": "www2.example.com",
            "Path": "/foo",
            "ServerGroup": "group1"
        }
    ]
}
```


## delete {: #delete }

##### Usage
```console
Usage:
  delete { ID | NAME | TAG }... [flags]

Aliases:
  delete, rm

Flags:

  === Error handling options ===

      --fail-if-not-found   

  === Input options ===

  -y, --assumeyes           Assume that the answer to any question which would be asked is yes
      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Output options ===

      --format string        Output format in Go templates (aliases: --fmt)
  -o, --output-type string   Output format: one of the following [table/json/yaml] (aliases: --out)
      --query string         JMESPath query
  -q, --quiet                Output IDs only

  === Parameter example ===

      --example   Output example parameters with JSON format

```


## health-status {: #health-status }

##### Usage
```console
Usage:
  health-status { ID | NAME | TAG }... [flags]

Aliases:
  health-status, health

Flags:

  === Input options ===

      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Output options ===

      --format string        Output format in Go templates (aliases: --fmt)
  -o, --output-type string   Output format: one of the following [table/json/yaml] (aliases: --out)
      --query string         JMESPath query
  -q, --quiet                Output IDs only

  === Parameter example ===

      --example   Output example parameters with JSON format

```


## renew-lets-encrypt-cert {: #renew-lets-encrypt-cert }

##### Usage
```console
Usage:
  renew-lets-encrypt-cert { ID | NAME | TAG }... [flags]

Flags:

  === Input options ===

  -y, --assumeyes           Assume that the answer to any question which would be asked is yes
      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Parameter example ===

      --example   Output example parameters with JSON format

```


## monitor-connection {: #monitor-connection }

##### Usage
```console
Usage:
  monitor-connection { ID | NAME | TAG }... [flags]

Aliases:
  monitor-connection, monitor

Flags:

  === Monitor options ===

      --end string     
      --start string   

  === Input options ===

      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Output options ===

      --format string        Output format in Go templates (aliases: --fmt)
  -o, --output-type string   Output format: one of the following [table/json/yaml] (aliases: --out)
      --query string         JMESPath query
  -q, --quiet                Output IDs only

  === Parameter example ===

      --example   Output example parameters with JSON format

```


