# Wisecow Application - Kubernetes Deployment Project

This project involves containerizing the Wisecow application and deploying it on Kubernetes with TLS security and CI/CD automation.

## Project Overview

**Wisecow** is a simple Bash-based web server that:
- Serves random wisdom quotes using `fortune`
- Displays them in ASCII art using `cowsay`
- Runs on port 4499 using `netcat`

## Current Progress - Phase 1: Development Environment Setup ✅

### Development VM Configuration

We've set up an Ubuntu 22.04 LTS virtual machine using Vagrant with all necessary tools pre-installed:

#### Tools Installed:
- **Application Dependencies**: `cowsay`, `fortune`, `netcat`
- **Containerization**: Docker Engine, Docker Compose
- **Orchestration**: Kubernetes CLI (`kubectl`), Minikube
- **Networking**: VirtualBox Host-Only Network

#### Quick Start - Development Environment

1. **Prerequisites**: Install Vagrant and VirtualBox on your host machine

2. **Start the VM**:
   ```bash
   vagrant up