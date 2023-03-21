# EC2 Setting information of Michael DevNet

## 1. Authority-Node

### 1.1. Execution Layer
- Screen name : el
- Type : geth
- Working directory : ~/agoranet/michael/
- Port : UDP: 30303;  TCP/IP: 30303
- Command :  


Init Execution Node
```shell
cmd/el/init_node 1
```

Run Execution Node
```shell
cmd/el/run_node 1
```

### 1.2. Consensus Layer
- Screen name : cl
- Type : beacon-chain
- Working directory : ~/agora-cl
- Port : UDP:3500, 4000, 12000, 13000; TCP/IP:3500, 4000, 12000, 13000
- Command :

Run Consensus Node
```shell
cmd/cl/run_node
```

### 1.3. ETH2 Validator
- Screen name : val
- Type : validator
- Working directory : ~/agora-cl
- Port :
- Command :

Import key - passwork is boa2022!@
```shell
cmd/cl/import_key 1
```

Run Validator
```shell
cmd/cl/run_validator
```


*****

## 2. EL-Scan
### 2.1. Execution Layer
- Screen name : el
- Type : geth
- Working directory : ~/agoranet/michael/
- Port : UDP: 30303;  TCP/IP: 30303
- Command :

Init Execution Node
```shell
cmd/el/init_node 0
```

Run Execution Node
```shell
cmd/el/run_node scan
```

### 2.2. Blockscout
- Screen name : scan
- Type : blockscout
- Working directory : ~/blockscout
- Port : TCP/IP: 14000
- Command :
  
Create Database
```shell
mix do ecto.create, ecto.migrate
```

Initialize Database
```shell
mix do ecto.drop
```

Run
```shell
mix phx.server
```

*****

## 3. CL-Scan
### 3.1. Execution Layer
- Screen name : el
- Type : geth
- Working directory : ~/agoranet/michael/
- Port : UDP: 30303;  TCP/IP: 30303
- Command :

Init Execution Node
```shell
cmd/el/init_node 0
```

Run Execution Node
```shell
cmd/el/run_node scan
```

### 3.2. ETH2 Beacon Explorer
- Screen name : scan
- Type : Beacon Explorer
- Working directory : ~/agora-scan
- Port :
- Command :

Run postgresql
```shell
docker-compose -f ~/agoranet/michael/config/agora-scan/docker-compose.yml up -d
```

Initialize database
```shell
sudo docker run -it --rm --net=host -v $(pwd):/src postgres:12.0 psql -f /src/tables.sql -d db -h 0.0.0.0 -U postgres
```

Compile database
```shell
sudo docker exec -ti golang bash
make all
```

Run explorer
```shell
./bin/explorer --config ~/agoranet/michael/config/agora-scan/config.yml
```

*****
