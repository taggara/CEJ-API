**CEJ: Transaction API**

**Components**

Bottle Application:
- Handles routes such as `/cej/login`, `/cej/auth`, and `/cej/transactions`.
- Integrates with OAuth2 for authentication via Azure AD.
- Uses session management with Beaker middleware.
- Reads configurations from `oauth-prod.json` and `db-prod.json`.
Transaction Processor:
- Processes raw transaction data.
- Validates transactions against a predefined JSON schema.
Database:
- PostgreSQL accessed via `pg8000`.
- Configuration parameters (host, database name, user, password) stored in `db-prod.json` and `db-qa.json`.
Logging:
- Centralized logging for API and transaction processing activities.
Py4J Gateway:
- Provides entry point for Apache Tomcat integration.
- Facilitates script execution from a Java environment.

**Data Flow**

1. User Authentication:
- User access ` `. A check is done for a current token.\cej\transactions
- User is redirected to `/cej/login`, triggering OAuth2 authorization flow.
- Azure AD is used for authentication.
QA: GK CEJ-OAuth-QUA - Microsoft Azure
Production: GK CEJ - Production-OAuth-PRD - Microsoft Azure
The custom API uses the Bottle web framework and integrates several components to handle user authentication, transaction processing, and
database interactions. It also supports integration with Apache Tomcat via the Py4J gateway.
This architecture ensures secure authentication, efficient transaction processing, and smooth integration with existing Java-based infrastructure.
- Azure AD redirects back to `/cej/auth` with the authorization code.
- API exchanges authorization code for an access token and stores them within the session.
2. Transaction Processing
- Authenticated user accesses `/cej/transactions`.
- API retrieves transaction data from PostgreSQL.
- Raw transaction data is processed and validated by the `transaction_processor`.
3. Integration with Apache Tomcat:
- `python_entry_point.py` initializes a Py4J gateway.
- Allows Tomcat to invoke Python scripts for transaction processing.

**Use Cases**

1. Retail Applications - Sales Data Integration
