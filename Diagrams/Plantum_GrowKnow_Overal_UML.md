@startuml
title GrowKnow – Overall Use Case Diagram (Scope)

left to right direction
actor "User" as u
actor "Register_User" as ru
actor "Admin" as a
actor "Automation Orchestrator\n(n8n)" as N8N

rectangle {
usecase "Browse AI News" as UC1 #Yellow
usecase "Subscribe to Newsletter" as UC2
usecase "Receive Weekly Newsletter" as UC3
usecase "Search & Filter Tools" as UC4 #Yellow
usecase "Explore Learning Roadmaps" as UC5
usecase "Suggest New Tools/Sources" as UC6
usecase "Provide Feedback / Corrections" as UC7
usecase "Admin Panel" as UC8 #Yellow
usecase "Manage Database & Pipelines" as UC9 #Yellow
usecase "Manage Users & Roles" as UC10
usecase "Trigger Newsletter Run" as UC_TriggerNL #Yellow
usecase "Review/Edit/Publish  Articles" as UC11
Usecase "Unsubscribe from Newsletter" as UC12
}

u -- UC1
u -- UC4
u -- UC5
u -- UC2
ru -- UC3
ru -- UC12
u -- UC6
u -- UC7
a -- UC8
a -- UC9
a -- UC10
N8N -- UC_TriggerNL

UC2 ..> UC3 : <<include>>
UC8 <.. UC11 : <<include>>
u <.. ru : <<extend>>
@enduml