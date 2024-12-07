

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
## 2. **Container Diagram**

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

![image](https://github.com/user-attachments/assets/1f5befe9-f33a-4518-a457-686f918f9d03)



```plantuml
@startuml
!define RECTANGLE rectangle

title Component Diagram - Player

' Actor: Player
actor "Player" as player #a2d5ff

' Web Application Components
package " Web Application" #f0f8ff {
    RECTANGLE "Login Page" as loginPage <<Component>> #b2dfc0
    RECTANGLE "Game Interface" as gameInterface <<Component>> #cce5ff
    RECTANGLE "Leaderboard View" as leaderboardView <<Component>> #d0e7ff
    RECTANGLE "Chat Window" as chatWindow <<Component>> #f4a261
    RECTANGLE "Tournament Dashboard" as tournamentDashboard <<Component>> #d5a6bd
}

' API Gateway Components
RECTANGLE "API Request Handler" as apiHandler <<Component>> #f7d6e0

' Service Components
package "Player Services" #ffec40 {
    RECTANGLE "Authentication Manager" as authManager <<Component>> #b2dfc0
    RECTANGLE "Matchmaking Engine" as matchmakingEngine <<Component>> #cce5ff
    RECTANGLE "AI Bot Manager" as aiBotManager <<Component>> #ffa07a
    RECTANGLE "Leaderboard Manager" as leaderboardManager <<Component>> #d0e7ff
    RECTANGLE "Chat Manager" as chatManager <<Component>> #f4a261
    RECTANGLE "Tournament Manager" as tournamentManager <<Component>> #d5a6bd
}

' Databases for Player Data
package "Databases" #ffd700 {
    RECTANGLE "User Database" as userDB <<Database>> #ffd700
    RECTANGLE "Game Database" as gameDB <<Database>> #ffec40
    RECTANGLE "Leaderboard Database" as leaderboardDB <<Database>> #c3e6cb
    RECTANGLE "Tournament Database" as tournamentDB <<Database>> #b3d9ff
    RECTANGLE "AI Logic Database" as aiBotDB <<Database>> #ff99c8
}

' Relationships between Player and Web App
player --> loginPage : "Log in"
player --> gameInterface : "Play Games"
player --> leaderboardView : "View Rankings"
player --> chatWindow : "Chat with Opponents"
player --> tournamentDashboard : "Manage Tournaments"

' Web App to API Gateway
loginPage --> apiHandler : "Submit Login Request"
gameInterface --> apiHandler : "Send Game Actions"
leaderboardView --> apiHandler : "Fetch Leaderboard Data"
chatWindow --> apiHandler : "Send/Receive Messages"
tournamentDashboard --> apiHandler : "Register/Track Progress"

' API Gateway to Services
apiHandler --> authManager : "Authentication Requests"
apiHandler --> matchmakingEngine : "Matchmaking Requests"
apiHandler --> aiBotManager : "Request AI Moves"
apiHandler --> leaderboardManager : "Leaderboard Queries"
apiHandler --> chatManager : "Handle Chat Requests"
apiHandler --> tournamentManager : "Tournament Actions"

' Services to Databases
authManager --> userDB : "Fetch/Store User Data"
matchmakingEngine --> gameDB : "Update Game Progress"
aiBotManager --> aiBotDB : "Fetch AI Data"
leaderboardManager --> leaderboardDB : "Update Leaderboard"
tournamentManager --> tournamentDB : "Register Players"
@enduml
```

---

### 3.2. **Component Diagram for Admins**

![image](https://github.com/user-attachments/assets/e3c9dcd5-9edc-478d-9a35-cc85cce32c9b)



```plantuml
@startuml
!define RECTANGLE rectangle

title Component Diagram - Admin

' Actor: Admin
actor "Admin" as adminActor #b3e5fc

'Web Application Components
package "Web Application" #e1f5fe {
    RECTANGLE "Login & Authentication Module" as loginModule <<Component>> #c8e6c9
    RECTANGLE "Dashboard UI" as dashboardUI <<Component>> #ffccbc
    RECTANGLE "User Management UI" as userManagementUI <<Component>> #dcedc8
    RECTANGLE "Tournament Management UI" as tournamentManagementUI <<Component>> #ffccbc
    RECTANGLE "User Reports UI" as userReportsUI <<Component>> #f8bbd0
    RECTANGLE "Analytics Dashboard" as analyticsDashboard <<Component>> #ffe0b2
}

' Admin API Gateway Components
RECTANGLE "API Router" as apiRouter <<Component>> #f0f4c3

' Admin Services Components
package "Admin Services" #c8e6c9 {
    RECTANGLE "Admin Panel Logic" as adminPanelLogic <<Component>> #c8e6c9
    RECTANGLE "User Management Logic" as userManagementLogic <<Component>> #dcedc8
    RECTANGLE "Tournament Management Logic" as tournamentManagementLogic <<Component>> #ffccbc
    RECTANGLE "User Reports Processor" as userReportsProcessor <<Component>> #f8bbd0
    RECTANGLE "Analytics Processor" as analyticsProcessor <<Component>> #ffe0b2
}

' Databases for Admin Data
package "Databases" #ffd700 {
    RECTANGLE "User Info Database" as userDB <<Database>> #ffd700
    RECTANGLE "Tournament Database" as tournamentDB <<Database>> #ffcdd2
    RECTANGLE "User Reports Database" as userReportsDB <<Database>> #f0f4c3
    RECTANGLE "Analytics Database" as adminAnalyticsDB <<Database>> #bbdefb
}

' Relationships for Admin interaction
adminActor --> loginModule : "Log In"
adminActor --> dashboardUI : "Navigate Dashboard"
adminActor --> userManagementUI : "Manage Users"
adminActor --> tournamentManagementUI : "Manage Tournaments"
adminActor --> userReportsUI : "Review User Reports"
adminActor --> analyticsDashboard : "View Game Analytics & Reports"

' Web App to API Router
loginModule --> apiRouter : "Send Login Requests"
dashboardUI --> apiRouter : "Fetch Dashboard Data"
userManagementUI --> apiRouter : "User Management Actions"
tournamentManagementUI --> apiRouter : "Tournament Actions"
userReportsUI --> apiRouter : "User Reports Operations"
analyticsDashboard --> apiRouter : "Analytics Queries"

' API Router to Services
apiRouter --> adminPanelLogic : "Route Admin Panel Requests"
apiRouter --> userManagementLogic : "Route User Management Actions"
apiRouter --> tournamentManagementLogic : "Route Tournament Requests"
apiRouter --> userReportsProcessor : "Route User Reports Processing"
apiRouter --> analyticsProcessor : "Route Analytics Queries"

' Services to Databases
userManagementLogic --> userDB : "Fetch/Update User Data"
tournamentManagementLogic --> tournamentDB : "Fetch/Store Tournament Data"
userReportsProcessor --> userReportsDB : "Process User Reports"
analyticsProcessor --> adminAnalyticsDB : "Query Game Analytics"
@enduml
```


---

## 4. **Deployment Diagram**

![image](https://github.com/user-attachments/assets/d89a2bf8-25ff-473c-bdb4-b1142a6a991f)


```plantuml
@startuml
!define RECTANGLE rectangle

title Deployment Diagram - Chess.com Competitor

' Nodes (Hardware)
node "Player's Browser" as playerBrowser #a2d5ff
node "Admin's Browser" as adminBrowser #c3e6cb

node "AWS EC2 Web Server" as webServer #f9c74f {
    artifact "Player Web Application" as playerWebApp <<Web Application>>
    artifact "Admin Web Application" as adminWebApp <<Web Application>>
}

node "AWS ECS/API Server" as apiServer #90be6d {
    artifact "Player API Gateway" as playerApiGateway <<API Gateway>>
    artifact "Admin API Gateway" as adminApiGateway <<API Gateway>>
    artifact "Authentication Service" as authService <<Service>>
    artifact "Game Service" as gameService <<Service>>
    artifact "Leaderboard Service" as leaderboardService <<Service>>
    artifact "Tournament Service" as tournamentService <<Service>>
    artifact "User Management Service" as userManagementService <<Service>>
    artifact "User Reports Processor" as userReportsProcessor <<Service>>
}

node "AWS DocumentDB" as dbServer #577590 {
    database "MongoDB: User Data" as userDB #f4a261
    database "MongoDB: Game Data" as gameDB #f4a261
    database "MongoDB: Leaderboard Data" as leaderboardDB #f4a261
    database "MongoDB: Tournament Data" as tournamentDB #f4a261
    database "MongoDB: User Reports" as userReportsDB #f4a261
}

' Connections
playerBrowser --> playerWebApp : "HTTP/HTTPS Requests"
adminBrowser --> adminWebApp : "HTTP/HTTPS Requests"

playerWebApp --> playerApiGateway : "API Calls"
adminWebApp --> adminApiGateway : "API Calls"

playerApiGateway --> authService : "Authentication Requests"
playerApiGateway --> gameService : "Game Actions"
playerApiGateway --> leaderboardService : "Leaderboard Data"
playerApiGateway --> tournamentService : "Tournament Data"

adminApiGateway --> userManagementService : "User Management Actions"
adminApiGateway --> tournamentService : "Manage Tournaments"
adminApiGateway --> userReportsProcessor : "Process User Reports"

authService --> userDB : "Query User Data"
gameService --> gameDB : "Save/Load Game Progress"
leaderboardService --> leaderboardDB : "Fetch Leaderboard Stats"
tournamentService --> tournamentDB : "Register/Update Tournaments"
userReportsProcessor --> userReportsDB : "Store & Retrieve Reports"
@enduml
```
