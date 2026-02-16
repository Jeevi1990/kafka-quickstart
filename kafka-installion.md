Kafka Installation Guide
1. Using Docker (Windows & macOS)
Prerequisites
Install Docker Desktop:
Download Docker for Windows
Download Docker for Mac
Steps
Start Docker Desktop.
Create a docker-compose.yml file with the following content:
Open a terminal in the directory containing docker-compose.yml.
Run:
Kafka will be available at localhost:9092.
2. Without Docker
Windows
Prerequisites
Install Java (JDK 8+): Download Java
Download Kafka: Kafka Downloads
Steps
Extract the Kafka archive.
Open Command Prompt and navigate to the Kafka directory.
Start Zookeeper:
Open a new Command Prompt, start Kafka:
Kafka will be running at localhost:9092.
macOS
Prerequisites
Install Java (JDK 8+):
Download Kafka: Kafka Downloads
Steps
Extract the Kafka archive.
Open Terminal and navigate to the Kafka directory.
Start Zookeeper:
Open a new Terminal, start Kafka:
Kafka will be running at localhost:9092.
