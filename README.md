# SAP ABAP – Purchase Order Management System

## Project Overview

The **Purchase Order Management System** is an SAP ABAP-based application developed using Object-Oriented Programming (OOPs) concepts. The system manages vendors, materials, purchase orders and purchase order items.

It provides functionalities for creating and displaying purchase orders, validating vendor and material information, calculating item and purchase order totals, managing purchase order statuses and generating ALV reports with dynamic filters.

The application is developed using a custom database structure and ABAP local classes to maintain modularity, reusability and code organization.

---

## Objectives

* Develop a purchase order management application using SAP ABAP.
* Implement Object-Oriented Programming concepts.
* Create and manage custom database tables using SAP Dictionary (SE11).
* Validate vendor and material information before creating purchase orders.
* Calculate item totals and purchase order totals automatically.
* Manage purchase order statuses.
* Generate interactive ALV reports.
* Implement dynamic selection screens and filtering options.

---

## Technologies Used

| Technology    | Purpose                                  |
| ------------- | ---------------------------------------- |
| SAP ABAP      | Application development                  |
| SAP GUI       | Development and execution environment    |
| SE38          | ABAP program development                 |
| SE11          | Database table and data element creation |
| SE16N         | Database record verification             |
| Open SQL      | Database operations                      |
| OOPs          | Modular application development          |
| CL_SALV_TABLE | ALV reporting                            |

---

## Database Design

The project uses five custom database tables.

### 1. Z25VENDOR – Vendor Master

Stores vendor information.

| Field       | Description           |
| ----------- | --------------------- |
| MANDT       | Client                |
| VENDOR_ID   | Vendor identification |
| VENDOR_NAME | Vendor name           |
| CITY        | Vendor location       |
| EMAIL       | Vendor email          |

### 2. Z25MATERIAL – Material Master

Stores material information.

| Field         | Description             |
| ------------- | ----------------------- |
| MANDT         | Client                  |
| MATERIAL_ID   | Material identification |
| MATERIAL_NAME | Material name           |
| UNIT          | Unit of measurement     |
| PRICE         | Material price          |
| CURRENCY      | Currency                |

### 3. Z25VENDOR_MAT1 – Vendor-Material Relationship

Maintains the relationship between vendors and the materials they supply.

| Field       | Description             |
| ----------- | ----------------------- |
| MANDT       | Client                  |
| VENDOR_ID   | Vendor identification   |
| MATERIAL_ID | Material identification |

### 4. Z25PO_HEADER – Purchase Order Header

Stores general purchase order information.

| Field         | Description                   |
| ------------- | ----------------------------- |
| MANDT         | Client                        |
| PO_ID         | Purchase order identification |
| VENDOR_ID     | Vendor identification         |
| PO_DATE       | Purchase order date           |
| DELIVERY_DATE | Expected delivery date        |
| CURRENCY      | Currency                      |
| TOTAL_AMOUNT  | Total purchase order amount   |
| STATUS        | Purchase order status         |

### 5. Z25PO_ITEM – Purchase Order Items

Stores individual items associated with purchase orders.

| Field       | Description                   |
| ----------- | ----------------------------- |
| MANDT       | Client                        |
| PO_ID       | Purchase order identification |
| ITEM_NO     | Item number                   |
| MATERIAL_ID | Material identification       |
| QUANTITY    | Ordered quantity              |
| UNIT        | Unit of measurement           |
| UNIT_PRICE  | Price per unit                |
| LINE_TOTAL  | Total item amount             |
| CURRENCY    | Currency                      |

---

## Object-Oriented Programming Implementation

The application uses three local ABAP classes.

### 1. LCL_PO_VALIDATOR

Responsible for validating input information.

Methods:

* VALIDATE_VENDOR – Checks whether the vendor exists.
* VALIDATE_MATERIAL – Checks whether the material exists.
* VALIDATE_QUANTITY – Ensures that the quantity is greater than zero.
* VALIDATE_VENDOR_MATERIAL – Checks whether the vendor is registered to supply the selected material.

### 2. LCL_PO_DAO

Responsible for database retrieval operations.

Methods:

* GET_VENDOR – Retrieves vendor details.
* GET_MATERIAL – Retrieves material details.
* DISPLAY_PURCHASE_ORDER – Retrieves purchase order header and item details.

### 3. LCL_PO_SERVICE

Responsible for purchase order business logic.

Methods:

* CALCULATE_ITEM_TOTAL – Calculates the individual item amount.
* CALCULATE_PO_TOTAL – Calculates the total purchase order amount.
* CREATE_PURCHASE_ORDER – Creates purchase orders and adds items.
* UPDATE_PO_STATUS – Updates purchase order status based on business rules.

---

## Key Features

### 1. Purchase Order Creation

* Creates new purchase orders.
* Allows multiple items to be added to an existing eligible purchase order.
* Validates vendor and material information.
* Checks vendor-material relationships.
* Generates item numbers dynamically.
* Calculates item totals automatically.
* Updates purchase order totals.

### 2. Purchase Order Display

Displays complete purchase order information, including:

* Purchase order ID.
* Vendor ID and vendor name.
* Purchase order date.
* Delivery date.
* Total amount.
* Currency.
* Purchase order status.
* Material details.
* Quantity and unit price.
* Individual item totals.

### 3. Purchase Order Status Management

Supports three purchase order statuses:

| Status Code | Description |
| ----------- | ----------- |
| N           | New         |
| R           | Released    |
| C           | Cancelled   |

Business rules:

* Only New purchase orders can be released.
* New and Released purchase orders can be cancelled.
* Released or Cancelled purchase orders cannot be released again.
* Cancelled purchase orders cannot be modified by adding new items.

