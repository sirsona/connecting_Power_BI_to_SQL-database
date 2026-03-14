# Connecting Power BI To A SQL Database (PostgreSQL)

Power BI is a powerful business intelligence (BI) and data visualization tool
developed by Microsoft. It allows organizations to analyze data, build
interactive dashboards, and generate reports that help decision-makers understand
trends, patterns, and business performance.

In modern organizations, large volumes of operational and analytical data are
stored in databases. Instead of manually exporting this data into spreadsheets,
companies connect Power BI directly to databases, so reports can be updated
automatically. This connection enables analysts to build dashboards that always
reflect the latest data.

One of the most widely used database systems for storing analytical data is
PostgreSQL. PostgreSQL is an open-source relational database management system
known for its reliability, scalability, and strong SQL support. Companies use SQL
databases like PostgreSQL to store structured data such as sales, transactions,
customer records, and inventory information. When Power BI connects to these
databases, analysts can query and visualize the data efficiently.

## Connecting Power BI To A Local PostgreSQL Database

To begin analyzing data stored in PostgreSQL, you first connect Power BI Desktop
to the database.

### 1. Open Power BI Desktop

Start by opening Power BI Desktop on your computer. The Home ribbon provides
access to data connection tools.

### 2. Click Get Data

On the Home ribbon, click Get Data. Power BI supports many data sources including
Excel, CSV, cloud services, and databases. If PostgreSQL is not immediately
visible, click More to see the full list of connectors. Type PostgreSQL in the search bar and Power BI will immediately filter the results.

![Get Data](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/01l8w1teg6tv0i563fxm.png)

### 3. Choose PostgreSQL Database

Select PostgreSQL database from the available connectors.

Power BI will open a connection dialog where you enter database details

In the dialog box enter:

- Server: `localhost:5432`
- Database: database name (e.g., `company` )
- Data connectivity mode:
  - Import (load data into Power BI)
  - DirectQuery (queries the database live)

Then click OK.

![Connect Server](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3c0p1qeswfp4antuaqbx.png)

### 4. Provide Credentials

Power BI will ask for authentication details.

Enter:

- Username: PostgreSQL user
- Password: database password
- Authentication type: database

After entering credentials, click Connect.

### Select Tables to Load

![Loading Table](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2r9rnt6yf318nbhrly0y.png)

The Navigator window appears showing all tables and views in the PostgreSQL
database.

For example you might select:

- `customers`
- `products`
- `sales`
- `inventory`
  You can preview each table and then click Load to import the data into Power BI.

## Connecting Power BI to a Cloud PostgreSQL Database (Aiven)

Many companies store their databases in the cloud. One example is Aiven, which
provides managed PostgreSQL services.

Connecting Power BI to a cloud PostgreSQL instance is similar to connecting
locally, but it requires additional connection details.

### 1. Obtain Connection Details from Aiven

![Aiven Dashboard](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mq47yh73j1ozyagkhcje.png)

From the Aiven dashboard you will find:

- Host (database server address)
- Port (usually 19534)
- Database name
- Username
- Password

### 2. Download and Install the SSL Certificate

Aiven requires SSL encryption for all PostgreSQL connections. Because of this,
you must download the CA Certificate and install it on your machine before
connecting Power BI to the database.

#### Download the CA Certificate

- Open your Aiven service dashboard.
- Navigate to the connection information section.
- Download the CA Certificate file.

The certificate will usually download as a file named: `ca.pem`.
Windows expects to use the `.crt` extension. To make the certificate compatible,
rename the downloaded `ca.pem` file to `ca.crt`.

#### Install the Certificate in Windows

- Double click the `ca.crt`.
- The Certificate window will open.
- Click Install Certificate.
- Choose Local Machine.
- Select Place all certificate in the following store.
- Choose Trusted Root Certification Authorities.
- Finish the installation.

### 3. Connect Using Power BI

- Open Power BI Desktop.
- Click Get Data from Home tab.
- Use the search bar to search for PostgreSQL database.
- Select it and click Connect.

![Aiven Connection](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/g00j7985moxpzykbebzj.png)

In the connection window, enter the following details from the Aiven dashboard:

- Server: `pg_12345-user.aivencloud.com:19534`
- Database name: `company`
  Click OK.

![Aiven Username](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b9o95nt4ldd00n58b9it.png)
Power BI will then prompt you for authentication.

Enter:

- Username
- Password

and select database authentication, then click Connect.

![Aiven Loading Tables](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/iy1noaemu8dr9msmg3z7.png)

Because the CA Certificate was installed earlier, Windows already trusts the
Aiven server, allowing Power BI to establish a secure SSL connection
automatically.

Once the connection succeeds, the Navigator window will appear showing the
available tables in your database, ready for you to select and load.
