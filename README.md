# Clickhouse DB Installation
## Tutorial step-by-step how to install Clickhouse Database in Kali Linux

### 1. Update System and Install Dependencies

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl wget python3 python3-pip git gpg apt-transport-https ca-certificates dirmngr
```
### 2. Remove Old Repository and Clear APT Cache (If already)
```
sudo rm -f /etc/apt/sources.list.d/clickhouse.list
sudo rm -rf /var/lib/apt/lists/*
```

### 3. Download and Add the Latest GPG Key
```
curl -fsSL https://packages.clickhouse.com/rpm/lts/repodata/repomd.xml.key | sudo gpg --dearmor -o /usr/share/keyrings/clickhouse-keyring.gpg
```

### 4. Add ClickHouse Repository
```
ARCH=$(dpkg --print-architecture)
echo "deb [signed-by=/usr/share/keyrings/clickhouse-keyring.gpg arch=${ARCH}] https://packages.clickhouse.com/deb stable main" | sudo tee /etc/apt/sources.list.d/clickhouse.list
```

### 5. Update APT and Install ClickHouse
```
sudo apt update && sudo apt install -y clickhouse-server clickhouse-client
```

### 6. Start ClickHouse Without Authentication
```
sudo systemctl start clickhouse-server
sudo systemctl enable clickhouse-server
```
### 7. Create a Sample Database and Table
```
clickhouse-client --query "CREATE DATABASE IF NOT EXISTS testdb;"
clickhouse-client --query "CREATE TABLE IF NOT EXISTS testdb.users (id UInt32, name String, email String) ENGINE = MergeTree() ORDER BY id;"
clickhouse-client --query "INSERT INTO testdb.users VALUES (1, 'Alice', 'alice@example.com'), (2, 'Bob', 'bob@example.com');"
```
