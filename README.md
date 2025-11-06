# 🏨 **Hotel Booking System (SQL Project)**

## **Overview**

The **Hotel Booking System** is a database project designed to manage hotel customer details, room availability, and booking records efficiently.
It includes three main tables — **Customers**, **Rooms**, and **Bookings** — with relationships defined through **foreign keys** to ensure data consistency and relational integrity.

This database can be used for small to medium-scale hotel management tasks such as storing customer data, tracking room availability, calculating total charges, and analyzing booking patterns.

---

## **📂 Database Structure**

### **1. Database Creation**

```sql
CREATE DATABASE hotel_booking_system;
USE hotel_booking_system;
```

Creates a new database named `hotel_booking_system` and switches the context to it.

---

### **2. Tables**

#### **a) customers**

Stores customer details such as name, contact information, and city.

```sql
CREATE TABLE customers (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    full_name VARCHAR(50),
    email VARCHAR(50),
    phone VARCHAR(15),
    city VARCHAR(30)
);
```

#### **b) rooms**

Contains information about rooms, including type, price, and availability status.

```sql
CREATE TABLE rooms (
    room_id INT AUTO_INCREMENT PRIMARY KEY,
    room_number INT UNIQUE,
    room_type VARCHAR(30),
    price_per_night DECIMAL(8,2),
    is_available BOOLEAN
);
```

#### **c) bookings**

Stores booking records linking customers and rooms with details such as check-in/check-out dates and total amount.

```sql
CREATE TABLE bookings (
    booking_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    room_id INT,
    check_in DATE,
    check_out DATE,
    total_amount DECIMAL(10,2),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (room_id) REFERENCES rooms(room_id)
);
```

---

## **🧾 Sample Data**

Sample records are inserted to demonstrate how the system works.

```sql
INSERT INTO customers (full_name, email, phone, city) VALUES
('Aman Sharma', 'aman@gmail.com', '9876543210', 'Delhi'),
('Riya Verma', 'riya@gmail.com', '9765432109', 'Mumbai'),
('Karan Patel', 'karanp@gmail.com', '9898989898', 'Ahmedabad'),
('Simran Kaur', 'simran@gmail.com', '9123456789', 'Chandigarh'),
('Vivek Singh', 'vivek@gmail.com', '9001234567', 'Lucknow'),
('Neha Jain', 'neha@gmail.com', '9345678912', 'Pune');
```

```sql
INSERT INTO rooms (room_number, room_type, price_per_night, is_available) VALUES
(101, 'Single', 2500.00, TRUE),
(102, 'Double', 3500.00, FALSE),
(103, 'Suite', 6000.00, TRUE),
(104, 'Deluxe', 4500.00, FALSE),
(105, 'Double', 3500.00, TRUE),
(106, 'Suite', 7000.00, TRUE);
```

```sql
INSERT INTO bookings (customer_id, room_id, check_in, check_out, total_amount) VALUES
(1, 2, '2025-10-10', '2025-10-12', 7000.00),
(2, 4, '2025-09-15', '2025-09-18', 13500.00),
(3, 5, '2025-08-01', '2025-08-03', 7000.00),
(4, 3, '2025-10-05', '2025-10-06', 6000.00),
(5, 6, '2025-09-25', '2025-09-27', 14000.00),
(1, 1, '2025-10-01', '2025-10-02', 2500.00);
```

---

## **📊 Queries and Operations**

### **1. Show all customers from a specific city**

```sql
SELECT * FROM customers WHERE city = 'Mumbai';
```

### **2. Show all available rooms**

```sql
SELECT room_number, room_type, price_per_night 
FROM rooms 
WHERE is_available = TRUE;
```

### **3. Show bookings with total amount greater than ₹8000**

```sql
SELECT * FROM bookings WHERE total_amount > 8000;
```

### **4. Total bookings made by each customer**

```sql
SELECT c.full_name, COUNT(b.booking_id) AS total_bookings
FROM customers c
JOIN bookings b ON c.customer_id = b.customer_id
GROUP BY c.full_name;
```

### **5. Show customers who booked more than one room**

```sql
SELECT c.full_name, COUNT(b.booking_id) AS total_bookings
FROM customers c
JOIN bookings b ON c.customer_id = b.customer_id
GROUP BY c.full_name
HAVING COUNT(b.booking_id) > 1;
```

### **6. Show full booking details (customer + room + booking info)**

```sql
SELECT 
    b.booking_id,
    c.full_name,
    r.room_number,
    r.room_type,
    b.check_in,
    b.check_out,
    b.total_amount
FROM bookings b
JOIN customers c ON b.customer_id = c.customer_id
JOIN rooms r ON b.room_id = r.room_id;
```

### **7. List customers and their booked room types**

```sql
SELECT c.full_name, r.room_type
FROM customers c
JOIN bookings b ON c.customer_id = b.customer_id
JOIN rooms r ON b.room_id = r.room_id;
```

---

## **🧠 Key Features**

* Manages **customer, room, and booking** data efficiently.
* Tracks **room availability** dynamically.
* Supports **relationship queries** between customers, rooms, and bookings.
* Enables **aggregated data analysis** (e.g., total bookings per customer).
* Ensures **data integrity** with foreign keys.

---

## **🧩 Future Enhancements**

* Add a **payment table** for managing billing details.
* Integrate **staff management** and **room service** tracking.
* Implement **stored procedures** for booking automation.
* Build a **web interface** using PHP, Python, or Node.js for front-end access.

---

## **📚 Author**

**Project by:** Jatinder Singh
**Role:** Developer & Database Designer
**Tools Used:** MySQL / MariaDB
