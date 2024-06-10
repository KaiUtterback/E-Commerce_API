# E-Commerce Flask API

## Overview
This project is a Flask-based RESTful API for managing an e-commerce system. The application allows you to manage customers, customer accounts, products, and orders. It uses Flask-SQLAlchemy for database interactions and Flask-Marshmallow for serialization and deserialization.

## Prerequisites
- Python 3.7+
- MySQL database

## Installation

1. **Clone the repository:**
   ```sh
   git clone <repository_url>
   cd <repository_directory>
   ```

2. **Create and activate a virtual environment:**
   ```sh
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. **Install the required packages:**
   ```sh
   pip install -r requirements.txt
   ```

4. **Set up your MySQL database:**
   ```sql
   CREATE DATABASE e_commerce_db;

   USE e_commerce_db;

   CREATE TABLE Customers (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(255) NOT NULL,
       email VARCHAR(320),
       phone VARCHAR(15)
   );

   CREATE TABLE Orders (
       id INT AUTO_INCREMENT PRIMARY KEY,
       date DATE NOT NULL,
       customer_id INT,
       status VARCHAR(50) NOT NULL DEFAULT 'Pending',
       FOREIGN KEY (customer_id) REFERENCES Customers(id)
   );

   CREATE TABLE Customer_Accounts (
       id INT AUTO_INCREMENT PRIMARY KEY,
       username VARCHAR(255) UNIQUE NOT NULL,
       password VARCHAR(255) NOT NULL,
       customer_id INT,
       FOREIGN KEY (customer_id) REFERENCES Customers(id)
   );

   CREATE TABLE Products (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(255) NOT NULL,
       price FLOAT NOT NULL
   );

   CREATE TABLE Order_Product (
       order_id INT,
       product_id INT,
       PRIMARY KEY (order_id, product_id),
       FOREIGN KEY (order_id) REFERENCES Orders(id),
       FOREIGN KEY (product_id) REFERENCES Products(id)
   );
   ```

5. **Configure the database URI in your Flask application:**
   ```python
   app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+mysqlconnector://<username>:<password>@localhost/e_commerce_db'
   ```

6. **Initialize the database and create tables:**
   ```sh
   python fitness_center.py
   ```

## API Endpoints

### Customer Endpoints
- **Add Customer**
  ```sh
  POST /customers
  ```
  Request Body:
  ```json
  {
      "name": "John Doe",
      "email": "john@example.com",
      "phone": "1234567890"
  }
  ```

- **List Customers**
  ```sh
  GET /customers
  ```

- **Get Customer**
  ```sh
  GET /customers/<int:id>
  ```

- **Update Customer**
  ```sh
  PUT /customers/<int:id>
  ```
  Request Body:
  ```json
  {
      "name": "John Doe",
      "email": "john@example.com",
      "phone": "1234567890"
  }
  ```

- **Delete Customer**
  ```sh
  DELETE /customers/<int:id>
  ```

### Customer Account Endpoints
- **Create Customer Account**
  ```sh
  POST /customer_accounts
  ```
  Request Body:
  ```json
  {
      "username": "john_doe",
      "password": "securepassword"
  }
  ```

- **Get Customer Account**
  ```sh
  GET /customer_accounts/<int:id>
  ```

- **Update Customer Account**
  ```sh
  PUT /customer_accounts/<int:id>
  ```
  Request Body:
  ```json
  {
      "username": "john_doe",
      "password": "newpassword"
  }
  ```

- **Delete Customer Account**
  ```sh
  DELETE /customer_accounts/<int:id>
  ```

### Product Endpoints
- **Create Product**
  ```sh
  POST /products
  ```
  Request Body:
  ```json
  {
      "name": "Product Name",
      "price": 19.99
  }
  ```

- **Get Product**
  ```sh
  GET /products/<int:id>
  ```

- **Update Product**
  ```sh
  PUT /products/<int:id>
  ```
  Request Body:
  ```json
  {
      "name": "Updated Product Name",
      "price": 29.99
  }
  ```

- **Delete Product**
  ```sh
  DELETE /products/<int:id>
  ```

- **List Products**
  ```sh
  GET /products
  ```

### Order Endpoints
- **Place Order**
  ```sh
  POST /orders
  ```
  Request Body:
  ```json
  {
      "date": "2024-06-10",
      "customer_id": 1,
      "product_ids": [1, 2]
  }
  ```

- **Retrieve Order**
  ```sh
  GET /orders/<int:id>
  ```

- **List Orders**
  ```sh
  GET /orders
  ```

- **Delete Order**
  ```sh
  DELETE /orders/<int:id>
  ```

- **Update Order Status**
  ```sh
  PUT /orders/<int:id>/status
  ```
  Request Body:
  ```json
  {
      "status": "Shipped"
  }
  ```

## License
This project is licensed under the MIT License.

---

This README provides an overview of the project, installation steps, how to run the application, and detailed information about the available API endpoints. Adjust the `repository_url` in the installation section and add any additional details specific to your project as needed.
