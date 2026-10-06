# HR & Transport Management System

A Java console application for a retail chain, made of two modules that share one PostgreSQL database:

- **HR module**: employees, roles, weekly shift scheduling, employee availability constraints, employment contracts and reports.
- **Transport module**: transport requests, trucks, drivers and delivery scheduling.

Built as a university team project (Analysis and Design of Software Systems, team of four).

**My part:** I designed and built the HR module, and the integration layer between HR and Transport.

## Features

### HR module
- Login by employee ID and password, with a menu that depends on the user's role
- Three permission levels: **employee**, **shift manager** and **HR manager**
- Employees can view their shifts, submit and edit weekly availability constraints, and view their contract and personal details
- HR managers can manage employees and roles, build weekly shift schedules and generate reports

### HR ↔ Transport integration
When a transport is planned for the following week, the system automatically finds the matching shift and opens a driver slot in it, based on:
- the driving license the transport requires
- the departure branch
- the shift time

The integration talks to the Transport module through an interface (`ITransportController`), so the two modules stay loosely coupled.

## Architecture

Each module is organized in layers:

```
Presentation  →  Service  →  Domain  →  Repository / DAO  →  PostgreSQL
                                 ↕
                                DTO
```

## Tech stack

- Java, Maven
- PostgreSQL (via JDBC)
- Log4j2 for logging
- JUnit 5, Mockito and AssertJ for unit and integration tests

## Getting started

### Prerequisites
- JDK 22 (as set in `pom.xml`)
- IntelliJ IDEA (recommended) and Maven
- A local PostgreSQL server on `localhost:5432`

The database connection settings are in `dev/HR_Mudol/DataBase/PostgresConnection.java`.

### Build and run
The project is set up for IntelliJ IDEA, with `dev/` as the source folder and `test/` as the test folder (Maven is used for dependencies).

1. Open the project in IntelliJ IDEA and let Maven download the dependencies.
2. Make sure PostgreSQL is running.
3. Run `Main`.

On startup you can choose to load existing data from the database or start with an empty system, and then open the HR menu or the Transport menu.

### Run the tests
Right-click the `test/` folder in IntelliJ IDEA and choose **Run 'All Tests'**.

## Project structure

```
dev/
  Main.java              entry point (choose HR or Transport)
  HR_Mudol/              HR module
    presentation/        console menus
    Service/             business logic and the HR–Transport integration
    domain/              employees, roles, shifts, constraints
    DAO/  DTO/           database access and data transfer objects
    DataBase/            PostgreSQL connection and initialization
  TransportModule/       Transport module
test/
  HRModule/              HR unit and integration tests
```
