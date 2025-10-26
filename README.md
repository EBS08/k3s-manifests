# K3s Manifests for EBS Tower

This repository contains **Kubernetes manifests** for your Dell Tower single-node K3s setup.  
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

jenkins.local portainer.local grafana.local prometheus.local kibana.local

Replace `<DELL-IP>` with your Dell Tower IP.

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
	•	Jenkins: http://jenkins.local
	•	Portainer: http://portainer.local
	•	Grafana: http://grafana.local
	•	Default admin: admin
	•	Default password: admin123 (stored as secret)
	•	Prometheus: http://prometheus.local
	•	Kibana: http://kibana.local

All services run with replica:1 because this is a single-node cluster. Scale replicas safely after adding more nodes.

Future Considerations
	•	Scale replicas for high availability once multi-node cluster is ready.
	•	Backup /data/k8s/ regularly for persistent data.
	•	Add monitoring and alerting for Dell Tower resources.

⸻

Notes
	•	NodePort services can also be accessed directly via <DELL-IP>:<nodePort>.
	•	All PVs are mapped to /data/k8s/ for durability.
	•	Docker runtime is used for all containers in K3s.

---

If you want, the **next step** is I can **write all the YAML files in one ZIP-ready package**, fully ready for Git, with **updated replicas and comments**, so you just `git clone` and deploy everything on your Dell Tower.  

Do you want me to prepare that?