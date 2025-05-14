# 🚗 RentCar Microservices Project

Ce projet est une application de **location de voitures** construite sur une architecture **microservices**. Elle utilise **gRPC** pour la communication interservices, une **API Gateway REST** pour l’interface client (Postman, navigateur…), et **Kafka** pour la communication asynchrone (pub/sub).

---

## 📦 Architecture

- **user-service** : Gère l’enregistrement, la connexion et la gestion des utilisateurs.
- **car-service** : Gère les opérations CRUD sur les voitures et publie des événements Kafka.
- **api-gateway** : Fournit une API REST publique qui communique avec les services via gRPC.
- **kafka** : Écoute les événements Kafka pour les voitures ajoutées.

```txt
+-------------+          +-------------------+        +--------------+
|             |  REST    |                   |  gRPC  |              |
|  Client     +--------->+    API Gateway    +------->+ user-service |
|             |          |                   |        +--------------+
+-------------+          |                   |
                         |                   |  gRPC
                         |                   v
                         |              +--------------+
                         +------------->+ car-service  |
                                         +--------------+
                                                |
                                                | Kafka (car-added)
                                                v
                                        +-----------------+
                                        | kafka  |
                                        +-----------------+
```

---

## 🧱 Structure du projet

```bash
.
├── apiGateway
│   ├── gateway.js
│   ├── protos/
│   │   ├── user.proto
│   │   └── car.proto
│   ├── Dockerfile
│   └── package.json
├── user-service
│   ├── user.js
│   ├── user.proto
│   ├── Dockerfile
│   └── package.json
├── car-service
│   ├── car.js
│   ├── producer.js    
│   ├── car.proto
│   ├── Dockerfile
│   └── package.json
├── kafka
│   ├── consumer.js    
│   ├── Dockerfile
│   └── package.json
└── docker-compose.yml
```

---

## 🚀 Lancement du projet

### 1. Cloner le projet

```bash
git clone https://github.com/ton-utilisateur/rentcar-microservices.git
cd rentcar-microservices
```

### 2. Lancer tous les services avec Docker Compose

```bash
docker-compose up --build
```

---

## 📌 Ports exposés

| Service         | Port interne | Port local | Protocole |
|-----------------|--------------|------------|-----------|
| user-service    | 50051        | 50051      | gRPC      |
| car-service     | 50052        | 50052      | gRPC      |
| api-gateway     | 3000         | 3000       | REST      |
| kafka (broker)  | 9092         | 9092       | Kafka     |

---

## 📬 Exemples d'appels API (via Postman ou autre)

### 🔐 Créer un utilisateur

```
POST http://localhost:3000/users
{
  "name": "Alice",
  "email": "alice@example.com",
  "password": "secret123"
}
```

### 🔑 Connexion utilisateur

```
POST http://localhost:3000/users/login
{
  "email": "alice@example.com",
  "password": "secret123"
}
```

### 🚘 Ajouter une voiture (et envoyer un message Kafka)

```
POST http://localhost:3000/cars
{
  "brand": "Toyota",
  "model": "Yaris",
  "available": true
}
```

### 📋 Lister toutes les voitures

```
GET http://localhost:3000/cars
```

---

## 🛠 Technologies utilisées

- **Node.js**
- **gRPC** (`@grpc/grpc-js`, `@grpc/proto-loader`)
- **Kafka** (`kafkajs`)
- **REST API** avec Express.js
- **Docker** & **Docker Compose**
- **Protocol Buffers (Protobuf)**

---

## 📎 Notes

- Les données sont stockées **en mémoire** (simples tableaux) → à remplacer par une base de données réelle.
- Les microservices utilisent des fichiers `.proto` pour la communication gRPC.
- Kafka est utilisé pour **la communication asynchrone** entre services (pub/sub).
- Le consumer Kafka est dans un conteneur séparé et écoute le topic `car-added`.

---

## 🔮 Améliorations futures

- Ajouter une base de données (MongoDB, PostgreSQL…)
- Ajouter une authentification avec JWT
- Intégrer un **reservation-service**
- Ajouter des tests unitaires
- Déploiement avec Docker Swarm ou Kubernetes
- Dashboard Kafka avec Kafdrop ou Kafka UI

---

## 👩‍💻 Auteur

- **Wiem 🦋**  
- Projet académique sur les microservices — 2025
