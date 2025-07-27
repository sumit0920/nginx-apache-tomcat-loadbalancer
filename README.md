# nginx-apache-tomcat-loadbalancer
This project demonstrates a real-world scenario where NGINX is configured as a reverse proxy and load balancer to distribute HTTP requests between Apache (serving static HTML) and Tomcat (serving dynamic Java WAR content). It ensures high availability and balanced traffic distribution in a microservices-based architecture.

---

# NGINX Load Balancer: Apache2 + Tomcat9 (Real-World DevOps + SysAdmin Project)

This project demonstrates how to configure **NGINX as a reverse proxy load balancer** to distribute traffic between **Apache2** (serving HTML) and **Tomcat9** (serving a Java WAR file) running on two separate backend servers.

---

## 🧩 Project Structure

```

nginx-apache-tomcat-loadbalancer/
├── nginx/
│   ├── nginx.conf
│   └── sites-available/webstack
├── apache/
│   └── index.html
├── tomcat/
│   └── index.html
├── README.md
└── diagram.png

````

---

## 🌐 Network Setup

| Component | Description | IP Address | Port |
|----------|-------------|------------|------|
| NGINX    | Load Balancer | nginx-lb.local | 80 |
| Apache2  | HTML Server   | apache.local | 8081 |
| Tomcat9  | Java WAR Server | tomcat.local | 8080 |

⚙️ These were the private IPs in my home lab. In production or cloud, DNS or dynamic service discovery would be used.

---

## 🔧 Configuration

### 🔹 NGINX

**File:** `sites-available/webstack`

```nginx
upstream backend {
    server apache.local:8081;
    server tomcat.local:8080;
}

server {
    listen 80;

    location / {
        proxy_pass http://backend;
    }
}
````

**Command to enable site and restart NGINX:**

```bash
sudo ln -s /etc/nginx/sites-available/webstack /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

---

## 📂 Sample Files

* `apache/index.html`: Simple HTML file served by Apache2.
* `tomcat/index.html`: A sample Java web application (WAR) deployed to Tomcat.

---

## 🔁 Expected Behavior

When you access the NGINX IP (e.g., `http://nginx-lb.local/`) in a browser and refresh multiple times:

* Requests alternate between **Apache2** and **Tomcat9**.
* Load is distributed in round-robin fashion.

---

## 🛠️ Skills Demonstrated

* System Administration (Apache, Tomcat, Networking)
* NGINX Reverse Proxy and Load Balancing
* Configuration Testing and Troubleshooting
* Real-World Infrastructure Deployment
* GitHub Project Structuring

---

## 📊 Diagram

![Architecture Diagram]
<img width="2002" height="1022" alt="Untitled Diagram drawio (1)" src="https://github.com/user-attachments/assets/ca6326e3-0698-47a2-a718-aaf972fd7f0d" />


---

## 📎 To-Do

* Add SSL support (HTTPS)
* Add health checks to NGINX upstream
* Deploy to cloud environment (AWS/GCP)
* Add logging and monitoring with Prometheus + Grafana

---

## 🚀 How to Run

1. Setup 3 VMs or containers with static IPs.
2. Configure Apache2 and Tomcat to serve test files.
3. Setup NGINX as described above.
4. Open browser → Hit NGINX IP → Refresh to test load balancing.

---

## 📌 Author

Sumit Sharma
System Administrator & Aspiring DevOps Engineer
🔗 [LinkedIn](https://www.linkedin.com/in/sumitsharma-ss/) | 🐙 [GitHub](https://github.com/sumit0920)

---

## 📜 License

MIT License – use freely, credit appreciated!

```




