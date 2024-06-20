# Air Traffic Control System

## Overview
This repository contains a POSIX-compliant C program simulating an Air Traffic Control System. The system is comprised of the following entities:
- Planes (Passenger and Cargo)
- Airports
- Air Traffic Controller (ATC)
- Passengers
- Cleanup process

The system manages the departure and arrival of planes at different airports, with synchronization and communication between the entities using pipes and a single message queue.

## Features
- Simulates Passenger and Cargo planes with specific characteristics.
- Manages multiple airports, each with a configurable number of runways.
- Handles communication and synchronization between planes, airports, and ATC using POSIX IPC mechanisms.
- Implements a cleanup process to gracefully terminate the system.

## Getting Started

### Prerequisites
- Ubuntu 22.04
- GCC compiler

### Installation
Compile the programs:
    ```sh
    gcc -o plane plane.c -lpthread
    gcc -o airport airport.c -lpthread
    gcc -o airtrafficcontroller airtrafficcontroller.c -lpthread
    gcc -o cleanup cleanup.c -lpthread
    ```

## Usage

### Running the Programs

1. **Air Traffic Controller:**
    Start the air traffic controller process first.
    ```sh
    ./airtrafficcontroller
    ```

2. **Airports:**
    In separate terminals, start the airport processes. You need to run as many instances as specified in the air traffic controller.
    ```sh
    ./airport
    ```

3. **Planes:**
    In separate terminals, start the plane processes. Each plane will prompt for user input to specify its details.
    ```sh
    ./plane
    ```

4. **Cleanup:**
    Run the cleanup process to monitor and terminate the system.
    ```sh
    ./cleanup
    ```

### Input Details
- For each plane, provide the plane ID, type, number of occupied seats (for passenger planes), luggage weight, body weight, cargo details (for cargo planes), and airport numbers for departure and arrival.
- For each airport, provide the airport number and runway details including load capacities.
- The cleanup process will periodically ask if the system should terminate.

### Output
The system will output various status messages to the terminal, indicating the progress of plane departures, arrivals, and system termination. Additionally, the air traffic controller will log plane journeys to `AirTrafficController.txt`.

## Synchronization and Communication
- **Pipes:** Used for communication between passenger processes and their parent plane process.
- **Message Queue:** A single message queue is used for communication between planes, airports, and the air traffic controller.

## Constraints
- Use of POSIX-compliant IPC mechanisms.
- No additional sleep calls or shared memory.
- Proper synchronization using mutexes and semaphores.
- Error handling for system calls is mandatory.
