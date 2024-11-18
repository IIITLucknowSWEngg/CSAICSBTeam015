---

## 1. **System Context Diagram**

The System Context Diagram offers a high-level view of the **Chess Clone App** and its interactions with external actors and systems.
![PHOTO-2024-11-18-14-29-23](https://github.com/user-attachments/assets/ba3a109e-8a9f-4eea-9ff3-75142b691e1e)

```plantuml
@startuml
' External Actors
actor "Player (User)" as Player
actor "Admin" as Admin
actor "Chess AI" as ChessAI
actor "Notification Service" as NotificationService

' System Boundary: Chess Clone App
package "Chess Clone App" {

    ' Subsystems
    rectangle "User Authentication \nand Profile Management" as AuthSystem
    rectangle "Game Lobby \nand Matchmaking" as GameLobby
    rectangle "Chess Gameplay Engine" as GameplayEngine
    rectangle "Leaderboard \nand Statistics" as Leaderboard
    rectangle "In-Game Chat" as ChatSystem
    rectangle "Admin Panel" as AdminPanel
}

' Relationships between actors and system components
Player --> AuthSystem : Sign Up/Login
Player --> GameLobby : Join/Create Match
Player --> GameplayEngine : Play Chess
Player --> Leaderboard : View Rankings
Player --> ChatSystem : Chat in Matches

Admin --> AdminPanel : Manage Users and Games
GameplayEngine --> ChessAI : Access AI Moves
GameplayEngine --> NotificationService : Notify Players
@enduml
```

---
## 2. **Conatiner Diagram**
![PHOTO-2024-11-18-14-30-11](https://github.com/user-attachments/assets/8b6d55c7-ca97-4f4a-9903-cd03877866fb)

```plantuml
@startuml
title Container Diagram - Chess Clone

' Add primary containers
rectangle "Web/Mobile App" as App <<User Interface>> #lightblue
rectangle "API Gateway" as APIGateway <<API Gateway>> #lightgreen
rectangle "Game Engine Service" as GameEngine <<Service>> #lightyellow
rectangle "User Service" as UserService <<Service>> #lightyellow
rectangle "Leaderboard Service" as LeaderboardService <<Service>> #lightyellow
rectangle "Chat Service" as ChatService <<Service>> #lightyellow

' Database containers
database "Game Database" as GameDB <<Database>> #lightpink
database "User Database" as UserDB <<Database>> #lightpink
database "Leaderboard Database" as LeaderboardDB <<Database>> #lightpink

' External services
rectangle "Notification Service" as NotificationService <<External Service>> #lightgray

' Relationships between containers
App --> APIGateway : API Requests
APIGateway --> UserService : Manage Users
APIGateway --> GameEngine : Game Logic
APIGateway --> LeaderboardService : Rankings
APIGateway --> ChatService : Messaging
APIGateway --> NotificationService : Player Notifications

GameEngine --> GameDB : Read/Write Games
UserService --> UserDB : Manage User Data
LeaderboardService --> LeaderboardDB : Update Rankings

@enduml
```

---

## 3. **Component Diagram**

### 3.1. **Component Diagram for Players**

![image](https://github.com/user-attachments/assets/43183bcf-5aae-4df1-b765-771b3c7faaa5)


```plantuml
@startuml
' External Actor
actor "Player" as Player

' System Boundary: Chess Clone App
package "Chess Clone App" {

    ' Subsystems for Player
    rectangle "Authentication \nand Profile Management" as AuthSystem
    rectangle "Game Lobby \nand Matchmaking" as GameLobby
    rectangle "Chess Gameplay Engine" as GameplayEngine
    rectangle "Leaderboard \nand Statistics" as Leaderboard
    rectangle "In-Game Chat" as ChatSystem
}

' Relationships between Player and system components
Player --> AuthSystem : Sign Up/Login
Player --> GameLobby : Join/Create Match
Player --> GameplayEngine : Play Chess
Player --> Leaderboard : View Rankings
Player --> ChatSystem : Chat with Opponent
@enduml
```

---

### 3.2. **Component Diagram for Admins**

![image](https://github.com/user-attachments/assets/b1dff844-96b9-485c-a57f-8199da55e4ca)


```plantuml
@startuml
' External Actor
actor "Admin" as Admin

' System Boundary: Chess Clone Admin Panel
package "Admin Panel" {

    ' Subsystems for Admin
    rectangle "User Management" as UserManagement
    rectangle "Game Monitoring" as GameMonitoring
    rectangle "Leaderboard Management" as LeaderboardManagement
    rectangle "Notification Management" as NotificationManagement
    rectangle "Reports and Analytics" as ReportsAnalytics
}

' Relationships between Admin and system components
Admin --> UserManagement : Manage Users
Admin --> GameMonitoring : Monitor Games
Admin --> LeaderboardManagement : Manage Rankings
Admin --> NotificationManagement : Send Notifications
Admin --> ReportsAnalytics : Generate Reports
@enduml
```


---

## 4. **Deployment Diagram**

![PHOTO-2024-11-18-14-32-28](https://github.com/user-attachments/assets/53b73b63-6112-4218-90c9-e74991e2dde1)
.

```plantuml
@startuml
title Deployment Diagram - Chess Clone

node "Player's Device" {
    [Web/Mobile App] <<User Interface>>
}

node "Server" {
    [API Gateway] <<API Gateway>>
    [Game Engine Service] <<Service>>
    [User Service] <<Service>>
    [Leaderboard Service] <<Service>>
    [Chat Service] <<Service>>
}

node "Database Server" {
    database "Game Database" as GameDB
    database "User Database" as UserDB
    database "Leaderboard Database" as LeaderboardDB
}

cloud "External Services" {
    [Notification Service] <<External Service>>
}

' Connections
[Web/Mobile App] --> [API Gateway] : API Calls
[API Gateway] --> [Game Engine Service] : Handle Moves
[API Gateway] --> [User Service] : Manage Profiles
[API Gateway] --> [Leaderboard Service] : Rankings
[API Gateway] --> [Chat Service] : Chat Messages
[Game Engine Service] --> GameDB : Save Game Data
[User Service] --> UserDB : User Data
[Leaderboard Service] --> LeaderboardDB : Rankings

@enduml
```
