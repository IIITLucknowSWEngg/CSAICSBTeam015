

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

![CHESS COM COMPONENT DIAGRAM](https://github.com/user-attachments/assets/a6dc64bc-ffdf-4d64-a206-38fe3e3b2fbb)



```plantuml
@startuml
!define C4P https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/master
!include C4P/C4_Component.puml

title Component Diagram - Frontend for Chess.com Competitor

Container_Boundary(Frontend, "Frontend Application") {
    Component(LoginPage, "Login Page", "HTML/CSS/JavaScript", "Allows users to register or log in using email or social media accounts")
    Component(Dashboard, "Dashboard", "HTML/CSS/JavaScript", "Displays user-specific information like active matches, tournament standings, and leaderboard")
    Component(GameInterface, "Game Interface", "HTML/CSS/JavaScript", "Interactive chessboard for playing chess, move validation, and timer display")
    Component(Chat, "Chat", "WebSocket API", "Real-time messaging system for players to communicate during the game")
    Component(Tournament, "Tournament Management", "HTML/CSS/JavaScript", "Allows users to register and view tournament details and status")
    Component(AdminPanel, "Admin Panel", "HTML/CSS/JavaScript", "Allows admins to manage user accounts, tournaments, and platform settings")
    Component(SpectatorInterface, "Spectator Interface", "HTML/CSS/JavaScript", "Allows users to watch live games and tournaments in real-time")
    Component(StaticAssets, "Static Assets", "AWS S3", "Hosts static files such as images, CSS, and JavaScript for frontend")
    Component(Auth, "Authentication Service", "Amazon Cognito", "Handles secure login, user registration, and social media authentication")
}

LoginPage -down-> Auth : "User enters credentials"
Auth -down-> Dashboard : "Validates user and redirects to dashboard"
Dashboard -down-> GameInterface : "Displays active games and leaderboard"
Dashboard -down-> Tournament : "Shows tournament registration and status"
GameInterface -down-> Chat : "Integrates chat for real-time communication"
Dashboard -down-> StaticAssets : "Loads UI components and static assets"
AdminPanel -down-> StaticAssets : "Loads admin-specific UI components"
SpectatorInterface -down-> StaticAssets : "Loads spectator interface components"
Chat -down-> StaticAssets : "Loads chat UI components"
Tournament -down-> StaticAssets : "Loads tournament UI components"
@enduml
```


---

## 4. **Deployment Diagram**

![CHESS COM DEPLOYMENT](https://github.com/user-attachments/assets/44432da4-f90a-4e4b-a835-88b340c20a97)



```plantuml
@startuml
!define C4P https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/master
!include C4P/C4_Deployment.puml

title Deployment Diagram - Chess.com Competitor

Node(AWSCloud, "AWS Cloud") {
    Node(WebServer, "Web Server") {
        Container(FrontendApp, "Frontend Application", "HTML/CSS/JavaScript", "Handles user interface and interactions", "Runs on AWS EC2 with Nginx or Apache")
    }

    Node(BackendServer, "Backend Server") {
        Container(BackendApp, "Backend Application", "Java (Spring Boot)", "Handles API requests, game logic, and authentication", "Runs on AWS EC2")
        ContainerDb(MongoDB, "MongoDB", "NoSQL Database", "Stores user data, game history, and leaderboards", "Managed on AWS Atlas (NoSQL)")
        Container(WebSocketAPI, "WebSocket API", "WebSocket", "Handles real-time updates and communication during the game", "Hosted on AWS EC2 or similar platform")
        Container(Auth, "Authentication Service", "Amazon Cognito", "Manages user authentication", "Managed by AWS Cognito service")
    }

    Node(StaticAssetsStorage, "Static Assets Storage") {
        Container(StaticAssets, "Static Assets", "AWS S3", "Hosts images, CSS, JS files", "Hosted on AWS S3")
    }
}

FrontendApp -down-> BackendApp : "API Calls (REST)"
FrontendApp -down-> StaticAssets : "Fetch Static Files (Images, JS, CSS)"
BackendApp -down-> MongoDB : "Database operations (NoSQL)"
BackendApp -down-> WebSocketAPI : "Real-time updates"
BackendApp -down-> Auth : "User authentication and authorization"
WebSocketAPI -down-> StaticAssets : "Fetch static assets (e.g., game UI)"
MongoDB -down-> StaticAssets : "Store game-related data"
@enduml
```
