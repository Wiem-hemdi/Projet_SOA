# 🚗 RentCar Microservices Project

Ce projet est une application de location de voitures basée sur une architecture **microservices**. Il utilise **gRPC** pour la communication interservices et une **API Gateway REST** pour l’interface avec les clients (Postman, navigateur, etc.).

---

## 📦 Architecture

- **user-service** : Gère l’enregistrement, la connexion et la gestion des utilisateurs.
- **car-service** : Gère les opérations sur les voitures (ajout, mise à jour, suppression).
- **api-gateway** : Fournit une API REST publique qui communique avec les services via gRPC.

```txt
+-------------+          +-------------------+        +--------------+
|             |  REST    |                   |  gRPC  |              |
|  Client     +--------->+    API Gateway    +------->+  user-service|
|             |          |                   |        |              |
+-------------+          +-------------------+        +--------------+
                                     |
                                     |  gRPC
                                     v
                             +--------------+
                             |  car-service |
                             +--------------+
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
│   ├── car.proto
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

## 📌 Points techniques

### 🧪 Ports exposés

| Service       | Port interne | Port local | Protocole |
|---------------|--------------|------------|-----------|
| user-service  | 50051        | 50051      | gRPC      |
| car-service   | 50052        | 50052      | gRPC      |
| api-gateway   | 3000         | 3000       | REST      |

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

### 🚘 Ajouter une voiture
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
- **gRPC** avec `@grpc/grpc-js` et `@grpc/proto-loader`
- **Docker** & **Docker Compose**
- **REST API** via Express.js
- **Protobuf** (Protocol Buffers)

---

## 📎 Notes

- Les données sont **stockées en mémoire** (tableaux simples) → à remplacer par une base de données pour un usage réel.
- Chaque microservice expose son propre fichier `.proto` pour la communication.
- Les services se reconnaissent grâce à leurs **noms Docker (ex: `user-service`)** via le réseau `rentcar-net`.

---

## 🔮 Améliorations futures

- Ajouter une base de données (MongoDB, PostgreSQL, etc.)
- Ajouter une authentification par token JWT
- Ajouter des tests unitaires
- Déployer avec Docker Swarm ou Kubernetes
- Intégrer un service `reservation-service`

---

## 👩‍💻 Auteur

- Wiem 🦋  
- Projet académique sur les microservices — 2025
