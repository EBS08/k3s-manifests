# K3s Manifests for EBS Tower

This repository contains **Kubernetes manifests** for your Server single-node K3s setup.  
It includes **persistent volumes, deployments, services, monitoring stack, and ingress**.

---

## **Requirements**

- Ubuntu 24.04 LTS
- K3s installed
- Docker runtime enabled in K3s
- `/data/k8s/` folder prepared for persistent volumes
- Traefik ingress installed (default in K3s)
- Git installed (optional)

---

##  📁  **Repository Structure**

```bash
k3s-manifests/
├── README.md
├── namespaces/
├── pv-pvcs/
├── deployments/
├── services/
├── ingress/
└── configmaps-secrets/

---

## **Persistent Volume Paths**

- PostgreSQL: `/data/k8s/postgres`
- MongoDB: `/data/k8s/mongodb`
- Jenkins: `/data/k8s/jenkins`
- Portainer: `/data/k8s/portainer`
- Prometheus: `/data/k8s/prometheus`
- Grafana: `/data/k8s/grafana`
- Elasticsearch: `/data/k8s/elasticsearch`
- Kibana: `/data/k8s/kibana`

---

## **Hosts Configuration**

Add these to `/etc/hosts` on your machine for ingress:

jenkins.ebs.corp portainer.ebs.corp grafana.ebs.monitor.corp prometheus.ebs.monitor.corp kibana.ebs.monitor.corp

Replace `<SERVER-IP>` with your Server IP.

---

## **Deployment Steps**

```bash
1. Apply namespace:
kubectl apply -f namespaces/

2.	Apply persistent volumes and claims:
kubectl apply -f pv-pvcs/

3.	Apply ConfigMaps and Secrets:
kubectl apply -f configmaps-secrets/

4.	Deploy applications:
kubectl apply -f deployments/

5.	Expose applications via NodePort:
kubectl apply -f services/

6.	Setup ingress:
kubectl apply -f ingress/

Access Applications
	•	Jenkins: http://jenkins.ebs.corp
	•	Portainer: http://portainer.ebs.corp
	•	Grafana: http://grafana.ebs.monitor.corp
	•	Default admin: admin
	•	Default password: admin123 (stored as secret)
	•	Prometheus: http://prometheus.ebs.monitor.corp
	•	Kibana: http://kibana.ebs.monitor.corp

All services run with replica:1 because this is a single-node cluster. Scale replicas safely after adding more nodes.

Future Considerations
	•	Scale replicas for high availability once multi-node cluster is ready.
	•	Backup /data/k8s/ regularly for persistent data.
	•	Add monitoring and alerting for Server resources.

⸻

Notes
	•	NodePort services can also be accessed directly via <SERVER-IP>:<nodePort>.
	•	All PVs are mapped to /data/k8s/ for durability.
	•	Docker runtime is used for all containers in K3s.

---