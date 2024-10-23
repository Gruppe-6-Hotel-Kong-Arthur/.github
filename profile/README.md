# Hotel Kong Arthur - Group 6

## Overview

Welcome to the **Hotel Kong Arthur - Group 6** GitHub Organization. Our team is tasked with developing an advanced data analytics platform for Hotel Kong Arthur to help optimize their operations. The system will enable hotel decision-makers to analyze key operational data in real time, providing insights on occupancy rates, revenue, customer satisfaction, and other important metrics.

This project leverages a microservice architecture to ensure scalability and flexibility. The backend is built using **Python** and **Flask**, and data is exchanged in **JSON** format. For data visualization, we are integrating **Tableau** to provide clear, actionable insights.

## Project Goals

- **Optimize Hotel Operations**: Provide real-time data analysis on key hotel metrics.
- **Microservice Architecture**: Design the system as independent services that can be updated or scaled individually.
- **Technologies**: Python, Flask, JSON (CSV) for data exchange, and Tableau for data visualization.
- **Live Data Handling**: Build a system that updates and shows data in real time, moving away from the historical, static data found in the current system.

For a detailed description of the project requirements, visit our [Trello Board](https://trello.com/invite/b/6718aabe0e15a2c0ca0d5252/ATTIb2bb54308eb271203b88bb8a689a499b378BCD22/hotel-kong-arthur-group-6).

## Repository Structure

Each repository within this organization follows a **microservice pattern**, where each microservice is self-contained and fulfills a specific business function, such as managing guest data, room availability, or booking information. Below is an overview of our planned services:

### Microservices Overview

- **Guest Service**: Handles guest registration, profile updates, and preferences.
- **Booking Service**: Manages room reservations, check-ins, and check-outs.
- **Room Service**: Manages room availability, types, and pricing.
- **Drink Service**: Handles drink orders from the bar, inventory, and billing for room service.
- **Drink Unit Sold Service**: Tracks the number of drink units sold to ensure accurate inventory and financial reporting.

## Data Sources

Our project integrates historical hotel data for development purposes, but the final system will handle live data feeds. Example data can be found in this repository: [Hotel Data](https://github.com/ITAKEA/hoteldata).

## Key Technologies

- **Backend**: Python (Flask)
- **Data Format**: JSON, CSV
- **Data Visualization**: Tableau
- **Architecture**: Microservices
- **Containerization**: Docker (for development and deployment)

## Project Management

All project tasks, progress, and backlog items are tracked via our **Trello Board**. You can access the board [here](https://trello.com/invite/b/6718aabe0e15a2c0ca0d5252/ATTIb2bb54308eb271203b88bb8a689a499b378BCD22/hotel-kong-arthur-group-6).

## Team Members

| Name              | Role               | GitHub Profile                               |
|-------------------|--------------------|----------------------------------------------|
| **Marcus**        | Lead Developer      | [marcus-rk](https://github.com/marcus-rk)    |
| **Christian**     | Lead Developer  | [ChristianBT96](https://github.com/ChristianBT96) |
