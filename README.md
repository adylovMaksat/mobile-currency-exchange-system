# Mobile Currency Exchange System

## Course
Networking Issues in Mobile Systems

## Project Overview
The Mobile Currency Exchange System is a mobile application that allows users to manage virtual currency wallets and perform simulated currency exchange transactions.

The application will provide user registration, login, current and historical exchange rates, simulated account funding, currency buying and selling, wallet balances, and transaction history.

Exchange rate information will be retrieved from the National Bank of Poland (NBP) API.

The system will consist of a mobile application, a web service, and a database. It will also handle unreliable mobile network connections, including timeouts, lost responses, offline access to cached information, and reconnection.

All financial operations are simulated. No real money will be transferred.

## Proposed Technologies
- Mobile Application: Flutter (Dart)
- Backend Web Service: Python (FastAPI)
- Database: SQLite
- External Data Source: National Bank of Poland (NBP) API
- Version Control: Git and GitHub
- Diagrams: diagrams.net (draw.io)

## Main System Components
1. Mobile Client — Displays exchange rates, wallets, transactions, and account information.
2. Web Service — Handles authentication, validation, exchange operations, and communication with the external API.
3. Database — Stores users, wallet balances, and transaction history.
4. NBP API — Provides current and historical exchange rates.

## Network Reliability
The application will display cached read-only data when the network is unavailable. New financial operations will be blocked while offline. If a response is lost after an operation is submitted, the client will check its status using a unique operation ID before retrying. The web service and database will prevent duplicate changes.

## Project Status
Lab 01 — Project setup and architecture in progress.