### 4. Purchase Order Overview – ALV

Displays purchase order header information using ALV reporting.

Features:

* Displays purchase order details.
* Displays vendor names.
* Displays readable status descriptions.
* Supports filtering by vendor ID.
* Supports filtering by purchase order status.
* Supports filtering by purchase order date.

### 5. Purchase Order Item Overview – ALV

Displays individual purchase order items using ALV reporting.

Features:

* Displays purchase order and vendor information.
* Displays material details.
* Displays quantities and prices.
* Displays individual item totals.
* Displays purchase order status and descriptions.
* Supports filtering by purchase order ID.
* Supports filtering by vendor ID.
* Supports filtering by material ID.

### 6. Dynamic Selection Screen

The application provides separate selection screen options for:

* Create Purchase Order.
* Display Purchase Order.
* Manage PO Status.
* Purchase Order Overview.
* Purchase Order Item Overview.

Input fields are dynamically displayed according to the selected operation.

---

## Calculation Logic

### Item Total Calculation

Item total is calculated using:

`Item Total = Quantity × Unit Price`

Example:

Quantity = 2

Unit Price = ₹50,000

Item Total = ₹1,00,000

### Purchase Order Total Calculation

The purchase order total is calculated by adding the line totals of all items belonging to the purchase order.

`PO Total = SUM(Line Totals)`

Example:

| Material  | Quantity | Unit Price |   Line Total |
| --------- | -------: | ---------: | -----------: |
| Laptop    |        2 |     50,000 |     1,00,000 |
| Webcam    |        1 |      3,500 |        3,500 |
| **Total** |          |            | **1,03,500** |

---

## Project Screenshots

Screenshots demonstrating the database design, ABAP implementation and application execution are available in the `Screenshots` folder.

### Selection Screens

Add screenshots demonstrating the different application operations.

### Database Tables

Add screenshots of:

* Vendor Master
* Material Master
* Vendor-Material Relationship
* Purchase Order Header
* Purchase Order Items

### ABAP OOPs Implementation

Add screenshots demonstrating:

* Validator Class
* DAO Class
* Service Class
* Class Implementations
* Dynamic Selection Screen
  

### Application Execution

Add screenshots demonstrating:

* Purchase Order Creation
* Purchase Order Display
* Status Management
* Purchase Order Overview ALV
* Purchase Order Item Overview ALV

### ALV Reports

Add screenshots demonstrating the header and item reports with their respective filters.

---

## How to Execute the Project

1. Log in to the SAP system.
2. Create the required custom data elements and database tables using SE11.
3. Activate all database objects.
4. Populate the vendor and material master tables.
5. Populate the vendor-material relationship table.
6. Add the required sample purchase order records, if needed.
7. Open transaction SE38.
8. Enter the program name `Z25_PO_MANAGEMENT`.
9. Create or open the ABAP program.
10. Copy the source code from the `ABAP_Source_Code` folder.
11. Save and activate the program.
12. Execute using F8.
13. Select the required purchase order operation.
14. Enter the required inputs and execute.

**Note:** The custom DDIC objects and sample database records must be created in the target SAP system before executing the program.

---

## Testing

The application can be tested using the following scenarios:

| Test Case                                     | Expected Result                          |
| --------------------------------------------- | ---------------------------------------- |
| Create PO with valid inputs                   | Purchase order item created successfully |
| Enter invalid vendor ID                       | Vendor validation error                  |
| Enter invalid material ID                     | Material validation error                |
| Enter zero or negative quantity               | Quantity validation error                |
| Select an invalid vendor-material combination | Relationship validation error            |
| Enter an earlier delivery date                | Date validation error                    |
| Add an item to a released PO                  | Operation rejected                       |
| Add an item to a cancelled PO                 | Operation rejected                       |
| Release a New PO                              | Status changes to Released               |
| Cancel a New or Released PO                   | Status changes to Cancelled              |
| Display an existing PO                        | Header and item details displayed        |
| Execute header ALV                            | Purchase order overview displayed        |
| Execute item ALV                              | Purchase order item overview displayed   |
| Apply report filters                          | Matching records displayed               |

---

## Repository Structure

```text
SAP-ABAP-Purchase-Order-Management-System/
│
├── README.md
│
├── Source_Code/
│   └── Z25_PO_MANAGEMENT.abap
│
├── Database_tables/
│   ├── Z
│   ├── Z25MATERIAL
│   ├── Z25VENDOR_MAT1
│   ├── Z25PO_HEADER
│   └── Z25PO_ITEM
│
├── Screenshots/
│   ├── 01_Selection_Screens/
│   ├── 02_Database_Tables/
│   ├── 03_ABAP_Program/
│   ├── 04_Execution_Outputs/
│   └── 05_ALV_Reports/
│
└── Documentation/
    ├── Project_Overview.pdf
    ├── Database_Design.pdf
    └── Test_Cases.pdf
```

---

## Future Enhancements

* Vendor master creation and modification.
* Material master management.
* Purchase order modification and deletion with appropriate authorization checks.
* Purchase order search and advanced reporting.
* Improved user interface using SAP module pool programming.
* Purchase order print functionality.
* Email notifications for purchase order status changes.

---

## Conclusion

The Purchase Order Management System demonstrates the practical implementation of SAP ABAP programming, Object-Oriented Programming, custom database table design, Open SQL operations, business validations, internal tables and ALV reporting.

The project provides hands-on experience in developing an enterprise-oriented business application using SAP ABAP.

---

**Project Name:** Purchase Order Management System
**Technology:** SAP ABAP
**Development Environment:** SAP GUI
**Program Name:** Z25_PO_MANAGEMENT
**Package:** Z25_pack_tijiya
