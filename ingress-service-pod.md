# 🔗 Connection Between Ingress, Service, and Pod

## 1. Pod

-   Smallest deployable unit in Kubernetes.
-   Runs your containerized application (e.g., Nginx, Python app, Java
    app).
-   Each Pod gets an **internal IP** but it's **ephemeral** (changes if
    the Pod restarts).

## 2. Service

-   Provides a **stable network endpoint** (ClusterIP, NodePort,
    LoadBalancer) for a set of Pods.
-   Uses **labels and selectors** to know **which Pods** it routes
    traffic to.
-   Handles **load balancing** across Pods.

## 3. Ingress

-   Acts as an **entry point** for external traffic (HTTP/HTTPS).
-   Uses an **Ingress Controller** (like NGINX ingress, Traefik, etc.).
-   Routes requests (based on **hostnames or paths**) to the appropriate
    **Service**.

------------------------------------------------------------------------

## ⚡ Flow

1.  User sends a request → `http://myapp.com/login`.
2.  **Ingress** receives the request and checks rules (e.g.,
    `/login → service-login`).
3.  **Service** forwards the traffic to one of the backend **Pods**
    running that app.
4.  The Pod processes the request and sends the response back through
    the same chain.

------------------------------------------------------------------------

## 📊 Diagram (Flow Chart)

       🌍 User (Browser / Client)
                 |
                 v
          ┌─────────────┐
          │   Ingress   │  (HTTP/HTTPS routing by host/path)
          └──────┬──────┘
                 |
                 v
          ┌─────────────┐
          │   Service   │  (Stable endpoint + load balancing)
          └──────┬──────┘
                 |
       ┌─────────┴─────────┐
       v                   v
    ┌───────┐          ┌───────┐
    │  Pod  │          │  Pod  │   (Your containers)
    │(App 1)│   ...    │(App 2)│
    └───────┘          └───────┘
