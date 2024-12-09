# **Software Design Document (SDD)**

## **1. Introduction**

### **1.1 Purpose**
This document outlines the software design for a chess platform. It includes the system architecture, entity relationships, microservice details, subsystem interactions, and deployment strategy, aiming to provide clear guidance for the development of the platform.

### **1.2 Scope**
The design covers the following:
- **System Architecture**: Overview of frontend, backend, database, and services.
- **Entity Relationship Diagram**: Representation of the entities and their relationships.
- **Database Schema**: Detailed description of database collections.
- **Subsystem Interaction**: Interaction between the system components.
- **Deployment Strategy**: Overview of the deployment architecture.

---

## **2. System Overview**

The platform is a **web application** designed for both **mobile and desktop devices**. It uses a **microservices architecture** where each service handles a specific feature such as authentication, game management, tournament management, leaderboard, and real-time chat.

### **2.1 Key Components**
- **Frontend**: Built using **React.js** for web-based access across devices.
- **Backend**: Microservices built using **Node.js** with **Express**, communicating via RESTful APIs and WebSocket.
- **Database**: **MongoDB** for storing user profiles, game history, tournament data, and chat messages.

### **2.2 Deployment Strategy**
The system will be deployed using **AWS** (Amazon Web Services) for scalable hosting. Docker will be used for containerization, providing a lightweight and portable deployment model.

---

## **3. System Architecture**

### **3.1 Architectural Style**
The platform follows a **microservices architecture** that separates different functionalities into independent services. This provides:
- Scalability
- Maintainability
- Easy updates without affecting other services

### **3.2 Components Overview**

#### **Frontend**
- **Technology**: **React.js** for web.
- **Features**: 
  - User authentication (sign-up, login)
  - Real-time gameplay
  - Chat during games
  - Tournament management
  - Leaderboard viewing

#### **Backend (Microservices)**

1. **Authentication Service**: Handles user authentication, registration, and session management.
2. **Game Service**: Manages the gameplay, player moves, match states, and results.
3. **Tournament Service**: Manages tournaments, player registrations, and match scheduling.
4. **Leaderboard Service**: Tracks player performance, updating rankings based on ELO.

#### **Database (MongoDB)**
- Stores data in collections:
  - **Users**: Stores user profiles.
  - **Matches**: Stores match details such as player moves and results.
  - **Tournaments**: Stores tournament details.
  - **Leaderboard**: Stores player rankings.
  - **Chat**: Stores messages exchanged during games.

### **3.3 Communication**
- **Frontend** communicates with the **Backend** via RESTful APIs for non-real-time operations (e.g., user authentication, game creation).
- **WebSocket** is used for real-time interactions (e.g., gameplay, chat).
- Microservices interact with the **Database** to store and retrieve information.

---

## **4. Entity Relationship Diagram (ERD)**

![image](https://github.com/user-attachments/assets/efe525cd-c21c-42b0-8f3e-882125ce0e34)


### **4.1 Entity Descriptions**

1. **User**:
   - **userId**: Unique identifier.
   - **username**: The user's display name.
   - **password**: The password for authentication.
   - **avatar**: The user's avatar image.
   - **ELO**: Player’s rating based on their game performance.
   - **history**: A list of matches the user has played.

2. **Match**:
   - **matchId**: Unique match identifier.
   - **player1**, **player2**: Players participating in the match.
   - **moves**: A sequence of moves played in the game.
   - **result**: The outcome (win, loss, or draw).

3. **Tournament**:
   - **tournamentId**: Unique tournament identifier.
   - **name**: Tournament name.
   - **participants**: List of players participating in the tournament.
   - **matches**: List of matches in the tournament.

4. **Leaderboard**:
   - **rank**: The player’s rank in the leaderboard.
   - **userId**: The identifier for the user.
   - **ELO**: Player's ELO rating.

5. **Chat**:
   - **chatId**: Unique identifier for each message.
   - **userId**: The ID of the user sending the message.
   - **message**: Content of the chat message.
   - **timestamp**: When the message was sent.

---

## **5. Database Schema**

The following collections will be present in the **MongoDB** database:

1. **Users Collection**: Stores user information such as `userId`, `username`, `password`, `avatar`, `ELO`, and `history`.
2. **Matches Collection**: Stores match data with `matchId`, `player1`, `player2`, `moves`, and `result`.
3. **Tournaments Collection**: Stores tournament data including `tournamentId`, `name`, `participants`, and `matches`.
4. **Leaderboard Collection**: Stores rankings with `rank`, `userId`, and `ELO`.

---

## **6. Microservices Breakdown**

### **6.1 Authentication Service**
- **Responsibilities**: Handles user login, registration, and session management.
- **Endpoints**:
  - `POST /register`: Registers a new user.
  - `POST /login`: Logs a user in and returns a session token.
  - `GET /profile`: Fetches user profile information.

### **6.2 Game Service**
- **Responsibilities**: Manages game creation, processing player moves, and determining match outcomes.
- **Endpoints**:
  - `POST /startGame`: Starts a new match.
  - `POST /makeMove`: Processes a player’s move.
  - `GET /gameStatus`: Retrieves the current status of a game.

### **6.3 Tournament Service**
- **Responsibilities**: Manages tournaments, player registrations, and match progress.
- **Endpoints**:
  - `POST /createTournament`: Creates a new tournament.
  - `GET /tournamentStatus`: Fetches the status of a tournament.

### **6.4 Leaderboard Service**
- **Responsibilities**: Maintains and updates the leaderboard based on ELO ratings.
- **Endpoints**:
  - `GET /leaderboard`: Fetches the current leaderboard.

### **6.5 Chat Service**
- **Responsibilities**: Manages real-time chat between users during matches.
- **Endpoints**:
  - `POST /sendMessage`: Sends a message during gameplay.

---

## **7. Subsystem Interaction Diagram**

![image](https://github.com/user-attachments/assets/677cc4c1-cc41-44dd-8765-5bd40c9fc660)


---

## **8. Conclusion**

This document provides a clear blueprint for the development of a modular, scalable chess platform with functionalities such as user authentication, matchmaking, tournaments, leaderboards, and real-time messaging. The architecture ensures a clear separation of concerns using **microservices**, making it easier to manage, scale, and extend as needed.

## **8.1 Engineering Blog References**

https://www.chess.com/blog/chesscom



