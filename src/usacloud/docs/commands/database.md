# コマンドリファレンス / database

## コマンド一覧

- Basic Commands
    - [list](#list)
    - [create](#create)
    - [read](#read)
    - [update](#update)
    - [delete](#delete)
- Power Management Commands
    - [boot](#boot)
    - [shutdown](#shutdown)
    - [reset](#reset)
- Monitoring Commands
    - [monitor-cpu](#monitor-cpu)
    - [monitor-database](#monitor-database)
    - [monitor-disk](#monitor-disk)
    - [monitor-interface](#monitor-interface)
- Other Commands
    - [wait-until-ready](#wait-until-ready)
    - [wait-until-shutdown](#wait-until-shutdown)


## list {: #list }

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

  === Zone options ===

      --zone string   (*required) 

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

```console
Usage:
  create [flags]

Flags:

  === Common options ===

      --name string          (*required) 
      --description string   
      --tags strings         
      --icon-id int          

  === Plan options ===

      --database-type string   (*required) options: [postgresql/postgres/mariadb]
      --plan string            (*required) options: [10g/30g/90g/240g/500g/1t]

  === WebUI options ===

      --enable-web-ui   

  === Backup options ===

      --enable-backup                  
      --backup-weekdays strings        (*required) options: [all/sun/mon/tue/wed/thu/fri/sat]
      --backup-start-time-hour int     
      --backup-start-time-minute int   options: [0/15/30/45]

  === Network options ===

      --switch-id int          (*required) 
      --ip-address strings     (*required) (aliases: --ipaddress)
      --netmask int            (*required) (aliases: --network-mask-len)
      --gateway string         (aliases: --default-route)
      --port int               
      --source-range strings   (aliases: --source-network)

  === Replication options ===

      --enable-replication             
      --replica-user-password string   (*required) 

  === User options ===

      --username string   (*required) 
      --password string   (*required) 

  === Zone options ===

      --zone string   (*required) 

  === Wait options ===

      --no-wait   

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

## read {: #read }

```console
Usage:
  read [flags]

Aliases:
  read, show

Flags:

  === Zone options ===

      --zone string   (*required) 

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

```console
Usage:
  update [flags]

Flags:

  === Common options ===

      --name string          
      --description string   
      --tags strings         
      --icon-id int          

  === WebUI options ===

      --enable-web-ui   

  === Backup options ===

      --enable-backup                  
      --backup-weekdays strings        (*required) options: [all/sun/mon/tue/wed/thu/fri/sat]
      --backup-start-time-hour int     
      --backup-start-time-minute int   

  === Network options ===

      --source-range strings   (aliases: --source-network)

  === Replication options ===

      --enable-replication             
      --replica-user-password string   (*required) 

  === Zone options ===

      --zone string   (*required) 

  === Wait options ===

      --no-wait   

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

## delete {: #delete }

```console
Usage:
  delete [flags]

Aliases:
  delete, rm

Flags:

  === Delete options ===

  -f, --force   

  === Zone options ===

      --zone string   (*required) 

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

## boot {: #boot }

```console
Usage:
  boot [flags]

Aliases:
  boot, power-on

Flags:

  === Zone options ===

      --zone string   (*required) 

  === Wait options ===

      --no-wait   

  === Input options ===

  -y, --assumeyes           Assume that the answer to any question which would be asked is yes
      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Parameter example ===

      --example   Output example parameters with JSON format

```

## shutdown {: #shutdown }

```console
Usage:
  shutdown [flags]

Aliases:
  shutdown, power-off

Flags:

  === Database-specific options ===

  -f, --force-shutdown   (aliases: --force)

  === Zone options ===

      --zone string   (*required) 

  === Wait options ===

      --no-wait   

  === Input options ===

  -y, --assumeyes           Assume that the answer to any question which would be asked is yes
      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Parameter example ===

      --example   Output example parameters with JSON format

```

## reset {: #reset }

```console
Usage:
  reset [flags]

Flags:

  === Zone options ===

      --zone string   (*required) 

  === Input options ===

  -y, --assumeyes           Assume that the answer to any question which would be asked is yes
      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Parameter example ===

      --example   Output example parameters with JSON format

```

## monitor-cpu {: #monitor-cpu }

```console
Usage:
  monitor-cpu [flags]

Flags:

  === Monitor options ===

      --end string     
      --start string   

  === Zone options ===

      --zone string   (*required) 

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

## monitor-database {: #monitor-database }

```console
Usage:
  monitor-database [flags]

Flags:

  === Monitor options ===

      --end string     
      --start string   

  === Zone options ===

      --zone string   (*required) 

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

## monitor-disk {: #monitor-disk }

```console
Usage:
  monitor-disk [flags]

Flags:

  === Monitor options ===

      --end string     
      --start string   

  === Zone options ===

      --zone string   (*required) 

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

## monitor-interface {: #monitor-interface }

```console
Usage:
  monitor-interface [flags]

Aliases:
  monitor-interface, monitor-nic

Flags:

  === Monitor options ===

      --end string     
      --start string   

  === Zone options ===

      --zone string   (*required) 

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

## wait-until-ready {: #wait-until-ready }

```console
Usage:
  wait-until-ready [flags]

Aliases:
  wait-until-ready, wait-for-boot

Flags:

  === Zone options ===

      --zone string   (*required) 

  === Input options ===

      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Parameter example ===

      --example   Output example parameters with JSON format

```

## wait-until-shutdown {: #wait-until-shutdown }

```console
Usage:
  wait-until-shutdown [flags]

Aliases:
  wait-until-shutdown, wait-for-down

Flags:

  === Zone options ===

      --zone string   (*required) 

  === Input options ===

      --generate-skeleton   Output skeleton of parameters with JSON format (aliases: --skeleton)
      --parameters string   Input parameters in JSON format

  === Parameter example ===

      --example   Output example parameters with JSON format

```

