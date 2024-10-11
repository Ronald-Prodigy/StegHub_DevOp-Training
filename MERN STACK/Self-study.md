# StegHub DevOpsTraining
**MERN WEB STACK STUDY MATERIALS**

# Side Self Study

## 1. Database Management Systems (DBMS)

### Types of DBMS:
- **Relational DBMS (RDBMS)**:
  - **Examples**: MySQL, PostgreSQL, Oracle Database, SQL Server
  - **Suitable for**: Structured data with relationships between tables; complex queries and transactions.
- **NoSQL DBMS**:
  - **Document Stores**: MongoDB, CouchDB
    - **Suitable for**: Semi-structured data; flexible schema; JSON-like documents.
  - **Key-Value Stores**: Redis, DynamoDB
    - **Suitable for**: Simple key-value pairs; high-speed read and write operations.
  - **Column Stores**: Cassandra, HBase
    - **Suitable for**: Large volumes of data; analytical queries; column-oriented storage.
  - **Graph Databases**: Neo4j, Amazon Neptune
    - **Suitable for**: Data with complex relationships; social networks; recommendation engines.

### Difference Between Relational DBMS and NoSQL:
- **Relational DBMS**:
  - **Structure**: Tables with rows and columns.
  - **Schema**: Fixed schema.
  - **ACID Compliance**: Strong consistency and transactional support.
  - **Use Case**: Traditional applications with structured data and complex queries.
- **NoSQL**:
  - **Structure**: Various structures (documents, key-value, columns, graphs).
  - **Schema**: Dynamic schema.
  - **BASE Compliance**: Eventual consistency and high availability.
  - **Use Case**: Large-scale data, real-time web apps, and flexible schema requirements.

## 2. Web Application Frameworks

### Server-Side (Backend) Frameworks:
- **Examples**: Express.js (Node.js), Django (Python), Ruby on Rails (Ruby), Spring (Java)
- **Used For**: Building the server-side logic, managing databases, handling HTTP requests, and ensuring security and scalability.

### Client-Side (Frontend) Frameworks:
- **Examples**: React.js, Angular, Vue.js, Svelte
- **Used For**: Building interactive user interfaces, managing client-side state, and enhancing the user experience with dynamic content.

## 3. Practice Basic JavaScript Syntax

### Basic JavaScript Concepts:
- **Variables**: `var`, `let`, `const`
- **Data Types**: String, Number, Boolean, Object, Array
- **Functions**: Function declarations and expressions
- **Control Structures**: `if` statements, loops (`for`, `while`)
- **DOM Manipulation**: Accessing and modifying HTML elements

### Example:
```javascript
let message = "Hello, World!";
console.log(message);

function add(a, b) {
  return a + b;
}

let sum = add(2, 3);
console.log(sum);
```

## 4. RESTful API

### What is RESTful API?
- **Definition**: REST (Representational State Transfer) is an architectural style for designing networked applications.
- **Principles**: Stateless, client-server architecture, cacheable responses, uniform interface.
- **Used For**: Creating scalable web services; allowing different systems to communicate over HTTP.

### Example Use Case:
- **GET**: Retrieve data from a server.
- **POST**: Send data to a server to create a resource.
- **PUT**: Update an existing resource on a server.
- **DELETE**: Remove a resource from a server.

## 5. Cascading Style Sheets (CSS)

### What is CSS Used For?
- **Purpose**: CSS is used to style and layout web pages, including the design, colors, fonts, and overall presentation of HTML elements.

### Basic Syntax and Properties:
- **Syntax**:
  ```css
  selector {
    property: value;
  }
  ```
- **Example**:
  ```css
  body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    color: #333;
  }

  h1 {
    color: #0066cc;
    font-size: 2em;
  }

  p {
    line-height: 1.5;
  }
  ```