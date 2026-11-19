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

## User Journeys

### Normal Journey 1: View Exchange Rates
1. The user opens the mobile application.
2. The mobile client requests exchange rates from the web service.
3. The web service retrieves current exchange rates from the NBP API.
4. The service returns the rates to the mobile application.
5. The application displays the rates and their update time.

### Normal Journey 2: Buy Currency
1. The user logs in.
2. The user selects a currency and enters an amount.
3. The mobile client sends a buy request with a unique operation ID.
4. The web service validates the request and available balance.
5. The database records the transaction and updates wallet balances atomically.
6. The service confirms the result to the mobile client.
7. The application displays the updated wallet balances.

### Interrupted Journey 1: Connection Lost While Viewing Rates
1. The user opens the exchange rates screen.
2. The internet connection becomes unavailable before the request completes.
3. The application displays previously cached rates, if available.
4. Cached information is labelled with its last update time.
5. When connectivity returns, the application retrieves fresh data.

### Interrupted Journey 2: Connection Lost After Buy Request
1. The user submits a currency purchase with a unique operation ID.
2. The server may complete the transaction, but its response is lost.
3. The application displays the operation status as unknown or pending confirmation, not successful.
4. After reconnection, the client checks the operation status using the same ID.
5. The service returns the authoritative result.
6. Repeating the same operation ID must not create a second transaction.

## Initial Network Risk List

| Risk | Impact | Planned Mitigation |
|---|---|---|
| Lost internet connection | Rates cannot be refreshed | Display timestamped cached rates |
| Slow network response | Long waiting time | Timeout and loading indicators |
| Lost transaction response | Unknown operation outcome | Query operation status after reconnection |
| Duplicate request | Duplicate currency exchange | Unique operation ID and server-side duplicate protection |
| Stale cached rates | User sees outdated information | Display cache age and require server validation for exchanges |
| Concurrent transactions | Incorrect wallet balances | Atomic database transactions and balance validation |
| NBP API unavailable | Exchange rates cannot be refreshed | Show an error and cached read-only rates |
