
```markdown
## Amazon DynamoDB with Fault Tolerance  
Course Project - Distributed Systems

This project implements a distributed key-value store system based on the principles of Amazon DynamoDB with fault tolerance features.
 The system ensures data availability, resilience to failures, and performance benchmarking, providing functionalities such as replication,
 transaction handling, and dynamic node management.

### Key Features
- Client-Server Architecture: Multiple servers host the database, and clients interact with these servers to perform operations like PUT and GET.
- Replication: Data is replicated across multiple servers for fault tolerance and high availability.
- Heartbeat Monitoring: Periodic heartbeat messages between servers to ensure they are alive and responsive.
- Persistent Storage: Data is stored persistently in a JSON file, ensuring durability.
- Consistent Hashing: Efficient data distribution across servers using consistent hashing.
- Write-Ahead Log (WAL): Ensures durability and recovery from failures.
- Backup and Recovery: Periodic snapshots of the data are taken for backup purposes.
- Transaction Management: Supports ACID transactions for data consistency.
- Fault Tolerance: Handles failures and ensures data availability, even in case of replica failures.
- Dynamic Node Management: Supports adding or removing nodes dynamically.

---

## Prerequisites

To run the project, you need:
- Python 3.x
- Required Python libraries (will be installed via `requirements.txt`)

### Required Libraries:
```
pip install -r requirements.txt
```

---

## How To Run:

### Step 1: Start the Servers

Open three different terminals and execute the following commands for each terminal:

1. **Start Server 1** (Port 5001):
   ```bash
   python -m server.server.py --port 5001 --replicas 127.0.0.1:5000
   ```

2. **Start Server 2** (Port 5002):
   ```bash
   python -m server.server.py --port 5002 --replicas 127.0.0.1:5000
   ```

3. **Start Server 3** (Port 5000):
   ```bash
   python -m server.server.py --port 5000 --replicas 127.0.0.1:5001 127.0.0.1:5002
   ```

> **Note:** Ensure you are in the main directory when running the above commands.

### Step 2: Start the Client

In a new terminal window, run the following command to start the client:

```bash
python -m client.client.py
```

The client will connect to the running server, and you can interact with the database by issuing `PUT` and `GET` commands.

---

## Functionalities

This system implements the following key features:

### 1. Handling Asynchronous and Non-Blocking Calls
   - The system supports asynchronous, non-blocking calls for improved performance, ensuring that operations like `PUT` and `GET` do not block the execution of other commands.

### 2. Persistent Storage
   - Data is stored persistently using JSON files, and every change to the database is saved. This ensures the system can recover from failures or restarts.

### 3. Consistent Hashing
   - Data is distributed across servers using consistent hashing, which minimizes the movement of data when nodes are added or removed.

### 4. Write-Ahead Log (WAL)
   - Each operation is logged in a Write-Ahead Log for durability. This allows recovery of the system's state in case of a failure.

### 5. Server Logging
   - All server activities, such as requests, responses, and failures, are logged for transparency and debugging purposes.

### 6. Periodic Backup
   - The system takes periodic snapshots of the data, ensuring that backups are available to restore the system in case of failures.

### 7. Transaction Property (ACID)
   - The system supports transactions that ensure atomicity, consistency, isolation, and durability (ACID). Transactions can be prepared, committed, or rolled back.

### 8. Replica Creation and Handling
   - The system automatically creates replicas for data and ensures replication across multiple servers. If one replica fails, another replica is used to maintain data availability.

### 9. Handling Server Failures
   - If one replica goes down, the client is automatically redirected to another replica server. The system ensures the failure is handled gracefully without data loss.

---

## Key Design Concepts

### Client-Server Architecture
The system uses a traditional client-server model where clients connect to servers to execute operations. Multiple servers can be used to ensure redundancy and fault tolerance.

### Replication
Each piece of data is replicated across multiple servers. When a `PUT` operation is executed on one server, it is automatically propagated to its replicas.

### Transaction Handling
A basic transaction protocol is implemented using a `TransactionManager`. The system supports the basic operations of preparing, committing, and rolling back transactions.

### Fault Tolerance
The system handles failures gracefully:
- **Dynamic Node Addition and Removal**: Nodes can be added or removed dynamically, and the data distribution is updated accordingly.
- **Automatic Healing**: The system uses backup and WAL mechanisms to restore from failures, ensuring minimal downtime.

---

## Benchmarking

The system supports benchmarking to measure the performance of key operations like `PUT`, `GET`, and transactions. The latencies for these operations are measured and logged.

You can benchmark the system using the following:
- Latency for `PUT` and `GET` operations
- Transaction latencies (prepare, commit, rollback)
- Replication and failure recovery times

---

## Future Enhancements

- **Enhanced Replication Strategies**: Implementing quorum-based or eventual consistency replication strategies.
- **Advanced Transaction Protocols**: Support for more advanced consistency protocols like Paxos.
- **Self-Healing Mechanisms**: Implement machine learning-based predictive fault detection and automated healing.
- **Real-World Testing**: Testing the system in a real-world scenario with higher load and complex fault conditions.

---

## Troubleshooting

- **Error: Server not responding**: Check if all servers are running and connected correctly.
- **Replica Down**: If a replica server goes down, ensure other replicas are available and the system heals automatically.
- **Transaction Errors**: Ensure transactions are correctly formatted and that there are no conflicts in the transaction states.

---

## Contact

If you have any questions or need further assistance, feel free to contact us:
- **Garima Tripathi**: [Email](mailto:garimatripathi0778@gmail.com)
- **Bhavya Kothari**: [Email](mailto:bhvyakothari13@gmail.com)


