

## 1. **System Context Diagram**

![SystemContext1](https://github.com/user-attachments/assets/c3491ab7-0afe-4937-b812-12d6ca7a9c45)

```plantuml
@startuml
' External Actors with Colors
actor "Player" as Player #LightBlue
actor "Spectator" as Spectator #LightGreen
actor "Admin" as Admin #LightYellow
actor "AI Chess Bot" as AIChessBot #Orange

' System Boundary: Chess.com Competitor with Colors
package "Chess.com Competitor" #LightGray {
    
    ' Subsystems with distinct colors
    rectangle "User Registration \nand Authentication" as Registration #A9DCDF
    rectangle "Game Management" as GameManagement #FFDDC1
    rectangle "Spectator Mode" as SpectatorMode #C2E9FF
    rectangle "Admin Panel" as AdminPanel #F7A8B8
    rectangle "Leaderboard and Stats" as Leaderboard #C3E6CB
    rectangle "In-App Chat \nand Support" as ChatSupport #FFABAB
    rectangle "Real-Time Match Tracking" as MatchTracking #D9A6FF
    rectangle "Tournaments" as Tournaments #FFC3A0
}

' Relationships between actors and system components with clear paths
Player --> Registration : Sign Up/Login
Player --> GameManagement : Play with AI / Play with other Players
Player --> Leaderboard : View Rankings
Player --> ChatSupport : Chat with Opponents
Player --> Tournaments : Participate in Tournaments
Player --> SpectatorMode : Watch Games

AIChessBot --> GameManagement : Simulate AI Matches

Spectator --> SpectatorMode : Watch Games
Spectator --> Leaderboard : View Rankings

Admin --> AdminPanel : Monitor Platform
Admin --> ChatSupport : Resolve User Issues
Admin --> Tournaments : Oversee Tournament Management

GameManagement --> MatchTracking : Monitors Matches
Tournaments --> MatchTracking : Tracks Live Tournament Matches
@enduml
```

---
## 2. **Conatiner Diagram**

### 2.1. **Container Diagram for Players**

![image](https://github.com/user-attachments/assets/ed404e75-1cf6-4d36-9320-e0439a60de07)


```plantuml
@startuml
!define RECTANGLE rectangle

title Container Diagram - Player

' Primary containers for the Player's system experience
RECTANGLE "Player Web Application" as playerWebApp <<Web Application>> #a2d5ff
RECTANGLE "Player API Gateway" as playerGateway <<API Gateway>> #f0f8ff

' Services for Player operations with distinct colors
RECTANGLE "Authentication Service" as authService <<Service>> #b2dfc0
RECTANGLE "Game Service" as gameService <<Service>> #cce5ff
RECTANGLE "AI Chess Bot Service" as aiChessBotService <<Service>> #ffa07a
RECTANGLE "Leaderboard Service" as leaderboardService <<Service>> #d0e7ff
RECTANGLE "Chat Service" as chatService <<Service>> #f4a261
RECTANGLE "Tournaments Service" as tournamentsService <<Service>> #d5a6bd

' Databases below their respective services
RECTANGLE "MongoDB: User Info" as userDB <<Database>> #ffd700
RECTANGLE "MongoDB: Game Progress" as gameDB <<Database>> #ffec40
RECTANGLE "MongoDB: Leaderboard Data" as leaderboardDB <<Database>> #c3e6cb
RECTANGLE "MongoDB: Tournaments Data" as tournamentsDB <<Database>> #b3d9ff
RECTANGLE "MongoDB: AI Bot Data" as aiBotDB <<Database>> #ff99c8

' Relationships for web app and system components
playerWebApp --> playerGateway : "API Requests"
playerGateway --> authService : "Sign Up/Login"
playerGateway --> gameService : "Matchmaking/Play with AI or other Players"
playerGateway --> aiChessBotService : "AI Moves/Decision Making"
playerGateway --> leaderboardService : "Retrieve Leaderboard Stats"
playerGateway --> chatService : "Enable Chat"
playerGateway --> tournamentsService : "Register/Participate in Tournaments"

' Service interactions with their respective databases
authService --> userDB : "User Authentication & Data"
gameService --> gameDB : "Track Game Progress"
aiChessBotService --> aiBotDB : "Fetch AI Logic & Decisions"
leaderboardService --> leaderboardDB : "Leaderboard Stats"
tournamentsService --> tournamentsDB : "Tournament Registrations & Progress"
@enduml
```

---

### 2.2. **Container Diagram for Admins**

![image](https://github.com/user-attachments/assets/c63c7df6-3200-49fd-b574-18cabed21822)

```plantuml
@startuml
!define RECTANGLE rectangle

title Container Diagram - Admin

' Primary containers for the Admin's system operations
RECTANGLE "Admin Web Application" as adminWebApp <<Web Application>> #b3e5fc
RECTANGLE "Admin API Gateway" as adminGateway <<API Gateway>> #e1f5fe

' Admin services with distinct colors
RECTANGLE "Admin Panel Service" as adminPanelService <<Service>> #c8e6c9
RECTANGLE "User Management Service" as userManagementService <<Service>> #dcedc8
RECTANGLE "Tournament Management Service" as tournamentManagementService <<Service>> #ffccbc
RECTANGLE "User Support Service" as userSupportService <<Service>> #f8bbd0
RECTANGLE "Analytics & Monitoring Service" as analyticsMonitoringService <<Service>> #ffe0b2

' Databases for the Admin system
RECTANGLE "MongoDB: User Info" as userDB <<Database>> #ffd700
RECTANGLE "MongoDB: Tournament Data" as tournamentDB <<Database>> #ffcdd2
RECTANGLE "MongoDB: User Reports" as userReportsDB <<Database>> #f0f4c3
RECTANGLE "MongoDB: Admin Analytics Data" as adminAnalyticsDB <<Database>> #bbdefb

' Relationships for admin web app and system components
adminWebApp --> adminGateway : "Admin Actions"
adminGateway --> adminPanelService : "Access Admin Panel"
adminGateway --> userManagementService : "Manage Users"
adminGateway --> tournamentManagementService : "Manage Tournaments"
adminGateway --> userSupportService : "Handle User Reports"
adminGateway --> analyticsMonitoringService : "View Game Analytics & Reports"

' Service interactions with their respective databases
userManagementService --> userDB : "Fetch/Update User Data"
tournamentManagementService --> tournamentDB : "Manage Tournaments Data"
userSupportService --> userReportsDB : "Store & Process Requests"
analyticsMonitoringService --> adminAnalyticsDB : "Retrieve Game Reports & Logs"
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
