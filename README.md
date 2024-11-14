# Overview

This project is a **Property Management Services** application that allows landlords and tenants to interact, manage properties, applications, and communicate via an integrated mailbox system. It supports property listing, rental applications, and in-app messaging between tenants and landlords.

## Installation Instructions

To get this project running locally, follow these steps:

### 1. Clone the repository:

```bash
git clone https://github.com/Nima-goharian/tenant-landlord-management-system
```

### 2. Navigate to the project directory:

```bash
cd tenant-landlord-management-system
```

### 3. Install the required npm packages:

```bash
npm install
```

### 4. Database Setup:

Ensure PostgreSQL is running on your system (you can use PG Admin to set it up).

1. Create a PostgreSQL database:

   ```sql
   CREATE DATABASE tenant_landlord_system;
   ```

2. Create the tables as described below:

#### Database Schema

**3.1 `users` Table:**

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  google_id VARCHAR(255),
  name CHAR(255),
  email CHAR(255),
  role CHAR(50),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**3.2 `tenant_landlord` Table:**

```sql
CREATE TABLE tenant_landlord (
  landlord_id INT,
  tenant_id INT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (landlord_id, tenant_id)
);
```

**3.3 `property_applications` Table:**

```sql
CREATE TABLE property_applications (
  application_id SERIAL PRIMARY KEY,
  property_id INT,
  tenant_id INT,
  full_name CHAR(255),
  contact_number CHAR(20),
  email CHAR(255),
  employer_name CHAR(255),
  job_title CHAR(255),
  monthly_income NUMERIC(10, 2),
  length_of_stay CHAR(50),
  number_of_occupants INT,
  pets CHAR(255),
  emergency_contact CHAR(255),
  emergency_contact_number CHAR(20),
  application_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  status CHAR(50)
);
```

**3.4 `properties` Table:**

```sql
CREATE TABLE properties (
  id SERIAL PRIMARY KEY,
  landlord_id INT,
  address CHAR(255),
  price NUMERIC(10, 2),
  bedrooms INT,
  bathrooms FLOAT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**3.5 `mailbox` Table:**

```sql
CREATE TABLE mailbox (
  message_id SERIAL PRIMARY KEY,
  sender_id INT,
  receiver_id INT,
  subject CHAR(255),
  message_content TEXT,
  sent_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Set Up Environment Variables

Create a `.env` file in the root directory and add the following configuration:

```bash
GOOGLE_CLIENT_ID="your-google-client-id"
GOOGLE_CLIENT_SECRET="your-google-client-secret"
SESSION_SECRET="your-session-secret"
PG_USER="your-postgresql-username"
PG_HOST="localhost"
PG_DATABASE="tenant_landlord_system"
PG_PASSWORD="your-database-password"
PG_PORT="5432"
CONTACT_US_EMAIL="your-contact-email"
CONTACT_US_PASSWORD="your-contact-email-password"
```

> **Note:** Replace the placeholder values with your actual credentials.

## Run the Application

Start the server with the following command:

```bash
nodemon index.js
```

Navigate to `http://localhost:3000` in your browser to view the application.

# fake-payment-gateway

## Dummy payment gateway for testng purposes. Can pay using card details as well as using the phone number.

fake-payment-gateway, that handle

- payment via card details
- payment via phone number
- each payment send email notification for customer
- can fetch all card/ phone payment history

## Tech

---

fake-payment-gateway uses:

- [JavaScript]
- [NodeJS]
- [KoaJS]

## Installation

1. download the project.

   ```bash
   git@github.com:ShalithaCell/fake-payment-gateway.git
   ```

   or

   ```bash
   https://github.com/ShalithaCell/fake-payment-gateway.git
   ```

2. Goto inside to '_fake-payment-gateway_' folder and run the command.

   ```bash
    npm install
   ```

3. Configure email sender

   - create .env file in project root folder. execute following command,

     In windows

     ```
     cd > .env
     ```

     In Mac/ Linux

     ```
      touch .env
     ```

   - add following code to the .env file with your email address credentials,

     ```
     MAIL_SENDER_IDENTITY="please enter your email address here"
     MAIL_SENDER_PASSWORD="please enter your email password here"
     ```

   - make sure you should enable, less secure apps in gmail account. \* [How to enable less secure apps](https://support.google.com/a/answer/6260879?hl=en)

4. Run the Project

   ```bash
   npm run start
   ```

---

## How to use

- [x] Before integration the fake-payment gateway, please simulate the api end-points using the postman.
      You can find the Postman collection inside the **_doc_** folder.

You can get all api end-points invoking the following link,

- [http://localhost:5100/api/](http://localhost:5100/api/)

1. For card payment
   - url : [http://localhost:5100/api/v1/payment/card](http://localhost:5100/api/v1/payment/card)
   - type : POST
   - sample request body :
   ```json
   {
     "app_name": "ABC",
     "service": "Electronic Items",
     "customer_email": "shalithax@gmail.com",
     "card_type  ": "VISA",
     "card_holder_name": "Example",
     "card_number": "4242424242424242",
     "expiryMonth": "01",
     "expiryYear": "2020",
     "cvv": "123",
     "amount": "5000.00",
     "currency": "USD"
   }
   ```
2. For payment using phone number
   - url : [http://localhost:5100/api/v1/payment/phone](http://localhost:5100/api/v1/payment/phone)
   - type : POST
   - sample request body :
   ```json
   {
     "app_name": "ABC",
     "service": "Electronic Items",
     "customer_email": "shalithax@gmail.com",
     "phone_number  ": "0771940055",
     "phone_holder_name": "shalitha",
     "amount": "5000.00",
     "currency": "USD"
   }
   ```
3. Get card payment transaction history
   - url : [http://localhost:5100/api/v1/payment/card](http://localhost:5100/api/v1/payment/card)
   - type : GET
4. Get phone payment transaction history
   - url : [http://localhost:5100/api/v1/payment/phone](http://localhost:5100/api/v1/payment/phone)
   - type : GET

---

## Development

---

Want to contribute? Great!

- I'm here for your pull-request.

The best way to contribute is by spreading the word about the library:

- Blog it
- Comment it
- Fork it
- Star it
- Share it

## License

---

MIT

**Free Software, Hell Yeah!**

[javascript]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/
[nodejs]: https://nodejs.org/en/
[koajs]: https://koajs.com/
