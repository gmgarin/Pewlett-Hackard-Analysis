# Pewlett-Hackard-Analysis

## **Overview of the Analysis**
### The goal of this analysis was to help Pewlett-Hackard company to identify employees who will be eligible for retirement as well as promotions. In addition, it also aimed to identify critical information about the positions or titles that will be opened up for hiring once eligible employees retire. This analysis utilized SQL and pgAdmin 4 to come up with a list of eligible employees including their positions and relavant employee data.

## **Results**
### *Entity Relationship Diagram*
#### The analysis of the data started by establishing relationship of data using Entity Relationship Diagram (ERD). This schematic diagram helped me identified the connection between the variables involved. See image below.

![This is an image](/Resources/EmployeeDB.png)
<p align="center">
    ERD 
</p>

### *Employee Titles*
#### The table shows the number of employees in each titles. Once these eligible employees retire, the positions that will be opened will be coming from senior engineer, senior staff, engineer, and staff.

![This is an image](/Resources/titles.png)
<p align="center">
    Retiring Titles
</p>

### *Mentorship Eligibility*
#### By using filtering through the dates, employees who are eligible for mentorship program are identified. 

![This is an image](/Resources/mentorship_list.png)
<p align="center">
    Mentorship Candidates
</p>

### *Retirement Titles*
#### The image below shows the employees whore are eligible for retirement. 

![This is an image](/Resources/retirement_titles.png)
<p align="center">
    Eligble Employees for Retirement
</p>

## **Summary**
#### After filtering the data by date of birth and date hired as well as cleaning the data, when the "silver tsunami" begins to make an impact, there are 90,398 roles that need to be filled. This was identified from the unique_titles using the code below:

            SELECT COUNT (emp_no)
            FROM unique_titles
           
#### Using the queries below, PH can create a table that will include all the employees of the company.

        SELECT DISTINCT ON (employees.emp_no) employees.emp_no,
            employees.first_name,
            employees.last_name,
            titles.title,
            titles.from_date,
            titles.to_date
        INTO total_employees
        FROM employees
        LEFT JOIN titles
        ON employees.emp_no = titles.emp_no
        ORDER BY employees.emp_no, titles.to_date DESC

        SELECT COUNT (emp_no)
        FROM total_employees

#### From the results, PH has 300,024 employees. Using this data, 30% of their employees are retiring. However, there are only approximately 1,549 employees are for the mentorship pogram. This was done using the code below:

        SELECT COUNT(title), title
        FROM mentorship_eligibility
        GROUP BY title
        ORDER BY COUNT(title) DESC;

#### In conlusion, with a third of the PH employees are retiring and only 1,549 employees are eligible for mentorship program, the company does not have enough qualified, retirement-ready employees to mentor the next generation PH employees.