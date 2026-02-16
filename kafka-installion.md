# Kafka Installation Guide

## 1. Using Docker (Windows & macOS)

### Prerequisites
- Install Docker Desktop:
  - [Download Docker for Windows](https://www.docker.com/products/docker-desktop/)
  - [Download Docker for Mac](https://www.docker.com/products/docker-desktop/)

### Steps
1. Start Docker Desktop.
2. Create a `docker-compose.yml` file with the following content:
   ```yaml
   version: '3'
   services:
     zookeeper:
       image: confluentinc/cp-zookeeper:latest
       environment:
         ZOOKEEPER_CLIENT_PORT: 2181
         ZOOKEEPER_TICK_TIME: 2000
     kafka:
       image: confluentinc/cp-kafka:latest
       environment:
         KAFKA_BROKER_ID: 1
         KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
         KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://localhost:9092
         KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
       ports:
         - "9092:9092"
   ```
3. Open a terminal in the directory containing `docker-compose.yml`.
4. Run:
   ```sh
   docker-compose up -d
   ```
5. Kafka will be available at `localhost:9092`.

---


## 2. Without Docker

### Latest Kafka (KRaft Mode, No Zookeeper)

#### Prerequisites
- Install Java (JDK 11+ recommended):
  - [Download Java for Windows](https://adoptopenjdk.net/)
  - On macOS: `brew install openjdk`
- Download Kafka (3.0+): [Kafka Downloads](https://kafka.apache.org/downloads)

#### Steps (Windows & macOS)
1. Extract the Kafka archive.
2. Open a terminal (Command Prompt for Windows, Terminal for macOS) and navigate to the Kafka directory.
3. Initialize storage directories (only needed once):
   ```sh
   bin/kafka-storage.sh format -t $(bin/kafka-storage.sh random-uuid) -c config/kraft/server.properties
   ```
   - On Windows, use `bin\windows\kafka-storage.bat` and adjust paths accordingly.
4. Start Kafka in KRaft mode:
   ```sh
   bin/kafka-server-start.sh config/kraft/server.properties
   ```
   - On Windows, use `bin\windows\kafka-server-start.bat config\kraft\server.properties`
5. Kafka will be running at `localhost:9092`.

#### Notes
- No Zookeeper is required for KRaft mode.
- Use the `config/kraft/server.properties` file for configuration.

---

### Legacy Mode (With Zookeeper)

#### Windows
- Install Java (JDK 8+): [Download Java](https://adoptopenjdk.net/)
- Download Kafka: [Kafka Downloads](https://kafka.apache.org/downloads)

##### Steps
1. Extract the Kafka archive.
2. Open Command Prompt and navigate to the Kafka directory.
3. Start Zookeeper:
   ```sh
   .\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
   ```
4. Open a new Command Prompt, start Kafka:
   ```sh
   .\bin\windows\kafka-server-start.bat .\config\server.properties
   ```
5. Kafka will be running at `localhost:9092`.

#### macOS
- Install Java (JDK 8+):  
  ```sh
  brew install openjdk
  ```
- Download Kafka: [Kafka Downloads](https://kafka.apache.org/downloads)

##### Steps
1. Extract the Kafka archive.
2. Open Terminal and navigate to the Kafka directory.
3. Start Zookeeper:
   ```sh
   bin/zookeeper-server-start.sh config/zookeeper.properties
   ```
4. Open a new Terminal, start Kafka:
   ```sh
   bin/kafka-server-start.sh config/server.properties
   ```
5. Kafka will be running at `localhost:9092`.
