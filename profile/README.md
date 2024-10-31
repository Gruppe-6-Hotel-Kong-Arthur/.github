# Hotel Kong Arthur - Group 6

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Flask](https://img.shields.io/badge/flask-%23000.svg?style=for-the-badge&logo=flask&logoColor=white)
![SQLite](https://img.shields.io/badge/sqlite-%2307405e.svg?style=for-the-badge&logo=sqlite&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=tableau&logoColor=white)

## Overview

Welcome to the **Hotel Kong Arthur - Group 6** GitHub Organization. Our team is tasked with developing an advanced data analytics platform for Hotel Kong Arthur to help optimize their operations. The system will enable hotel decision-makers to analyze key operational data in real time, providing insights on occupancy rates, revenue, customer satisfaction, and other important metrics.

This project leverages a microservice architecture to ensure scalability and flexibility. The backend is built using **Python** and **Flask**, and data is exchanged in **JSON** formatted and can export **CSV** format. For data visualization, we are integrating **Tableau** to provide clear, actionable insights.

## Project Goals

- **Optimize Hotel Operations**: Provide real-time data analysis on key hotel metrics.
- **Microservice Architecture**: Design the system as independent services that can be updated or scaled individually.
- **Technologies**: Python, Flask, JSON (CSV) for data exchange, and Tableau for data visualization.
- **Live Data Handling**: Build a system that updates and shows data in real time, moving away from the historical, static data found in the current system.

For a detailed description of the project requirements, visit our [Trello Board](https://trello.com/invite/b/6718aabe0e15a2c0ca0d5252/ATTIb2bb54308eb271203b88bb8a689a499b378BCD22/hotel-kong-arthur-group-6) and project description [Analyse af Hoteldata med Microservices, Tableau, SCRUM](https://github.com/user-attachments/files/17489442/Analyse.af.Hoteldata.med.Microservices.Tableau.Scrum.pdf).

## Repository Structure

Each repository within this organization follows a **microservice pattern**, where each microservice is self-contained and fulfills a specific business function, such as managing guest data, room availability, or booking information. Below is an overview of our planned services:

### Microservices Overview

- **Guest Service**: Handles guest registration, profile updates, and preferences.
- **Reservation Service**: Manages room reservations/bookings, check-ins, and check-outs.
- **Room Inventory Service**: Manages room availability, types, and pricing.
- **Drink Service**: Handles drink orders from the bar, inventory, and billing for room service.
- **Drink Sales Service**: Tracks the number of drink units sold to ensure accurate inventory and financial reporting.
- **CSV Export Service**: Generates CSV files for data visualization from the aggregated data of various services. Ensures data is formatted correctly for tools like Tableau.
- **Hotel API Gateway**: Acts as a single entry point for client applications, routing requests to the appropriate microservices.

---

```mermaid
flowchart TD
    %% Microservices and Interactions
    subgraph API_Gateway
        HotelAPI[Hotel API Gateway]
    end

    subgraph GuestService
        GuestsTable[Guests]
        CountriesTable[Countries]
    end

    subgraph ReservationService
        ReservationsTable[Reservations]
    end

    subgraph RoomInventoryService
        RoomTypesTable[RoomTypes]
        RoomsTable[Rooms]
        SeasonsTable[Seasons]
        SeasonDatesTable[SeasonDates]
    end

    subgraph DrinkService
        CategoriesTable[Categories]
        DrinksTable[Drinks]
    end

    subgraph DrinkSalesService
        DrinkSalesTable[DrinkSales]
    end

    subgraph CSVExportService
        CSVExport[CSV Export Service]
    end

    %% External Client Requests
    Client[Client Application] --> HotelAPI

    %% API Gateway to Microservices
    HotelAPI --> GuestService
    HotelAPI --> ReservationService
    HotelAPI --> RoomInventoryService
    HotelAPI --> DrinkService
    HotelAPI --> DrinkSalesService
    HotelAPI --> CSVExportService

    %% Microservices to Databases
    GuestService --> GuestsTable
    GuestService --> CountriesTable

    ReservationService --> ReservationsTable
    ReservationService --> RoomsTable
    ReservationService --> GuestsTable
    ReservationService --> SeasonsTable

    RoomInventoryService --> RoomTypesTable
    RoomInventoryService --> RoomsTable
    RoomInventoryService --> SeasonsTable
    RoomInventoryService --> SeasonDatesTable

    DrinkService --> CategoriesTable
    DrinkService --> DrinksTable

    DrinkSalesService --> DrinkSalesTable
    DrinkSalesService --> DrinksTable

    CSVExportService --> GuestsTable
    CSVExportService --> ReservationsTable
    CSVExportService --> RoomTypesTable
    CSVExportService --> DrinksTable
    CSVExportService --> DrinkSalesTable

    %% Table Relationships
    %% RoomTypesTable ||--o{ RoomsTable : contains
    %% SeasonsTable ||--o{ SeasonDatesTable : "contains"
    %% GuestsTable }o--|| CountriesTable : "resides in"
    %% CategoriesTable ||--o{ DrinksTable : "includes"
```



---
```mermaid
erDiagram
    RoomTypes ||--o{ Rooms : contains
    Seasons ||--o{ SeasonDates : contains
    Guests }o--|| Countries : "resides in"
    Categories ||--o{ Drinks : "includes"

    RoomTypes {
        INTEGER id PK
        TEXT type_name UK
        REAL base_price
        INTEGER max_count
    }

    Rooms {
        INTEGER id PK
        INTEGER room_type_id FK
        INTEGER availability
    }

    Reservations {
        INTEGER id PK
        INTEGER guest_id FK
        INTEGER room_id FK
        INTEGER season_id FK
        DATE start_date
        DATE end_date
        REAL price
    }

    Seasons {
        INTEGER id PK
        TEXT season_type UK
        REAL multiplier
    }

    SeasonDates {
        INTEGER id PK
        INTEGER season_id FK
        DATE start_date
        DATE end_date
    }

    Guests {
        INTEGER id PK
        TEXT first_name
        TEXT last_name
        INTEGER country_id FK
    }

    Countries {
        INTEGER id PK
        TEXT name UK
    }

    Categories {
        INTEGER category_id PK
        TEXT category_name UK
    }

    Drinks {
        INTEGER drink_id PK
        TEXT drink_name
        INTEGER category_id FK
        REAL price_dkk
    }

    DrinkSales {
        INTEGER drink_id FK
        INTEGER units_sold NOT NULL
    }
```

## Data Sources

Our project integrates historical hotel data for development purposes, but the final system will handle live data feeds. Example data can be found in this repository: [Hotel Data](https://github.com/ITAKEA/hoteldata).

## Key Technologies

- **Backend**: Python with Flask and SQLite
- **Data Format**: JSON, CSV
- **Data Visualization**: Tableau
- **Architecture**: Microservices
- **Containerization**: Docker (for development and deployment)

### Steps for Setting Up and Running Services

#### 1. Clone Repositories

In your terminal, clone each microservice repository:

```bash
# Clone each repository and enter the base folder
git clone https://github.com/Gruppe-6-Hotel-Kong-Arthur/HotelAPIGateway.git
git clone https://github.com/Gruppe-6-Hotel-Kong-Arthur/CSVExportService.git
git clone https://github.com/Gruppe-6-Hotel-Kong-Arthur/DrinkSalesService.git
git clone https://github.com/Gruppe-6-Hotel-Kong-Arthur/DrinkService.git
git clone https://github.com/Gruppe-6-Hotel-Kong-Arthur/ReservationService.git
git clone https://github.com/Gruppe-6-Hotel-Kong-Arthur/GuestService.git
git clone https://github.com/Gruppe-6-Hotel-Kong-Arthur/RoomInventoryService.git
```

#### 2. Build the Docker Images

Navigate to each microservice directory and build its Docker image, pruning unused images after the build:

```bash
# Build HotelAPIGateway
cd HotelAPIGateway
docker build -t hotel_api_gateway . && docker image prune -f
cd ..

# Build CSVExportService
cd CSVExportService
docker build -t csv_export_service . && docker image prune -f
cd ..

# Build DrinkSalesService
cd DrinkSalesService
docker build -t drink_sales_service . && docker image prune -f
cd ..

# Build DrinkService
cd DrinkService
docker build -t drink_service . && docker image prune -f
cd ..

# Build ReservationService
cd ReservationService
docker build -t reservation_service . && docker image prune -f
cd ..

# Build GuestService
cd GuestService
docker build -t guest_service . && docker image prune -f
cd ..

# Build RoomInventoryService
cd RoomInventoryService
docker build -t room_inventory_service . && docker image prune -f
cd ..
```

#### 3. Create a Docker Network

Create a custom Docker network for inter-service communication:

```bash
docker network create microservice-network
```

#### 4. Run the Docker Containers

Run each service in a container, linking them to the `microservice-network` and pruning stopped containers:

```bash
# Run HotelAPIGateway
docker run -d \
  --name hotel_api_gateway \
  --network microservice-network \
  -p 5000:5000 \
  hotel_api_gateway && docker container prune -f

# Run CSVExportService
docker run -d \
  --name csv_export_service \
  --network microservice-network \
  -p 5001:5001 \
  csv_export_service && docker container prune -f

# Run DrinkSalesService
docker run -d \
  --name drink_sales_service \
  --network microservice-network \
  -p 5002:5002 \
  drink_sales_service && docker container prune -f

# Run DrinkService
docker run -d \
  --name drink_service \
  --network microservice-network \
  -p 5003:5003 \
  drink_service && docker container prune -f

# Run ReservationService
docker run -d \
  --name reservation_service \
  --network microservice-network \
  -p 5004:5004 \
  reservation_service && docker container prune -f

# Run GuestService
docker run -d \
  --name guest_service \
  --network microservice-network \
  -p 5005:5005 \
  guest_service && docker container prune -f

# Run RoomInventoryService
docker run -d \
  --name room_inventory_service \
  --network microservice-network \
  -p 5006:5006 \
  room_inventory_service && docker container prune -f
```

#### 5. Verify Running Containers

Check that all services are running correctly:

```bash
docker ps
```

Or you can use Docker Desktop to verify the containers are running and connected to the `microservice-network`.


## Project Management

All project tasks, progress, and backlog items are tracked via our **Trello Board**. You can access the board [here](https://trello.com/invite/b/6718aabe0e15a2c0ca0d5252/ATTIb2bb54308eb271203b88bb8a689a499b378BCD22/hotel-kong-arthur-group-6).

## Team Members

| Name              | Role               | GitHub Profile                               |
|-------------------|--------------------|----------------------------------------------|
| **Marcus**        | Lead Developer      | [marcus-rk](https://github.com/marcus-rk)    |
| **Christian**     | Lead Developer      | [ChristianBT96](https://github.com/ChristianBT96) |
