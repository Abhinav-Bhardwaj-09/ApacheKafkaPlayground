# Kafka + Kafka UI (Docker)

## One-Time Setup (First Time Only)

Run this when you clone/download the project for the first time.

```bash
docker compose -f kafka-compose.yml up -d
```

This will:

* Download Kafka image
* Download Kafka UI image
* Create containers
* Start Kafka and Kafka UI

Verify:

```bash
docker ps
```

Open Kafka UI:

```text
http://localhost:18080
```

---

## Daily Usage

### Start Kafka & Kafka UI

Whenever you restart your Mac or Docker Desktop:

```bash
docker compose -f kafka-compose.yml start
```

Verify:

```bash
docker ps
```

Open:

```text
http://localhost:18080
```

---

### Stop Kafka & Kafka UI

When you're done working:

```bash
docker compose -f kafka-compose.yml stop
```

---

## Reset Everything (Rarely Needed)

If containers become corrupted or you want a fresh start:

```bash
docker compose -f kafka-compose.yml down
```

Start again:

```bash
docker compose -f kafka-compose.yml up -d
```

---

## Troubleshooting

### Check Running Containers

```bash
docker ps
```

### Kafka Logs

```bash
docker logs -f kafka
```

### Kafka UI Logs

```bash
docker logs -f kafka-ui
```

---

## Topic Management - Kafka Commands (Learning Purpose)

Enter Kafka container:

```bash
docker exec -it kafka bash
```

### Create Topic

```bash
/opt/kafka/bin/kafka-topics.sh \
  --create \
  --topic messages-topic \
  --bootstrap-server localhost:9092
```

### List Topics

```bash
/opt/kafka/bin/kafka-topics.sh \
  --list \
  --bootstrap-server localhost:9092
```

### Describe Topic

```bash
/opt/kafka/bin/kafka-topics.sh \
  --describe \
  --topic messages-topic \
  --bootstrap-server localhost:9092
```

### Produce Messages

```bash
kafka-console-producer.sh \
--topic messages-topic \
--bootstrap-server localhost:9092
```

### Consume Messages

```bash
kafka-console-consumer.sh \
--topic messages-topic \
--bootstrap-server localhost:9092 \
--from-beginning
```

### Delete Topic

```bash
/opt/kafka/bin/kafka-topics.sh \
  --delete \
  --topic messages-topic \
  --bootstrap-server localhost:9092
```

### Exit Container

```bash
exit
```

---

## Notes

- Create a topic once and reuse it from your Spring Boot Producer and Consumer applications.
- Delete a topic only when you no longer need it or want to start fresh.
- In real-world applications, topics are usually long-lived and are rarely deleted.

---

## Kafka UI

Open Kafka UI:

```text
http://localhost:18080
```

From Kafka UI, you can:

- View Topics
- Create Topics
- Delete Topics
- Browse Messages
- View Consumer Groups

For learning:
1. Learn topic creation/deletion using CLI commands.
2. Use Kafka UI for day-to-day monitoring and message inspection.

---

## Quick Reference

### First Time

```bash
docker compose -f kafka-compose.yml up -d
```

### Every Day

```bash
docker compose -f kafka-compose.yml start
```

### Stop

```bash
docker compose -f kafka-compose.yml stop
```

### Fresh Start

```bash
docker compose -f kafka-compose.yml down
docker compose -f kafka-compose.yml up -d
```
