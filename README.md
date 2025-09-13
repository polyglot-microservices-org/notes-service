# 📝 Notes Service

> **Note management API built with Python Flask and MongoDB**

## 📋 Overview

Python Flask microservice for note-taking with CRUD operations, MongoDB persistence, and microservices integration.

## 🏗️ Architecture

- **Language**: Python 3.9+ with Flask
- **Database**: MongoDB with connection retry
- **Port**: 5002
- **Health Check**: `/healthz`
- **Docker Image**: `yaswanthmitta/multiapp-notes-app`

## 🚀 API Documentation

### Base URL
```
http://localhost:5002
```

### Endpoints

#### Create Note
**POST** `/notes`

Create a new note with title and content.

**Request Body:**
```json
{
  "title": "Meeting Notes",
  "content": "Discussed project timeline and deliverables. Next meeting scheduled for Friday."
}
```

**Response:**
```json
{
  "message": "Note created successfully",
  "id": "507f1f77bcf86cd799439011",
  "title": "Meeting Notes",
  "content": "Discussed project timeline and deliverables. Next meeting scheduled for Friday."
}
```

#### Get All Notes
**GET** `/notes`

Retrieve all notes.

**Response:**
```json
[
  {
    "_id": "507f1f77bcf86cd799439011",
    "title": "Meeting Notes",
    "content": "Discussed project timeline and deliverables. Next meeting scheduled for Friday."
  },
  {
    "_id": "507f1f77bcf86cd799439012",
    "title": "Project Ideas",
    "content": "1. Implement user authentication\n2. Add real-time notifications\n3. Create mobile app"
  }
]
```

#### Get Note by ID
**GET** `/notes/{id}`

Retrieve a specific note by ID.

**Response:**
```json
{
  "_id": "507f1f77bcf86cd799439011",
  "title": "Meeting Notes",
  "content": "Discussed project timeline and deliverables. Next meeting scheduled for Friday."
}
```

#### Update Note
**PUT** `/notes/{id}`

Update an existing note (title and/or content).

**Request Body:**
```json
{
  "title": "Updated Meeting Notes",
  "content": "Discussed project timeline, deliverables, and budget. Next meeting scheduled for Friday at 2 PM."
}
```

**Response:**
```json
{
  "message": "Note updated successfully"
}
```

#### Delete Note
**DELETE** `/notes/{id}`

Delete a note by ID.

**Response:**
```json
{
  "message": "Note deleted successfully"
}
```

#### Health Check
**GET** `/healthz`

Service health status.

**Response:**
```json
{
  "status": "ok"
}
```

### Error Responses
```json
{
  "error": "Note not found"
}
```

## 🔧 Configuration

**Environment**: `MONGO_URI=mongodb://notes-db:27017/`, `DB_NAME=notes_db`

**Database**: MongoDB with 10-retry connection logic and automatic reconnection

## 🐳 Docker

**Multi-stage build**: Python 3.9-slim base image

**Security**: Non-root user (ID 1000), minimal dependencies

**Health checks**: Built-in container monitoring on `/healthz`

**Optimization**: Layer caching, .dockerignore for faster builds

## ☸️ Kubernetes

**Deployment**: Flask app with rolling updates and replica management

**StatefulSet**: MongoDB with persistent storage (1Gi PVC)

**Services**: ClusterIP for internal communication

**HPA**: Auto-scaling based on CPU/memory thresholds

**Probes**: Liveness, readiness, and startup health checks

**Resources**: CPU/memory limits and requests configured

## 🔄 CI/CD Pipeline

**CI Tests**: Linting (flake8), Code analysis, SCA (safety), SAST (bandit), Build validation, Unit tests

**CI Flow**: GitHub runners → Docker build with Git SHA → Push to registry → Update K8s manifests

**CD Flow**: Self-hosted runners → Rolling updates → DAST health checks → Auto rollback

**Image Tagging**: `yaswanthmitta/multiapp-notes-app:<git-sha>`

## 🔒 Security

**Application**: Input validation, ObjectId validation, secure error handling

**Container**: Non-root user, minimal base image, resource limits

**Database**: Network isolation, encrypted PVC storage, authenticated connections

## 📊 Monitoring

**Metrics**: Request rate, response time, error rate, database performance

**Health Checks**: Liveness, readiness, and startup probes

**Integration**: Prometheus metrics collection and Grafana dashboards

## 🧪 Testing

**Unit Tests**: Flask test client for API endpoints

**Integration Tests**: Local MongoDB with curl testing

**Load Testing**: Apache Bench for performance validation

## 🚨 Troubleshooting

**Common Issues**: MongoDB connection failures, ObjectId validation errors, memory issues

**Debug Commands**: `kubectl logs`, `kubectl get pods`, `kubectl top pods`

## 📈 Performance

**Flask**: Connection pooling, timeout configuration

**Database**: Text search indexes, compound indexes for queries

**Resources**: 128Mi-256Mi memory, 100m-200m CPU limits

## 🔗 Integration

**Frontend**: Nginx routes `/api/notes/*` to notes-service:5002

**Service Mesh**: Kubernetes DNS, load balancing, health check integration

## 📚 Dependencies

**Python**: Flask 2.3.3, flask-cors 4.0.0, pymongo 4.5.0

**External**: MongoDB, Kubernetes, Docker Hub, Nginx

## 🔍 Features

**Text Search**: MongoDB full-text search on title and content

**Future**: Categories, tags, timestamps

## 🏷️ Tags
`python` `flask` `mongodb` `microservices` `rest-api` `kubernetes` `docker` `notes` `content-management`

---

**🌟 Robust Python Flask microservice for comprehensive note management!**