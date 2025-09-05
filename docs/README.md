# System Orchestration Repository  

This repository constitutes the **orchestration layer** for the integrated operation of three microservices developed as part of the **MVP project for the Third Sprint of the Full Stack Development postgraduate program at CCEC - PUC-Rio**. It provides a structured framework to facilitate local development, integration testing, and coordinated execution of the microservices architecture.  

The system orchestrates the following services:  

- **OrderAPI** (ASP.NET Core)  
- **LogisticsAPI** (ASP.NET Core)  
- **ProductAPI** (Flask)  

Each microservice resides in its **own dedicated GitHub repository** as per the project requirements. This orchestration repository consolidates them through **Docker Compose**, ensuring consistent and reproducible runtime environments.  

---  

## Repository Structure

```
system-orchestration/
│
├── docker-compose.yml    # Defines all services and their runtime configuration
├── .env                  # Centralized environment variables (ports, configs)
│
├── services/             # Git submodules linking to the microservice repositories
│   ├── orderapi/
│   ├── logisticsapi/
│   └── productapi/
│
└── docs/
    └── README.md
```

- The `services/` directory does **not contain original code**, but rather serves as a reference to external repositories via Git submodules.  
- Docker volumes are employed to **persist SQLite database files**, ensuring continuity of data across container lifecycles.  

---  

## Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/yourname/shopbridge_system-orchestration.git
cd shopbridge_system-orchestration
```

### 2. Initialize submodules
```bash
git submodule update --init --recursive
```
This command retrieves the code from the three microservice repositories into the `services/` directory.  

### 3. Launch the system
```bash
docker-compose up --build
```
This builds and starts all services (OrderAPI, LogisticsAPI, ProductAPI) with their local SQLite databases, providing an integrated environment suitable for development and testing.  

---  

## Service Endpoints

- **OrderAPI** → [http://localhost:5001](http://localhost:5001)  
- **LogisticsAPI** → [http://localhost:5002](http://localhost:5002)  
- **ProductAPI** → [http://localhost:5003](http://localhost:5003)  

Within the Docker Compose network, services can communicate with one another using their respective service names (`orderapi`, `logisticsapi`, `productapi`) as hostnames.  

---  

## Notes

- Each microservice maintains independence and can continue development within its own repository.  
- Updates to a microservice are integrated into this orchestration repository by **updating the respective submodule reference**.  
- SQLite databases are persisted via Docker volumes, guaranteeing data availability across container restarts.  

---  

## References

[1] S. Newman, *Building Microservices: Designing Fine-Grained Systems*. O’Reilly Media, 2015.  
