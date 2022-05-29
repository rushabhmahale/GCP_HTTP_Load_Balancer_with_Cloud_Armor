# GCP_HTTP_Load_Balancer_with_Cloud_Armor

## Why loadbalacer is necessary
Elastic Load Balancing automatically distributes your incoming traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more Availability Zones. It monitors the health of its registered targets, and routes traffic only to the healthy targets. Elastic Load Balancing scales your load balancer as your incoming traffic changes over time. It can automatically scale to the vast majority of workloads.

Reffer this doc:- https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/
![lb for gcp](https://user-images.githubusercontent.com/63963025/170854578-d6f78da3-031d-4a98-9118-6fc386ae3b90.gif)

## Types of loadbalancer in GCP
- Global external HTTP(S) load balancer
- Regional external HTTP(S) load balancer
- Internal HTTP(S) load balancer
- SSL proxy load balancer
- TCP proxy load balancer	
- External TCP/UDP Network load balancer
- Internal TCP/UDP load balancer

## Global external HTTP(S) load balancer
External HTTP(S) Load Balancing is a proxy-based Layer 7 load balancer that enables you to run and scale your services behind a single external IP address. External HTTP(S) Load Balancing distributes HTTP and HTTPS traffic to backends hosted on a variety of Google Cloud platforms (such as Compute Engine, Google Kubernetes Engine (GKE), Cloud Storage, and so on), as well as external backends connected over the internet or via hybrid connectivity. For details, see Use cases.

Reffer this doc:- https://cloud.google.com/load-balancing/docs/https
## Regional external HTTP(S) load balancer
This load balancer contains many of the features of the existing global external HTTP(S) load balancer (classic), along with advanced traffic management capabilities.
Use this load balancer if you want to serve content from only one geolocation (for example, to meet compliance regulations) or if the Standard Network Service Tier is desired.

Reffer this doc:- https://cloud.google.com/load-balancing/docs/https

## Internal HTTP(S) load balancer
Google Cloud Internal HTTP(S) Load Balancing is a proxy-based, regional Layer 7 load balancer that enables you to run and scale your services behind an internal IP address.Internal HTTP(S) Load Balancing distributes HTTP and HTTPS traffic to backends hosted on Compute Engine, Google Kubernetes Engine (GKE), and Cloud Run. The load balancer is accessible only in the chosen region of your Virtual Private Cloud (VPC) network on an internal IP address.

Reffer this doc:- https://cloud.google.com/load-balancing/docs/l7-internal
## SSL proxy load balancer
SSL Proxy Load Balancing is a reverse proxy load balancer that distributes SSL traffic coming from the internet to virtual machine (VM) instances in your Google Cloud VPC network. When using SSL Proxy Load Balancing for your SSL traffic, user SSL (TLS) connections are terminated at the load balancing layer, and then proxied to the closest available backend instances by using either SSL (recommended) or TCP. For the types of backends that are supported, see Backends.


Reffer this doc:- https://cloud.google.com/load-balancing/docs/ssl

## TCP proxy load balancer	
TCP Proxy Load Balancing is a reverse proxy load balancer that distributes TCP traffic coming from the internet to virtual machine (VM) instances in your Google Cloud VPC network. When using TCP Proxy Load Balancing, traffic coming over a TCP connection is terminated at the load balancing layer, and then forwarded to the closest available backend using TCP or SSL. TCP Proxy Load Balancing lets you use a single IP address for all users worldwide. The TCP proxy load balancer automatically routes traffic to the backends that are closest to the user.

Reffer this doc:- https://cloud.google.com/load-balancing/docs/tcp

## External TCP/UDP Network load balancer
Google Cloud external TCP/UDP Network Load Balancing (after this referred to as Network Load Balancing) is a regional, pass-through load balancer. A network load balancer distributes external traffic among virtual machine (VM) instances in the same region. You can configure a network load balancer for TCP, UDP, ESP, ICMP, and ICMPv6 traffic.

Reffer this doc:- https://cloud.google.com/load-balancing/docs/network

## Internal TCP/UDP load balancer
Internal TCP/UDP Load Balancing distributes traffic among internal virtual machine (VM) instances in the same region in a Virtual Private Cloud (VPC) network. It enables you to run and scale your services behind an internal IP address that is accessible only to systems in the same VPC network or systems connected to your VPC network.

Reffer this doc:- https://cloud.google.com/load-balancing/docs/internal

