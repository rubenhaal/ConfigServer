## 🌍 Languages
- [English](#English)
- [Deutsch](#Deutch)

## English

#  Spring Cloud Config Server

This project is a **Spring Cloud Config Server** that serves configuration files to client applications (e.g., `dummy-service`).  
We use the **native backend**, meaning configuration files (`.yml`) are read from a local `config/` directory.

---

## Architecture

```text
(Client Service) ---> (Config Server) ---> (Local YML configuration files)
```

**Config Server**: Central point that exposes configuration over HTTP.

**Clients**: Fetch their configuration at startup from the Config Server.

**Configuration files**: Stored locally in config/ for this demo (later can be moved to Git).


## How to Run

1. Start like a normal springboot service.

2. Test the endpoint (serving configuration for dummy-service in dev profile):
curl http://localhost:8888/dummy-service/dev

You should get a JSON payload with properties like app.message and server.port.

### Configuration
``` 
config-server/
├─ build.gradle
├─ src/main/java/.../ConfigServerApplication.java
├─ src/main/resources/application.yml
└─ config/
├─ application.yml
└─ dummy-service-dev.yml
```
### application.yml (server configuration)

```  
server:
port: 8888

spring:
profiles:
active: native   # Use local files instead of Git
cloud:
config:
server:
native:
# Path to the folder with YML configuration
search-locations: file:./config

management:
endpoints:
web:
exposure:
include: "*"
endpoint:
health:
show-details: always
``` 

### Example config files in config/

Common file (applies to all services):
```
# application.yml
logging:
level:
root: INFO
```

### Service-specific file (dummy-service-dev.yml):
```
# Configuration for dummy-service with 'dev' profile
app:
message: "Hello from Config Server local (dev profile) 👋"
server:
port: 8081
```

## Deutch


#  Spring Cloud Config Server

Bei diesem Projekt handelt es sich um einen **Spring Cloud config Server**, der Konfigurationsdateien as Client-Anwendungen (z.B Dummy-Service) bereitstellt.
Wir verwenden das native Backend, d.h. Konfigurationsdatein (.yml) werden aus einem  localen config/ Verzeichnis gelesen

---

## 🧩 Architecture

```text
(Client Service) ---> (Config Server) ---> (Local YML configuration files)
```

**Config Server**: Zentraler Punkt, der die Konfiguration über HTTP verfügbar macth.

**Clients**: Rufen Sie ihre Konfiguration beim Stat vom Konfigurationsserver ab.

**Configuration files**: Für diese Demo lokal config/ gespeichert (kann später nach git verschoben werden)


## Anwendung starten

1. Starten Sie den Dienst wie einen normalen Spring-Boot-Service.

2. Testen Sie den Endpoint (stellt die Konfiguration für dummy-service im dev-Profil bereit):

   curl http://localhost:8888/dummy-service/dev

Sie sollten eine JSON-Antwort mit Eigenschaften wie app.message und server.port erhalten.

### Konfiguration
``` 
config-server/
├─ build.gradle
├─ src/main/java/.../ConfigServerApplication.java
├─ src/main/resources/application.yml
└─ config/
├─ application.yml
└─ dummy-service-dev.yml
```
### application.yml (server configuration)

```  
server:
port: 8888

spring:
profiles:
active: native   # Use local files instead of Git
cloud:
config:
server:
native:
# Path to the folder with YML configuration
search-locations: file:./config

management:
endpoints:
web:
exposure:
include: "*"
endpoint:
health:
show-details: always
``` 

### Beispielkonfigurationsdateien im Verzeichnis config/

Common file (applies to all services):
```
# application.yml
logging:
level:
root: INFO
```

### Service-specific file (dummy-service-dev.yml):
```
# Configuration for dummy-service with 'dev' profile
app:
message: "Hello from Config Server local (dev profile) 👋"
server:
port: 8081
```