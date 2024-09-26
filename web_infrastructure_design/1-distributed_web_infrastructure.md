# Infrastructure Explanation

## 1. Additional Elements and Their Purposes

### Load-Balancer (HAproxy)
- **Purpose:** Distributes incoming traffic evenly between the two web servers to ensure that no single server is overwhelmed. This improves availability and performance.

### Two Servers
- **Purpose:** Each server handles web serving, application processing, and application files, providing redundancy and load distribution. If one server fails, the other can still handle traffic.

### Database (MySQL)
- **Purpose:** Centralized storage for application data. This allows both servers to access and manipulate data in a consistent manner.

# 2. My Load-Balancer Distribution uses a Round robin Algorithm

### Common Algorithms:
- **Round Robin:** Distributes requests sequentially across the available servers.

### How It Works:
- **Round Robin Example:** If Server 1 and Server 2 are both available, the load balancer will first route traffic to Server 1, then Server 2, and repeat the cycle. This balances the load evenly but does not account for server load or capacity.

# I configured HAproxy as an active-active setup

## 3. Load-Balancer Setup: Active-Active vs. Active-Passive

### Active-Active Setup:
- **Description:** All servers are actively handling traffic. The load balancer distributes incoming requests across all active servers.
- **Advantages:** Maximizes resource utilization and improves fault tolerance. If one server fails, the remaining servers continue to handle traffic.

### Active-Passive Setup:
- **Description:** Only one server is actively handling traffic while the other server(s) remain idle or on standby. The load balancer routes traffic only to the active server.
- **Advantages:** Simplifies configuration but can lead to inefficiencies as the passive server is not utilized. In case of failure, traffic is routed to the passive server.

## 4. Database Primary-Replica (Master-Slave) Cluster

### Primary Node (Master):
- **Role:** Handles all write operations (inserts, updates, deletes) and serves as the main source of data. It is the authoritative source of truth for the database.

### Replica Node (Slave):
- **Role:** Copies the data from the primary node and handles read operations (queries). It provides load balancing for read queries and enhances data redundancy.

### How It Works:
- **Replication:** The primary node periodically sends updates to the replica nodes. Replicas apply these updates to their data stores to stay synchronized with the primary.

## 5. Differences Between Primary and Replica Nodes

### Primary Node:
- **Writes:** Handles all write operations.
- **Reads:** Can handle read operations but typically dedicated to write operations.

### Replica Node:
- **Writes:** Cannot handle write operations (only reads).
- **Reads:** Can handle read operations and distribute query loads to improve performance.

## 6. Issues with This Infrastructure

### Single Points of Failure (SPOF):
- **Database (MySQL):** If the database server fails, the entire application loses access to data.
- **Load-Balancer (HAproxy):** If the load balancer fails, incoming traffic cannot be distributed to the servers.

### Security Issues:
- **No Firewall:** Without a firewall, the infrastructure is exposed to potential attacks from external sources.
- **No HTTPS:** Data transmitted between users and the web servers is not encrypted, making it vulnerable to interception and tampering.

### No Monitoring:
- **Lack of Visibility:** Without monitoring, you cannot track server performance, detect failures, or identify potential issues before they affect users.
- **Proactive Maintenance:** Monitoring tools help in proactive maintenance by providing alerts and insights into system health and performance.
