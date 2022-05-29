# GCP_HTTP_Load_Balancer_with_Cloud_Armor

## Also you can refer [AWS-application-load-balancer-with-WAF](https://github.com/rushabhmahale/AWS-application-load-balancer-with-WAF)
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

# Steps to be followed :- 
## Step1 Configure Firewallrule for Loadbalancer 
- This is GCP Console  
![image](https://user-images.githubusercontent.com/63963025/170855956-f61e70e8-f1ed-4a25-93ea-84c4e1f36be2.png)
- In Left hand side there is Nevigation menu 
 ![image](https://user-images.githubusercontent.com/63963025/170855999-72a03d28-5df2-4c7a-a1bf-38ddd6aa356f.png)
- Go to VPC--> Firewall
![image](https://user-images.githubusercontent.com/63963025/170856085-b82f9ed5-08ef-4ca7-822e-abefb217a23a.png)
- Create Firewall Rule.
![image](https://user-images.githubusercontent.com/63963025/170856310-a4e4bf42-40bc-4032-979f-9598c21b9283.png)

- <b>Name</b>	http-traffic
- <b>Network</b>	default
- <b>Targets</b>	Specified target tags
- <b>Target tags</b>	http-server
- <b>Source filter</b>	IPv4 Ranges
- <b>Source IPv4 ranges</b>	0.0.0.0/0
- <b>Protocols and ports</b>	Specified protocols and ports, and then check tcp, type: 80
![image](https://user-images.githubusercontent.com/63963025/170856353-297dd930-9071-4031-a71d-2d22393e69af.png)
![image](https://user-images.githubusercontent.com/63963025/170856366-0827fc9f-3d20-45c6-b98f-2cbdbab55d37.png)

- Now Create another <b>Firewall Rule</b> 
- With this Configuration
- <b>Name</b>	healthcheck-lb
- <b>Network</b>	default
- <b>Targets</b>	Specified target tags
- <b>Target tags</b>	http-server
- <b>Source filter</b>	IPv4 Ranges
- <b>Source IPv4 ranges</b>	130.211.0.0/22, 35.191.0.0/16
- <b>Protocols and ports</b>	Specified protocols and ports, and then check tcp

![image](https://user-images.githubusercontent.com/63963025/170856475-2d3274e5-4b51-46b2-8333-475de8f44ff7.png)

## Step2 Configure instance templates and create instance groups
- Go to Naviagtion menu --> Compute Engine --> Instance templates  
![image](https://user-images.githubusercontent.com/63963025/170856545-7e379d61-bb88-4c85-87e8-d2f2e983822a.png)

- Create instance template
![image](https://user-images.githubusercontent.com/63963025/170856630-d000626e-da9c-4a29-b3d5-3f9d45ff10f1.png)

- Name, type us-east1-template.
- For Series, select N1.
- Click NETWORKING, DISKS, SECURITY, MANAGEMENT, SOLE-TENANCY. 
![image](https://user-images.githubusercontent.com/63963025/170856733-dc9c88be-8755-4d16-b14a-5fe3588b89d6.png)
- Click the Management tab
- Add metadata 
- <b>Key</b> startup-script-url
- <b>Value</b> gs://cloud-training/gcpnet/httplb/startup.sh

![image](https://user-images.githubusercontent.com/63963025/170856762-8158a719-0a67-41be-b95a-c189bbe5374d.png)

- Networking
- <b>Network tags</b>	http-server
- <b>Network</b>	default
- <b>Subnetwork</b>	default (us-east1)
![image](https://user-images.githubusercontent.com/63963025/170856895-522ebaa9-e9e8-4b03-9d15-7cd9ea77b270.png)

- Now copy the template and only change  network---> Subnetwork--> default (europe-west1) --> create 
 ![image](https://user-images.githubusercontent.com/63963025/170856959-e6f08959-9b7d-468c-af15-7edafe7d9cd2.png)

- <b>Name</b>europe-west1-template.
![image](https://user-images.githubusercontent.com/63963025/170857043-25435420-1a2d-486c-bb99-9bbb64f2b331.png)

![image](https://user-images.githubusercontent.com/63963025/170857054-71d8be96-a578-485f-aa4e-ef0ce47978da.png)

## Lets Create the managed instance groups
- Navigation Menu--> Compute Engine--> Instance grooups
![image](https://user-images.githubusercontent.com/63963025/170857103-70f851cc-9a9a-4067-909c-f7d709f966b1.png)
- Create Instance groups
![image](https://user-images.githubusercontent.com/63963025/170857234-e91264fc-bbf9-4155-b788-b8669dfe283a.png)

- Name	us-east1-mig
- Location	Multiple zones
- Region	us-east1
- Instance template	us-east1-template
- Autoscaling > Autoscaling metrics > Click dropdown > Metric type	CPU utilization
- Target CPU utilization	80, click Done.
- Cool-down period	45
- Minimum number of instances	1
- Maximum number of instances	5

![image](https://user-images.githubusercontent.com/63963025/170857258-4f813b6b-610e-41fb-9ea4-bea6a9a82e89.png)
![image](https://user-images.githubusercontent.com/63963025/170857278-8499cdce-9a34-44ae-9843-2ff124e0e8d0.png)
![image](https://user-images.githubusercontent.com/63963025/170857297-42a2eef0-88ac-4a4f-8d5e-58cb6aad8936.png)

- Create another MIG(Manage instance Group)
- Name	europe-west1-mig
- Location	Multiple zones
- Region	europe-west1
- Instance template	europe-west1-template
- Autoscaling > Autoscaling metrics > Click dropdown > Metric type	CPU utilization
- Target CPU utilization	80, click Done.
- Cool-down period	45 
- Minimum number of instances	1
- Maximum number of instances	5
![image](https://user-images.githubusercontent.com/63963025/170857376-5bef16dd-d444-4b4e-880e-834fcfd1e467.png)
![image](https://user-images.githubusercontent.com/63963025/170857389-0da57b40-5426-43bd-a9dc-f0e4042402ca.png)
![image](https://user-images.githubusercontent.com/63963025/170857410-3ce0cc3d-aa61-4def-a861-0249cc24944b.png)






