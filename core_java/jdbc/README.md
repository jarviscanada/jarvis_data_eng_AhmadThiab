# Introduction
This app uses data access-designed patterns for CRUD operations (create, save, update, delete). The objective is to seperate the technical details of data access from the rest of the application.
The app also uses JDBC as its relational database API to connect and work with a PostgreSQL database. To do so, Apache Maven build tool is used to add the PSQL JDBC driver dependency. Finally,
Docker

# Implementaiton
## ER Diagram
![My image](C:\Users\Hams\Downloads\ERDiagram.PNG)
## Design Patterns
Discuss DAO and Repository design patterns (150-200 words)
This app contains the following:
- `DatabaseConnectionManager` class which leverages a JDBC driver for handling all the connections to our Database using the DriverManager object.
- `JDBCExecutor` class which uses the `DatabaseConnectionManager` previously defined to set up a connection and run different CRUD operations.
- `DataAccessObject` abstract class which extends `DataTransferObject` where we define several abstract methods such as findById, findAll, update, create, delete and getLastVal method that will be uses to get the last value of a sequence using unique primary key incrementation.
- `DataTransferObject` interface which simply contains a getId method.
- `Customer` class which is nothing more than a data representation of the customer table that implements the `DataTransferObject` interface.
- `CustomerDAO` class which extends `DataAccessObject` and implements the different abstract method in it.
- `order` class which contains the customer information, sales person information, order specific information and a list of OrderLine objects. This class also implements the `DataTransferObject` interface.
- `OrderLine` class which is a sub object and doesn't have its own DAO. It contains different values from the order item and product table.
- `orderDAO` class which extends `DataAccessObject` and implements only the findById method.
# Test
## Database setup
### Running PostgreSQL
1. Pull Docker Image
   `docker pull postgres`

2. Build data directory
   `mkdir -p ~/srv/postgres`

3. Run docker image
   `docker run --rm --name lil-postgres -e POSTGRES_PASSWORD=password -d -v $HOME/srv/postgres:/var/lib/postgresql/data -p 5432:5432 postgres`

### Stopping PostgreSQL
`docker stop lil-postgres`

### Logging into Database
* `psql -h localhost -U postgres -d hplussport`

### Creating starter data
1. `psql -h localhost -U postgres -f database.sql`
2. `psql -h localhost -U postgres -d hplussport -f customer.sql`
3. `psql -h localhost -U postgres -d hplussport -f product.sql`
4. `psql -h localhost -U postgres -d hplussport -f salesperson.sql`
5. `psql -h localhost -U postgres -d hplussport -f orders.sql`

## Run the app
The code comes with a few tests already such as create, update and findById. The user simply has to run the JDBCExecutor class to test them out. From there, it is possible for the user to use that template 
to test other methods.