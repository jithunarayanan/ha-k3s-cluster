# High Availability Kubernetes Cluster with K3S

This project sets up a **High Availability (HA) Kubernetes cluster** using K3S. The cluster spans across **two AWS Availability Zones (AZs)** to ensure redundancy and fault tolerance. It is designed to handle development and staging workloads.

## Architecture Overview

- **Cluster Configuration:**
  - 2 Master Nodes:
    - **Master Node 1:** Dedicated for cluster management and scheduling.
    - **Master Node 2:** Dedicated exclusively to hosting the embedded **etcd** datastore for higher data consistency and reliability.
  - 2 Worker Nodes:
    - Designed to handle application workloads and scaling operations.

- **Scalability:**
  - The cluster is designed with scalability in mind and can be scaled horizontally by adding more worker or master nodes as needed.

- **AWS Infrastructure:**
  - Spread across two Availability Zones to enhance resilience and reduce downtime risks.

- **Load Balancer:**
  - Optionally, a **load balancer** can be configured to expose the application. This needs to be manually configured as the alternative approach of using **NodePort** for application exposure is simpler but less flexible.

- **Autoscaling Group:**
  - The setup allows for the use of an **Autoscaling Group** configured with a pre-built Amazon Machine Image (AMI) to automate scaling and streamline infrastructure management.

## Prerequisites

- AWS Account with necessary permissions for EC2 and networking components.
- Installed tools:
  - [K3S](https://k3s.io/)
  - `kubectl` CLI
  - Terraform/Ansible (optional for infrastructure automation)
- Proper IAM Roles and Policies configured for cluster operations.

## Deployment Steps

1. **Provision Infrastructure:**
   - Set up the instances for master and worker nodes in two AWS Availability Zones.

2. **Install and Configure K3S:**
   - Install K3S on all nodes, ensuring one master node is dedicated to `etcd`.

3. **Cluster Setup:**
   - Initialize the cluster and join worker nodes.
   - Validate the setup using `kubectl get nodes`.

4. **Optional Load Balancer Configuration:**
   - Manually configure a load balancer to expose the application.
   - Alternatively, applications can be exposed using NodePort for a simpler approach.

5. **Optional Autoscaling Group:**
   - Configure an Autoscaling Group with a pre-built AMI for seamless scaling of resources.

6. **Scaling:**
   - Add additional master or worker nodes as the workload grows by following K3S scaling documentation.

## Future Enhancements

- Integrate monitoring and logging tools like **Prometheus** and **Grafana**.
- Implement automated scaling with Kubernetes **Horizontal Pod Autoscaler (HPA)**.
- Explore **rolling updates** and **canary deployments** for application changes.

---
