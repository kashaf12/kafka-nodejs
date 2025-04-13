# Kafka Docker Compose Setup

This project provides a Docker Compose setup for running a Kafka environment, including Zookeeper, Kafka, and Kafka UI. Additionally, it includes scripts for Kafka administration, producing, and consuming messages.

## Services

### 1. Zookeeper

- **Image**: `zookeeper`
- **Ports**: `2181:2181`

### 2. Kafka

- **Image**: `confluentinc/cp-kafka`
- **Depends on**: Zookeeper
- **Ports**:
  - `9092:9092` (external)
  - `29092` (internal)
- **Environment Variables**:
  - `KAFKA_ZOOKEEPER_CONNECT`: `zookeeper:2181`
  - `KAFKA_ADVERTISED_LISTENERS`: `PLAINTEXT://localhost:9092`
  - `KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR`: `1`

### 3. Kafka UI

- **Image**: `provectuslabs/kafka-ui`
- **Container Name**: `kafka-ui`
- **Ports**: `8080:8080`
- **Environment Variables**:
  - `DYNAMIC_CONFIG_ENABLED`: `true`

## Usage

1. Ensure Docker and Docker Compose are installed on your system.
2. Clone this repository.
3. Navigate to the project directory.
4. Run the following command to start the services:
   ```bash
   docker-compose up
   ```

## Scripts

### 1. Admin Script

The admin script initializes Kafka by creating topics.

- **File**: [`src/admin.js`](src/admin.js)
- **Usage**:
  ```bash
  node src/admin.js
  ```

### 2. Producer Script

The producer script sends messages to the `rider-updates` topic.

- **File**: [`src/producer.js`](src/producer.js)
- **Usage**:
  ```bash
  node src/producer.js
  ```
  Enter messages in the format `<riderName> <location>` (e.g., `John north`).

### 3. Consumer Script

The consumer script listens to messages from the `rider-updates` topic.

- **File**: [`src/consumer.js`](src/consumer.js)
- **Usage**:
  ```bash
  node src/consumer.js <groupId>
  ```
  Replace `<groupId>` with a unique consumer group ID.

### 4. Kafka Client

The Kafka client is configured to connect to the Kafka broker.

- **File**: [`src/client.js`](src/client.js)
- **Configuration**:
  - **Client ID**: `my-app`
  - **Brokers**: `localhost:9092`

## Notes

- Ensure that the ports `2181`, `9092`, and `8080` are available on your system.
- Modify the `docker-compose.yml` file as needed to suit your environment.

## License

This project is licensed under the MIT License.
