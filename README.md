Hybrid Cloud Security Lab
Overview

This repository documents the design and implementation of a structured hybrid homelab built to simulate enterprise infrastructure while developing toward cloud security roles.

The lab is built on Proxmox Virtual Environment and integrates virtualization, segmented networking, containerized workloads, and centralized logging to create a realistic hands-on environment for infrastructure and security development.

This project serves as a living lab to bridge certification knowledge with applied architecture and operational experience.

Objectives:

o Develop hands-on experience with virtualization and hypervisors

o Implement VLAN-based network segmentation

o Deploy Windows and Linux server environments

o Implement centralized logging and monitoring

o Deploy and manage Docker-based container workloads

o Practice identity and access management concepts

o Document architectural decisions and lessons learned

High-Level Architecture

Core Components:

o Proxmox hypervisor (x86 host)

o Managed switch with VLAN support

o Ubuntu Server virtual machines

o Windows Server virtual machines

o Docker container host VM

o Raspberry Pi nodes for infrastructure services

o Centralized logging and monitoring stack


Network Design

Planned segmentation model:

o Management Network

o Server Network

o Client Network

o Test / Attack Network

o VLAN configuration and IP schema will be documented as the lab evolves.

o Virtual Machine Layout (Phase 1)

o Ubuntu Server (Infrastructure Node)

o Windows Server (Identity / Domain Services)

o Docker Host VM

o Security Monitoring VM (planned)

o Resource allocation and configuration details will be documented in subsequent updates.

o Container Deployment Strategy

o Containers are deployed within a dedicated Ubuntu Server VM using Docker and Docker Compose.

Planned workloads:

o Nginx reverse proxy

o Web application containers

o Database containers

o Security tooling containers

o Container networking, persistent volumes, and logging integration will be documented.

o Security Focus Areas

o Network segmentation

o Identity management

o Logging and monitoring

o Service isolation

o Attack simulation within controlled environments

o Infrastructure hardening

o Future Expansion

o Cloud integration (Azure/AWS)

o Hybrid identity configuration

o Infrastructure as Code

o Container image security scanning

o Edge compute branch (DDIL-focused experimentation)

Public data ingestion services

Lessons Learned

This section will capture implementation challenges, architectural decisions, and improvements over time.

Status

Phase 0: Repository and architecture planning
Phase 1: Hypervisor deployment and base VM configuration
Phase 2: Network segmentation and identity services
Phase 3: Container deployment and logging integration
