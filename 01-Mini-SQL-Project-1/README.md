
# **Employee Management System Project**

## **Overview**
You will develop an **Employee Management System** using **Java with PostgreSQL**. The system will manage employees, departments, contracts, and clients. Students will use **JDBC with HikariCP** for database connectivity and perform full **CRUD operations** on at least one model. The project will also require advanced SQL queries, including joins and aggregation.

---

## **Project Requirements**

### **1. Models & Relationships**

The database should include the following four models:

#### **1. Employee**
- **employee_id** (PK, SERIAL)  
- **first_name** (VARCHAR, NOT NULL)  
- **last_name** (VARCHAR, NOT NULL)  
- **email** (VARCHAR, UNIQUE, NOT NULL)  
- **phone** (VARCHAR, UNIQUE, NOT NULL)  
- **hire_date** (DATE, NOT NULL)  
- **salary** (NUMERIC, NOT NULL)  
- **department_id** (FK → Department, NOT NULL)  

**Relationships:**  
- Each employee **belongs to a department** (Many-to-One).

#### **2. Department**
- **department_id** (PK, SERIAL)  
- **name** (VARCHAR, UNIQUE, NOT NULL)  
- **location** (VARCHAR, NOT NULL)  
- **manager_id** (FK → Employee, NULLABLE)  

**Relationships:**  
- Each department **has many employees**.  
- A department **may have a manager** (optional).

#### **3. Contracts**
- **contract_id** (PK, SERIAL)  
- **contract_name** (VARCHAR, NOT NULL)  
- **start_date** (DATE, NOT NULL)  
- **end_date** (DATE, NOT NULL)  
- **employee_id** (FK → Employee, NOT NULL)  
- **client_id** (FK → Client, NOT NULL)  

**Relationships:**  
- A contract **belongs to one employee**.  
- A contract **is associated with one client**.  

#### **4. Clients**
- **client_id** (PK, SERIAL)  
- **client_name** (VARCHAR, NOT NULL)  
- **industry** (VARCHAR, NOT NULL)  
- **email** (VARCHAR, UNIQUE, NOT NULL)  
- **phone** (VARCHAR, UNIQUE, NOT NULL)  

**Relationships:**  
- A client **can have multiple contracts** (One-to-Many).  

---

### **2. CRUD Operations**
Full CRUD operations must be implemented for **at least one model (Employee, Contract, or Client)**.  

- **Create:** Add new employees, departments, contracts, and clients.  
- **Read:** Retrieve employee details, contracts per client, and department-wise employees.  
- **Update:** Modify employee details (e.g., salary increase, department transfer).  
- **Delete:** Remove employees, contracts, or clients (ensure referential integrity).  

---

### **3. Advanced SQL Features**

#### **Joins**
- Retrieve all employees along with their **department names and contract details**.
- Get a **list of all contracts with client information**.

#### **Aggregation**
- Get the **top 5 employees based on the number of contracts they have signed**:  


#### **Date Functions**
- Retrieve **all contracts active within a given year**.
- Find **employees hired in the last 6 months**.

#### **Limit and Offset**
- Implement **pagination** for the list of employees and contracts.

#### **Conditional Logic (AND/OR)**
- Allow complex searches, such as:
  - Employees earning above $50,000 **OR** working in a specific department.
  - Clients in a specific industry **AND** having at least one contract.

---

### **4. Java Integration**
#### **JDBC Driver and Connection Management**
- Use the **PostgreSQL JDBC driver** for database connection.  
- Integrate **HikariCP** for connection pooling.

#### **DAO (Data Access Object) Pattern**
- Implement a **DAO class for each model**.
- Each DAO should include CRUD operations and complex queries.


---

## **Bonus Requirements (Optional)**
1. **ON CONFLICT Clause:**  
   - Prevent duplicate email or phone entries for employees.
   - Example:
     ```sql
     INSERT INTO Employee (first_name, last_name, email, phone, hire_date, salary, department_id)
     VALUES ('John', 'Doe', 'john.doe@example.com', '123-456-7890', '2024-03-10', 60000, 2)
     ON CONFLICT (email) DO NOTHING;
     ```
   
2. **Cascading Deletes:**  
   - If a department is deleted, **should employees be deleted or reassigned?**
   - If a client is deleted, **should contracts be removed or reassigned?**

3. **Configuration Management:**  
   - Store database connection details in a `.properties` file.

   
4. **Error Handling**
- Handle **SQL exceptions** gracefully.
- Implement **logging** for all database operations.

