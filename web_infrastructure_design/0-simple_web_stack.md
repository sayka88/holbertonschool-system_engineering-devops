# Web Infrastructure Explanation

## 1. What is a Server?
A server is a physical or virtual machine that provides services, resources, or data to other computers, known as clients, over a network. It runs server software that listens for requests from clients and responds with the appropriate data or services.

## 2. What is the Role of the Domain Name?
The domain name (e.g., www.foobar.com) is a human-readable address that users type into their web browsers to access a website. It translates to an IP address through DNS (Domain Name System), which allows the web browser to locate and connect to the server hosting the website.

## 3. What Type of DNS Record is www in www.foobar.com?
The `www` subdomain in `www.foobar.com` is typically an A record or CNAME record.
- **A Record:** Points directly to the IP address of the server hosting the website (e.g., 8.8.8.8).
- **CNAME Record:** Points to another domain name that resolves to the IP address of the server.

## 4. What is the Role of the Web Server?
The web server (e.g., Nginx) handles HTTP requests from users. It serves static content like HTML, CSS, and JavaScript files and forwards requests for dynamic content to the application server. It also manages user sessions and handles other web-related tasks.

## 5. What is the Role of the Application Server?
The application server processes dynamic content by executing the application code. It handles requests that require interaction with the database and generates responses based on the logic defined in the application files. It communicates with the web server to send data back to the client.

## 6. What is the Role of the Database?
The database (e.g., MySQL) stores and manages data used by the application, such as user information, content, and configuration settings. The application server queries the database to retrieve or update data as needed to generate the requested content.

## 7. What is the Server Using to Communicate with the Computer of the User Requesting the Website?
The server communicates with the user's computer using HTTP (Hypertext Transfer Protocol) or HTTPS (HTTP Secure) over the internet. These protocols facilitate the exchange of data between the user's web browser and the server.

# Issues with This Infrastructure

## 1. Single Point of Failure (SPOF)
Since all components (web server, application server, and database) are hosted on a single server, if that server fails, the entire website becomes unavailable. There is no redundancy or failover mechanism in place to ensure continued availability.

## 2. Downtime When Maintenance is Needed
Performing maintenance, such as deploying new code or updating the server, requires restarting the web server or other components. This can lead to downtime or service interruptions for users, as the server will be temporarily unavailable.

## 3. Cannot Scale if Too Much Incoming Traffic
The single server setup has limited capacity to handle increased traffic. If the website experiences a surge in visitors, the server may become overloaded, leading to performance issues or crashes. Scaling requires additional servers or a more complex architecture to distribute the load and handle higher traffic volumes.
