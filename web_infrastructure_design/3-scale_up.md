## Differences Between Application Server and Web Server

1. **Web Server (Nginx in your setup):**
   - **Purpose:** Handles HTTP requests from clients, serves static content (HTML, CSS, JavaScript), and forwards dynamic requests to the application server.
   - **Role:** Acts as the first point of contact for client requests, efficiently managing traffic, performing load balancing, and handling SSL/TLS encryption.
   - **Benefits:** Optimizes performance for static content, manages secure connections, and protects the backend servers from direct exposure to the internet.

2. **Application Server:**
   - **Purpose:** Processes the business logic of applications, executes code, and interacts with the database server to generate dynamic content.
   - **Role:** Runs server-side scripts and manages the interaction between the application’s backend logic and the data stored in the database.
   - **Benefits:** Handles complex operations, ensures scalability by adding more instances, and separates application logic from the presentation layer.

## Proposed Infrastructure Changes

1. **Adding 1 Server:**
   - **Reason:** To improve load handling and redundancy, and provide each server component (Web, Application, and Database) with dedicated resources. This separation enhances performance and simplifies maintenance and scaling.

2. **Adding Another Load Balancer (HAProxy) to Form a Cluster:**
   - **Reason:** To create an HA (High Availability) environment with Active-Active or Active-Passive setup, ensuring that if one load balancer fails, traffic can still be managed without interruption.
   - **Configuration:** Active-Active setups distribute requests evenly between the two load balancers, improving performance. Active-Passive setups keep one load balancer on standby to take over in case of failure, enhancing reliability.

3. **Splitting Components onto Separate Servers:**
   - **Reason:** To enhance security, manageability, and performance by isolating different roles (web, application, and database) onto their own dedicated servers.
     - **Web Server:** Handles HTTP requests, SSL termination, and routes requests to the application server.
     - **Application Server:** Processes application logic, communicates with the database server, and returns dynamic content.
     - **Database Server:** Manages data storage and retrieval, with primary-replica configuration for improved read performance and redundancy.

## Infrastructure Specifics

1. **Additional Server:**
   - **Purpose:** To isolate and optimize specific tasks for the web, application, and database functions, ensuring that no single server is overloaded.

2. **Load Balancer Cluster (HAProxy):**
   - **Distribution Algorithm:** Common algorithms include Round Robin, Least Connections, and IP Hash. Each algorithm has distinct advantages:
     - **Round Robin:** Distributes requests evenly across all servers.
     - **Least Connections:** Sends traffic to the server with the fewest active connections, balancing load dynamically.
     - **IP Hash:** Directs requests from the same client to the same server, useful for maintaining session persistence.
   - **Setup Type:** Active-Active is preferred for load distribution, while Active-Passive is preferred for failover.

3. **Security Enhancements:**
   - **Firewalls:** Protect each server segment, restricting access and preventing unauthorized traffic.
   - **SSL Certificates:** Secure the connection between the client and the web server, ensuring encrypted communication.

