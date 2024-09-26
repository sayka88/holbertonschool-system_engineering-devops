# Web Infrastructure Detailed Explanation

## Additional Elements and Why They Are Added

1. **Firewalls**
   - **Purpose:** Firewalls are added to control incoming and outgoing network traffic based on predetermined security rules. They act as a barrier between trusted internal networks and untrusted external networks, such as the internet, protecting the infrastructure from unauthorized access, attacks, and data breaches.

2. **HTTPS (SSL/TLS)**
   - **Purpose:** Traffic is served over HTTPS to encrypt the data transmitted between the user's browser and the web server. This prevents eavesdropping, tampering, and man-in-the-middle attacks, ensuring data integrity and security. HTTPS is also essential for maintaining user trust and is often required for compliance with security standards.

3. **Monitoring Tools**
   - **Purpose:** Monitoring tools like Sumologic, Prometheus, or Nagios are used to track the performance, availability, and health of the infrastructure. They provide real-time alerts, logs, and metrics, enabling proactive identification and resolution of issues before they impact users.
   - **Data Collection:** Monitoring tools collect data by pulling logs, metrics, and events from servers, applications, and network devices. They may use agents installed on servers, API integrations, or direct log parsing to gather information about system performance, errors, and user activity.

4. **Monitoring Web Server QPS (Queries Per Second)**
   - **Explanation:** To monitor your web server's QPS, configure your monitoring tool to collect metrics specific to the HTTP requests handled by your web server. This can be achieved by:
     - Enabling access logging on the web server (e.g., Nginx, Apache).
     - Configuring the monitoring tool to parse these logs and extract metrics like request rates.
     - Setting up custom dashboards and alerts to track QPS and identify spikes or drops in traffic.

## Issues with This Infrastructure

1. **SSL Termination at the Load Balancer Level**
   - **Issue:** Terminating SSL at the load balancer means the traffic between the load balancer and backend servers (web servers, application servers) is unencrypted. This can expose sensitive data to potential interception if the internal network is compromised. To enhance security, end-to-end encryption should be maintained by re-encrypting traffic from the load balancer to the backend servers.

2. **Only One MySQL Server Capable of Accepting Writes**
   - **Issue:** Having a single MySQL server responsible for write operations creates a single point of failure. If the primary server goes down, the application cannot process any write requests, leading to potential data loss or downtime. Additionally, this setup limits scalability, as the single server may struggle to handle high write loads. Implementing a multi-primary setup or failover mechanisms can help mitigate this issue.

3. **Servers with All Components (Database, Web Server, Application Server)**
   - **Issue:** Hosting the web server, application server, and database on the same machine creates a tightly coupled architecture that lacks flexibility and scalability. If one component fails, it can take down the entire server, affecting all services. Resource contention can also become a problem, as the components compete for CPU, memory, and disk I/O, leading to performance degradation. Splitting these components onto dedicated servers or using containerization can improve reliability and performance.
