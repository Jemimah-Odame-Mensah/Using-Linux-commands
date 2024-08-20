# File permissions in Linux

## Project Description

The research team at my organization needs to update the file permissions for certain files and directories within the **_projects_** directory. The permissions do not currently reflect the level of authorization that should be given. Checking and updating these permissions will help keep their system secure.

## Objective

The objective of this project was to update file and directory permissions within the **_projects_** directory to align with the organization's security policies. The goal was to ensure that the correct authorization levels were enforced, preventing unauthorized access and protecting sensitive information

### Skills Learned

- Linux Command-Line Proficiency
- File Permission Management

## Steps
### 1. Check File and Directory Details:
The following code demonstrates how I used Linux commands to determine the existing permissions set for a specific directory in the file system.

![check file and directory without hidden ones](https://github.com/user-attachments/assets/7e5b6ab2-4664-4ef7-aec0-f1b14a0be712)
*Ref 1: Check file and directory details*

- The first line of the screenshot displays the command I entered: **_cd projects_**. This command allowed me to navigate into the projects directory.
- The second line shows the command **_ls -l_**, which listed the contents and displayed the permissions of the files and directories in the projects directory.
- The output of my command indicates that there was one directory named **_"drafts"_** and four other project files. The 10-character string in the first column of the output represented the permissions set for each file or directory.

Next, I checked whether any hidden files and directories existed within the projects directory.

![check any hidden file](https://github.com/user-attachments/assets/6a19b715-73ae-4128-88d7-eb54f4377bd8)
*Ref 1: Check hidden file and directory details*
- I used the ls command with the -a option to display hidden files and directories.
- The output of my command indicates that there were two hidden directories, **_"."_** and **_".."_**, along with one hidden file named **_".project_x.txt"_**.

### Describe the Permissions String:
The 10-character string can be deconstructed to determine who is authorized to access the file and their specific permissions. The characters and what they represent are as follows:
- **1st character:** This character is either a **d** or hyphen (**-**) and indicates the file type. If it’s a **d**, it’s a directory. If it’s a hyphen (**-**), it’s a regular file.
- **2nd-4th characters:** These characters indicate the read (**r**), write (**w**), and execute (**x**) permissions for the **_"user"_**. When one of these characters is a hyphen (**-**) instead, it indicates that this permission is not granted to the **_"user"_**.
- **5th-7th characters:** These characters indicate the read (**r**), write (**w**), and execute (**x**) permissions for the **_"group"_**. When one of these characters is a hyphen (**-**) instead, it indicates that this permission is not granted for the **_"group"_**.
- **8th-10th characters:** These characters indicate the read (**r**), write (**w**), and execute (**x**) permissions for **_"other"_**. This owner type consists of all other users on the system apart from the **_"User"_** and the **_"group"_**. When one of these characters is a hyphen (**-**) instead, that indicates that this permission is not granted for **_"other"_**.

For example, the file permissions for **_project_t.txt_** ( in *Ref 1: Check file and directory details*) are **-rw-rw-r--**. Since the first character is a hyphen (**-**), this indicates that **_project_t.txt_** is a file, not a directory. The second, fifth, and eighth characters are all **r**, which indicates that user, group, and other all have read permissions. The third and sixth characters are **w**, which indicates that only the user and group have write permissions. No one has execute permissions for **_project_t.txt_**.

### 2. Retrieve Login Attempts Outside of Mexico:
Another suspicious activity involved login attempts that the team determined did not originate in Mexico. Therefore, I investigated login attempts that occurred outside of Mexico.
As demonstrated below, I used SQL filters to create a query that identifies all login attempts outside of Mexico:

![SQL retrieve login attempts outside of mexico](https://github.com/user-attachments/assets/0bfd8e6d-824c-4ef2-884e-04179f6b135e)
*Ref 3: SQL query*

In the screenshot, the first three lines represent my query, and the remaining portion shows a sample of the output. I started by selecting all data from the **_log_in_attempts_** table using the **_SELECT *_** and **_FROM_** keywords. Then, I used a **_WHERE_** clause with **_NOT_** to filter for countries other than Mexico. I used **_LIKE_** with **_MEX%_** as the pattern to match because the dataset represents Mexico as **_MEX_** and **_MEXICO_**. The percentage sign **_%_** represents any number of unspecified characters when used with **_LIKE_**. 

### 4. Retrieve Employees in Marketing:
My team needed to perform security updates on specific employee machines in the Marketing department located in the East building. I was responsible for gathering information on these employee machines and queried the **_employees_** table.
As demonstrated below, I used SQL filters to create a query that identifies all employees in the Marketing department across offices in the East building:

![SQL retrieve employees in marketing department in the east building](https://github.com/user-attachments/assets/f0fdf982-fce0-46f4-85bd-57def401daff)
*Ref 4: SQL query*

In the screenshot, the first three lines represent my query, and the remaining portion shows a sample of the output. I started by selecting all data from the **_employees_** table using the **_SELECT *_** and **_FROM_** keywords. Then, I used a **_WHERE_** clause with **_AND_** to filter for employees who work in the Marketing department and in the East building. I used **_LIKE 'East%'_** to match the data in the **_office_** column, which represents the East building with a specific office number. The first condition, **_department = 'Marketing'_**, filters for employees in the Marketing department. The second condition, **_office LIKE 'East%'_**, filters for employees in the East building.

### 5. Retrieve Employees in Finance or Sales:
The machines for employees in the Finance and Sales departments also need to be updated. Since a different security update is needed, I had to get information on employees only from these two departments. As shown below, I used SQL filters to create a query that identifies all employees in the Sales or Finance departments:

![SQL retrieve employees in finance or salse department](https://github.com/user-attachments/assets/b58ba27d-bf49-46b0-adf5-704c3887855e)
*Ref 5: SQL query*

In the screenshot, the first three lines represent my query, and the remaining portion shows a sample of the output. I started by selecting all data from the **_employees_** table using the **_SELECT *_** and **_FROM_** keywords. Then, I used a **_WHERE_** clause with **_OR_** to filter for employees in either the Finance or Sales departments. The first condition, **_department = 'Finance'_**, filters for employees in the Finance department. The second condition, **_department = 'Sales'_**, filters for employees in the Sales department.

### 6. Retrieve All Employees Not in IT:
My team needed to make one more update to employee machines. Employees in the Information Technology (IT) department had already received this update, so the update was required for employees in all other departments. I used SQL filters to create a query that identifies all employees not in the IT department:

![SQL retrieve all employees not in IT department](https://github.com/user-attachments/assets/909ccef4-b2f7-499b-8316-79138988c1ec)
*Ref 6: SQL query*

I started by selecting all data from the **_employees_** table using the **_SELECT *_** and **_FROM_** keywords. Then, I used a **_WHERE_** clause with **_NOT_** to filter out employees not in the IT department.


## Summary

In this project, I applied SQL filters to extract specific information on login attempts and employee machines. I worked with two different tables, **_log_in_attempts_** and **_employees_**, using the **_AND_**, **_OR_**, and **_NOT_** operators to filter for the specific information required for each task. Additionally, I used the **_LIKE_** operator and the **_%_** wildcard to match patterns in the data.
