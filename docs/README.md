# System Orchestration Repository

This repository provides the orchestration layer for running the three microservices of the project:  

- **OrderAPI** (ASP.NET Core)  
- **LogisticsAPI** (ASP.NET Core)  
- **ProductAPI** (Flask)  

Each microservice is contained in its **own GitHub repository** as required. This repository brings them together through Docker Compose for local development and integration testing.

---

## Repository Structure

```
system-orchestration/
│
├── docker-compose.yml    # Defines all services and their runtime configuration
├── .env                  # Centralized environment variables (ports, configs)
│
├── services/             # Git submodules pointing to the microservice repos
│   ├── orderapi/
│   ├── logisticsapi/
│   └── productapi/
│
└── docs/
    └── README.md
```

- The `services/` directory does not contain original code; instead, it links to external repositories via Git submodules.  
- Volumes are used to persist SQLite database files for each service.  

---

## Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/yourname/system-orchestration.git
cd system-orchestration
```

### 2. Initialize submodules
```bash
git submodule update --init --recursive
```
This pulls the code from the three microservice repositories into the `services/` folder.

### 3. Run the system
```bash
docker-compose up --build
```

This command builds all services (OrderAPI, LogisticsAPI, ProductAPI) and starts them with their local SQLite databases.  

---

## Service Endpoints

- **OrderAPI** → [http://localhost:5001](http://localhost:5001)  
- **LogisticsAPI** → [http://localhost:5002](http://localhost:5002)  
- **ProductAPI** → [http://localhost:5003](http://localhost:5003)  

Inside the Docker Compose network, services can call each other using their service names (`orderapi`, `logisticsapi`, `productapi`) as hostnames.

---

## Notes

- Each microservice can still be developed independently in its own repository.  
- Updates to a microservice should be pulled into the orchestration repo by updating its submodule reference.  
- SQLite databases are persisted in Docker volumes, so data will survive container restarts.  

---

## References

[1] S. Newman, *Building Microservices: Designing Fine-Grained Systems*. O’Reilly Media, 2015.  
