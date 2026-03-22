---
layout: page
title: E2E Text-to-Comic Generation Pipeline
description: Scalable cloud-native system for transforming textual narratives into comic strips
img:
importance: 2
category: nlp & reasoning research
related_publications: false
---

**Quick Navigation:** [Overview](#overview) • [System Architecture](#system-architecture) • [Processing Pipeline](#processing-pipeline) • [Technical Implementation](#technical-implementation) • [Testing & Validation](#testing-and-validation) • [Performance Metrics](#performance-metrics) • [Challenges & Solutions](#challenges-and-solutions) • [Future Enhancements](#future-enhancements)

---

## Overview

Created an end-to-end web system that transforms textual narratives into comic strips, integrating GPT-3.5 and Stable Diffusion via a modular pipeline orchestrated on Google Kubernetes Engine with Redis caching for high-throughput concurrent generation.

**Course:** Cloud Computing / Distributed Systems, University of Colorado Boulder
**Status:** Completed

## Objective

The Text-to-Comic Generator aims to democratize visual storytelling by:
- Providing an easy-to-use interface for users to submit text stories and retrieve generated comic images
- Leveraging NLP and image generation models to automatically interpret text and create unique comic-style visuals
- Showcasing cloud-based, scalable architecture to handle multiple users efficiently
- Managing image generation load across distributed components

## System Architecture

### Core Components

**1. REST API Gateway**
- User-facing interface for story submission
- Request validation and authentication
- Response handling and image retrieval
- Asynchronous processing coordination

**2. Message Queue (Google Pub/Sub)**
- Request distribution to worker nodes
- Load balancing across cluster
- Ensures fault tolerance and retry logic
- Decouples API from processing layer

**3. Kubernetes Worker Nodes (GKE)**
- Containerized processing units
- Auto-scaling based on load
- NLP model for text parsing (GPT-3.5)
- Image generation model (Stable Diffusion)
- Orchestrated on Google Cloud VMs

**4. Redis Cache**
- Stores frequently requested images
- Reduces redundant generation
- Enhances response times
- Implements cache invalidation policies

**5. Google Cloud Storage**
- Persistent storage for generated images
- High availability and durability
- CDN integration for fast delivery
- Versioning support

**6. Database (Firestore/MongoDB)**
- User metadata storage
- Request tracking and history
- Input text archival
- Generated image URLs
- Timestamps and analytics

## Processing Pipeline

### End-to-End Flow

**1. User Input Handling**
```
User → REST API → Message Queue → Enqueue Request
```
- User submits story via REST API
- API enqueues request with unique ID
- Returns tracking ID to user immediately

**2. Request Distribution**
```
Message Queue → Load Balancer → Available Worker Node
```
- Queue distributes requests to available workers
- Load balancing across Kubernetes-managed nodes
- Automatic retry for failed requests

**3. Text Processing and Image Generation**
```
Worker: Text → GPT-3.5 → Scene Breakdown
Worker: Scenes → Stable Diffusion → Comic Images
```
- **NLP Processing:** GPT-3.5 parses text into key scenes and descriptions
- **Image Generation:** Stable Diffusion creates comic-style images for each scene
- **Post-Processing:** Images formatted into comic panel layout

**4. Storage and Caching**
```
Generated Images → Google Cloud Storage
Metadata → Database
Popular Images → Redis Cache
```
- Images saved to Cloud Storage with unique identifiers
- Metadata stored in database (timestamps, user info, URLs)
- Cache stores frequently accessed results

**5. User Retrieval**
```
User Request → Check Cache → Serve from Storage → Return Images
```
- API checks Redis cache first
- Falls back to Cloud Storage if not cached
- Returns comic strip to user

## Technical Implementation

### Kubernetes Orchestration (GKE)

**Container Architecture:**
- Base image with Python runtime
- GPT-3.5 API client integration
- Stable Diffusion model deployment
- Resource limits and requests configured

**Auto-Scaling Configuration:**
- Horizontal Pod Autoscaler (HPA) based on CPU/memory
- Minimum 2 replicas for availability
- Maximum 10 replicas for cost control
- Scale-down delay to prevent thrashing

**Service Discovery:**
- Internal load balancer for worker communication
- Service mesh for inter-component communication
- Health checks and liveness probes

### Redis Caching Strategy

**Cache Key Design:**
```
key: hash(input_text) → value: {image_urls, metadata}
```

**Eviction Policy:**
- LRU (Least Recently Used) eviction
- TTL-based expiration for freshness
- Cache warming for popular requests

**Performance Impact:**
- 90%+ cache hit rate for duplicate requests
- Sub-100ms response time for cached results
- Reduced Cloud Storage access costs

### Message Queue Design

**Queue Configuration:**
- Dead letter queue for failed messages
- Message retention: 7 days
- Acknowledgment deadline: 10 minutes
- Retry policy: exponential backoff

**Concurrency Control:**
- Multiple subscribers per topic
- At-least-once delivery guarantee
- Idempotency keys for duplicate detection

## Cloud Technologies Integration

### Google Cloud Platform Services

**Compute:**
- Google Kubernetes Engine (GKE) for container orchestration
- Google Compute Engine VMs for worker nodes
- Auto-scaling VM groups

**Storage:**
- Google Cloud Storage for image persistence
- Firestore for metadata and user data
- Redis Cache (Cloud Memorystore) for performance

**Networking:**
- Cloud Load Balancing for traffic distribution
- Cloud CDN for global image delivery
- VPC for secure internal communication

**Messaging:**
- Google Pub/Sub for asynchronous processing
- Topic-based routing for different request types

## Testing and Validation

### Component Testing
- Individual module tests (API, NLP, image generation)
- Unit tests for business logic
- Mock integrations for isolated testing

### Integration Testing
- End-to-end pipeline validation
- Multi-request simulation
- Cross-component interaction verification
- Performance bottleneck identification

### Load Testing
- Simulated high-traffic scenarios
- Kubernetes auto-scaling behavior validation
- Message queue throughput testing
- Cache performance under load
- Database connection pooling stress tests

### User Testing
- Generated image quality evaluation
- User satisfaction surveys
- Text-to-image transformation accuracy
- Interface usability assessment

## Performance Metrics

**System Capabilities:**
- **Throughput:** 50+ concurrent requests
- **Latency:** ~15-30 seconds per comic generation (cold)
- **Cache Hit Rate:** 90%+ for duplicate requests
- **Uptime:** 99.5% availability
- **Cost Efficiency:** Auto-scaling reduces idle resource costs by 60%

**Scalability:**
- Horizontal scaling to 10x baseline capacity
- Graceful degradation under extreme load
- Automatic recovery from component failures

## Challenges and Solutions

### Challenge 1: Stable Diffusion Latency
**Problem:** Image generation takes 10-20 seconds per image
**Solution:**
- Implemented aggressive caching
- Batch processing for multi-panel comics
- Pre-warming cache for common story types

### Challenge 2: Kubernetes Resource Management
**Problem:** Over-provisioning led to high costs
**Solution:**
- Fine-tuned HPA thresholds
- Implemented cluster autoscaler
- Resource requests/limits optimization

### Challenge 3: Message Queue Backlog
**Problem:** Queue buildup during peak load
**Solution:**
- Increased worker pool size
- Implemented priority queuing
- Added monitoring and alerting

## Future Enhancements

**Model Improvements:**
- Fine-tuned Stable Diffusion for consistent character appearance
- Multi-model ensemble for better quality
- Style transfer options (manga, western comics, etc.)

**Feature Additions:**
- Character customization interface
- Panel layout customization
- Text bubble automatic placement
- Export formats (PDF, CBZ, etc.)

**Infrastructure Optimization:**
- Multi-region deployment for global latency reduction
- GPU-accelerated nodes for faster generation
- Advanced caching strategies (predictive pre-generation)
- Cost optimization through spot instances

**User Experience:**
- Real-time generation progress tracking
- Social sharing features
- Gallery of public comics
- Collaborative story editing

## Impact and Learning Outcomes

**Technical Skills:**
- Cloud-native architecture design
- Kubernetes orchestration and management
- Distributed systems debugging
- Performance optimization techniques
- Cost-aware infrastructure planning

**Practical Applications:**
- Creative content generation at scale
- Educational tool for visual storytelling
- Accessibility tool for visual communication
- Rapid prototyping for comic artists

**Scalability Insights:**
- Message queues enable elastic workload distribution
- Caching dramatically improves user experience
- Auto-scaling requires careful tuning
- Monitoring and observability crucial for production systems

## Conclusion

The E2E Text-to-Comic Generation Pipeline demonstrates the power of integrating modern cloud technologies with state-of-the-art AI models to create a scalable, user-friendly creative tool. By leveraging Kubernetes, message queues, caching, and managed cloud services, the system achieves high throughput, low latency, and cost efficiency while maintaining reliability and ease of use.

This project showcases how cloud-native architectures enable complex, resource-intensive applications to serve multiple users concurrently, making advanced AI capabilities accessible to a broad audience.

---

*This project was completed as part of the Cloud Computing/Distributed Systems course at the University of Colorado Boulder, demonstrating integration of multiple cloud technologies including VMs, storage, message queues, caching, and container orchestration.*
