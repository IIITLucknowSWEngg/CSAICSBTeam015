

## 1. **System Context Diagram**

![SYSTEM CONTEXT CHESS COM](https://github.com/user-attachments/assets/43b60fb9-e565-466f-a8cd-48c52c9bbd14)


```plantuml
@startuml
!include https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/master/C4_Context.puml

title System Context Diagram - Chess.com Competitor

Person(User, "Player", "Plays chess, chats, spectates")
Person(Admin, "Administrator", "Manages tournaments and the platform")
Person(Spectator, "Spectator", "Watches games and tournaments")

System(System, "Chess.com Competitor", "Provides chess gameplay, tournaments, and spectating")

System_Ext(SocialLogin, "Social Login Services", "Handles user authentication via social accounts")
System_Ext(ChessEngine, "Chess Engine API", "Provides move validation and analysis")
System_Ext(GDPR, "GDPR Authority", "Ensures compliance with data protection regulations")

User -> System : "Play Chess, Chat, Spectate"
Admin -> System : "Manage tournaments and platform"
Spectator -> System : "Watch live games and tournaments"
System -> SocialLogin : "Authenticate users"
System -> ChessEngine : "Validate moves, provide analysis"
System -> GDPR : "Compliance with data protection"

@enduml
```

---
## 2. **Container Diagram**

![CHESS COM CONTAINER DIAGRAM](https://github.com/user-attachments/assets/a949cda4-874a-4141-87e3-0927da7f1759)


```plantuml
@startuml
!define C4P https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/master
!include C4P/C4_Container.puml

title Container Diagram - Chess.com Competitor

Person(Player, "Player", "Plays chess, chats, and participates in tournaments")
Person(Admin, "Administrator", "Manages tournaments and platform settings")
Person(Spectator, "Spectator", "Watches live games and tournaments")

System_Boundary(ChessPlatform, "Chess.com Competitor") {
    Container(Frontend, "Frontend Application", "HTML/CSS/JavaScript", "Provides user interfaces for all users")
    Container(API, "Backend Server", "Node.js/Express", "Handles business logic, user management, and API endpoints")
    ContainerDb(Database, "Database", "MongoDB", "Stores user data, game history, leaderboards, and chat logs")
    Container(Realtime, "WebSocket Service", "WebSocket API", "Enables real-time gameplay, chat, and spectating")
    Container(StaticContent, "Static Content", "AWS S3", "Hosts static files such as frontend assets")
    Container(ChessEngine, "Chess Engine API", "External System", "Validates chess moves and provides AI-powered analysis")
    Container(Auth, "Authentication Service", "Amazon Cognito", "Handles secure user authentication and social login integration")
}

System_Ext(SocialLogin, "Social Login Services", "Handles user authentication via social accounts")
System_Ext(GDPR, "GDPR Authority", "Ensures compliance with data protection regulations")

Player -down-> Frontend : "Access platform via browser"
Admin -down-> Frontend : "Manages tournaments and settings"
Spectator -down-> Frontend : "Watches live games and tournaments"

Frontend -down-> API : "Requests gameplay, user, and tournament data"
Frontend -down-> Realtime : "Connects for live updates and real-time gameplay"
Frontend -down-> StaticContent : "Loads static assets"

API -down-> Database : "Stores and retrieves user data"
API -down-> ChessEngine : "Validates moves, requests AI analysis"
API -down-> Auth : "Authenticates users"
Realtime -down-> API : "Communicates game state and chat data"

API -down-> GDPR : "Ensures compliance with regulations"
Auth -down-> SocialLogin : "Handles third-party authentication"
Auth -down-> Database : "Stores user credentials"
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
