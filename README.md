SELECT 
    lPAD(employee_id, 5, '0') AS "Employee ID",
    CONCAT(last_name, ' ', first_name) AS "Full Name",
    CONCAT(LOWER(first_name), '.', LOWER(last_name), '@company.com') AS "Email"
FROM 
    Employee;



SELECT 
    first_name AS "First Name",
    last_name AS "Last Name",
    DATE_FORMAT(employment_date, '%d-%m-%Y') AS "Hire Date",
    TIMESTAMPDIFF(YEAR, employment_date, CURDATE()) AS "Years of Service"
FROM 
    Employee;



SELECT 
    MIN(salary) AS "Minimum Salary",
    MAX(salary) AS "Maximum Salary"
FROM 
    Employee;



SELECT 
    AVG(bonus) AS "Average Bonus (with Bonuses)"
FROM 
    Employee
WHERE 
    bonus IS NOT NULL;



SELECT 
    AVG(IFNULL(bonus, 0)) AS "Average Bonus (Company-wide)"
FROM 
    Employee;



SELECT 
    COUNT(*) AS "Total Employees"
FROM 
    Employee;



SELECT 
    COUNT(*) AS "Employees with Bonuses"
FROM 
    Employee
WHERE 
    bonus IS NOT NULL;



SELECT 
    d.department_name AS "Department",
    COUNT(DISTINCT d.department_id) AS "Total Departments",
    COUNT(DISTINCT d.city) AS "Total Offices",
    e.position AS "Position",
    COUNT(*) AS "Number of Employees"
FROM 
    Employee e
JOIN 
    Department d ON e.department_id = d.department_id
GROUP BY 
    d.department_name, e.position;


 
SELECT 
    d.department_name AS "Department",
    e.position AS "Position",
    COUNT(*) AS "Number of Employees with Sales"
FROM 
    Employee e
JOIN 
    Department d ON e.department_id = d.department_id
JOIN 
    Invoice i ON e.employee_id = i.employee_id
GROUP BY 
    d.department_name, e.position
HAVING 
    COUNT(i.invoice_id) > 5;



SELECT 
    LPAD(product_id, 4, '0') AS "Product ID",
    CONCAT(manufacturer, ' :: ', SUBSTRING_INDEX(product_name, '/', 1)) AS "Product Name",
    UPPER(CONCAT(product_type, ' - ', category)) AS "Category"
FROM 
    Product
ORDER BY 
    manufacturer;
