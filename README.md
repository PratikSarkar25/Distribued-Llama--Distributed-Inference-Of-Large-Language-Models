# Distributed Llama: Distributed Inference of Large Language Models

## Overview

Distributed Llama is a distributed inference framework that enables Large Language Models (LLMs) to run across multiple devices by partitioning model computation and synchronizing intermediate activations over a network.

The project explores efficient utilization of low-resource hardware for large-scale language model inference through distributed computing, quantization, and network-aware synchronization.

## Features

* Distributed LLM inference across multiple devices
* Horizontal model partitioning architecture
* Weight quantization support
* Memory-efficient execution
* Multi-node synchronization over Ethernet
* API server for inference requests
* Scalable deployment architecture
* Performance benchmarking and analysis

---

## System Architecture

```text
[SWITCH / ROUTER]
      | | | |
      | | | |_______ Device 1 (ROOT)
      | | |_________ Device 2 (WORKER 1)
      | |___________ Device 3 (WORKER 2)
      |_____________ Device 4 (WORKER 3)
```

The root node coordinates inference requests, while worker nodes process assigned model partitions and synchronize activations during token generation.

---

## Tech Stack

* C++
* Python
* Distributed Computing
* Ethernet Communication
* Quantized Large Language Models
* Linux / macOS / Windows

---

## Project Structure

```text
distributed-llama/
│
├── models/
├── src/
├── api/
├── docs/
├── scripts/
├── launch.py
├── Makefile
└── README.md
```

---

## Installation

### Linux

```bash
sudo apt install git build-essential
```

### macOS

```bash
brew install git
```

### Windows

Install Git and MinGW using Chocolatey:

```powershell
choco install git mingw
```

---

## Building the Project

Clone the repository and compile on all devices:

```bash
git clone <your-repository-url>
cd distributed-llama

make dllama
make dllama-api
```

---

## Downloading a Model

On the ROOT device:

```bash
python3 launch.py
```

Displays available models.

Download a model:

```bash
python3 launch.py llama3_2_3b_instruct_q40
```

---

## Starting Worker Nodes

Run on every worker machine:

```bash
./dllama worker --port 9999 --nthreads 4
```

---

## Running Distributed Inference

Execute on the ROOT device:

```bash
./dllama inference \
  --prompt "Hello world" \
  --steps 32 \
  --model models/llama3_2_3b_instruct_q40/dllama_model_llama3_2_3b_instruct_q40.m \
  --tokenizer models/llama3_2_3b_instruct_q40/dllama_tokenizer_llama3_2_3b_instruct_q40.t \
  --buffer-float-type q80 \
  --nthreads 4 \
  --max-seq-len 4096 \
  --workers 10.0.0.2:9999 10.0.0.3:9999 10.0.0.4:9999
```

---

## Running the API Server

Start the API server on the ROOT device:

```bash
./dllama-api \
  --port 9999 \
  --model models/llama3_2_3b_instruct_q40/dllama_model_llama3_2_3b_instruct_q40.m \
  --tokenizer models/llama3_2_3b_instruct_q40/dllama_tokenizer_llama3_2_3b_instruct_q40.t \
  --buffer-float-type q80 \
  --nthreads 4 \
  --max-seq-len 4096 \
  --workers 10.0.0.2:9999 10.0.0.3:9999 10.0.0.4:9999
```

Access the API:

```text
http://10.0.0.1:9999/v1/models
```

---

## Applications

* Distributed AI Systems
* Large Language Model Deployment
* Edge AI
* Model Parallelism Research
* Resource-Constrained Inference
* High-Performance Computing

---

## Key Concepts Explored

### Distributed Inference

Inference computation is divided among multiple machines, enabling larger models to run with limited memory resources.

### Quantization

Model weights and synchronization buffers are quantized to reduce memory consumption and network overhead.

### Synchronization

Devices exchange intermediate activations to maintain consistency during token generation.

### Scalability

The architecture demonstrates how additional devices can improve inference throughput while highlighting communication bottlenecks.

---

## Learning Outcomes

Through this project, I gained practical experience in:

* Large Language Model Architecture
* Distributed Systems
* Network Communication
* Model Parallelism
* Quantization Techniques
* Performance Optimization
* High-Performance Computing
* Distributed AI Infrastructure

---

## Future Enhancements

* GPU Acceleration
* Kubernetes Deployment
* Dynamic Load Balancing
* Monitoring and Observability
* Multi-Region Deployment
* Faster Communication Protocols
* Support for Newer Foundation Models

---

## Author

Pratik Sarkar

M.Sc. Data Science & Artificial Intelligence

Ramakrishna Mission Vivekananda Educational and Research Institute (RKMVERI)

---

## License

This project is intended for educational, research, and learning purposes.
