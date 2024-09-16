[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/r-tQZu0l)
# BBT3104-Lab1of6-DatabaseTransactions


| **Key**                                                               | Value                                                                                                                                                                              |
|---------------|---------------------------------------------------------|
| **Group Name**                                                               | ? |
| **Semester Duration**                                                 | 19<sup>th</sup> August - 25<sup>th</sup> November 2024                                                                                                                       |

## Flowchart

## Pseudocode
START TRANSACTION
SET @orderNumber = MAX(orderNumber) + 1 FROM orders

INSERT INTO orders (@orderNumber, currentDate, requiredDate, shippedDate, status, customerNumber)
SAVEPOINT before_product_1

INSERT INTO orderdetails (orderNumber, productCode, quantityOrdered, priceEach, orderLineNumber)
UPDATE products SET quantityInStock = quantityInStock - orderedQuantity

SAVEPOINT before_product_2
INSERT product_2
IF error THEN
   ROLLBACK TO SAVEPOINT before_product_2
ENDIF

INSERT remaining products
RECEIVE payment from customer

COMMIT TRANSACTION

## Support for the Sales Departments' Report
Improvement for Database Design to Track Instalment Payments:

A new table could be introduced to track partial payments. This table could store the orderNumber, paymentAmount, paymentDate, and balance. Each time a payment is made, a new record is inserted. This allows the sales department to query orders with unpaid balances by checking if the total payment amount is less than the order total.

Example table schema for payment_details:
   sql
   CREATE TABLE payment_details (
       paymentID INT AUTO_INCREMENT PRIMARY KEY,
       orderNumber INT,
       paymentAmount DECIMAL(10, 2),
       paymentDate DATE,
       balance DECIMAL(10, 2),
       FOREIGN KEY (orderNumber) REFERENCES orders(orderNumber)
   );
   

This schema would allow the sales department to easily generate a report of orders that have not been fully paid by querying for orders where the balance is greater than zero.
