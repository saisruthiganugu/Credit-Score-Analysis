
# Credit Score Tool

**Credit Score Analysis Tool** is a project developed for Swedbank in Sweden. The primary objective is to automate the credit score evaluation process by integrating data from various sources, including credit bureaus and banking transaction records. This tool provides real-time credit scoring, predictive analytics based on customer behavior, and detailed reporting features for bank staff. It is designed using a microservices architecture, ensuring scalability and efficient management of different service components.

## Features

### 1. User Interaction and Authentication

- **Action**: A bank officer logs into the system through the User Interface. Only bank officers can access the application and serve users.
- **Process**:
  - The User Management Service handles the login request, authenticating user credentials against the database.
  - Upon successful authentication, an access token (using OAuth) is generated for secure sessions.
  - For any API request, the access token is sent to the server for authorization.

### 2. Data Collection and Processing

- **Action**: The bank officer initiates a credit score check for a client.
- **Process**:
  - The Data Collection Service gathers financial data from internal databases (account and loan histories) and external credit bureaus (third-party systems).
  - This service validates and preprocesses the data (e.g., normalizing formats, removing duplicates) to prepare it for analysis.

### 3. Credit Scoring Calculation

- **Action**: Processed data is forwarded to the Credit Scoring Service.
- **Process**:
  - The Credit Scoring Service applies a scoring model, which may include statistical algorithms and machine learning to evaluate credit risk based on historical data.
  - The resulting credit score and detailed analytics are sent to the Report Service.

### 4. Report Generation and Delivery

- **Action**: Generation of a credit report based on the calculated score.
- **Process**:
  - The Report Service fetches the score and analysis from the Credit Scoring Service.
  - It compiles a detailed credit report, which may include recommendations or flags for high-risk factors.
  - The report is made available to the bank officer via the UI and can also be sent to other stakeholders via email using Java email service.

### Common Activities

- All data transactions and user actions are logged and can be seen on Splunk (Logging Tool).
- All interactions between the client (browser) and the microservices go through the Spring Cloud Gateway, which routes requests, handles load balancing, and provides an additional layer of security.
- For real-time data updating operations, such as credit score calculation, Kafka is used.

## Usage

To use the Credit Score Tool, follow these steps:

1. **Login**: A bank officer logs into the system using their credentials.
2. **Initiate Credit Score Check**: Select a client and initiate a credit score check.
3. **Review Reports**: Access the generated credit report and analytics through the UI. Reports can also be sent via email to relevant stakeholders.

## Technologies Used

- **Backend**: Java
- **Database**: MySQL
- **Cache**: Redis
- **Logging**: Log4j2, Splunk
- **Messaging**: Kafka
- **API Gateway**: Spring Cloud Gateway
