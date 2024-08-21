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
*Ref 2: Check hidden file and directory details*
- I used the ls command with the -a option to display hidden files and directories.
- The output of my command indicates that there were two hidden directories, **_"."_** and **_".."_**, along with one hidden file named **_".project_x.txt"_**.

### Describe the Permissions String:
The 10-character string can be deconstructed to determine who is authorized to access the file and their specific permissions. The characters and what they represent are as follows:
- **1st character:** This character is either a **d** or hyphen (**-**) and indicates the file type. If it’s a **d**, it’s a directory. If it’s a hyphen (**-**), it’s a regular file.
- **2nd-4th characters:** These characters indicate the read (**r**), write (**w**), and execute (**x**) permissions for the **_"user"_**. When one of these characters is a hyphen (**-**) instead, it indicates that this permission is not granted to the **_"user"_**.
- **5th-7th characters:** These characters indicate the read (**r**), write (**w**), and execute (**x**) permissions for the **_"group"_**. When one of these characters is a hyphen (**-**) instead, it indicates that this permission is not granted for the **_"group"_**.
- **8th-10th characters:** These characters indicate the read (**r**), write (**w**), and execute (**x**) permissions for **_"other"_**. This owner type consists of all other users on the system apart from the **_"User"_** and the **_"group"_**. When one of these characters is a hyphen (**-**) instead, that indicates that this permission is not granted for **_"other"_**.

For example, the file permissions for **_"project_t.txt"_** ( in *Ref 1: Check file and directory details*) are **-rw-rw-r--**. Since the first character is a hyphen (**-**), this indicates that **_"project_t.txt"_** is a file, not a directory. The second, fifth, and eighth characters are all **r**, which indicates that **_"user"_**, **_"group"_**, and **_"other"_** all have read permissions. The third and sixth characters are **w**, which indicates that only the **_"user"_** and **_"group"_** have write permissions. No one has execute (**x**) permissions for **_"project_t.txt"_**.

### 2. Change File Permissions:
The organization requested that the **_"other"_** owner type should not have write (**w**) access to any of the files. I checked for any files in the projects directory with write (**w**) permission for the **_"other"_** owner type and found that **_"project_k.txt"_** had such permission. The code below shows how I removed the write permission:

![change file permision without hidden files](https://github.com/user-attachments/assets/33928143-5fbc-4ed9-bc42-c38afcb039be)
*Ref 3: Change file permissions*

- The first line in the screenshot shows the command I entered: **_chmod o-w project_k.txt_**
- The **_chmod_** command changes the permissions on files and directories. The first argument indicates what permission should be changed, and the second argument specifies the file or directory. The **o** represents **_"other"_** the **-w** removes write access, and **_"project_k.txt"_** is the file being modified.
- The second line in the screenshot displays the command I entered: **_ls -l_**. I used this to review the updates I made. The other lines display the output of the second command.

The organization also required that **_"project_m.txt"_** should not be readable or writable by the **_"group"_** or **_"other"_** owner types. Since **_"project_m.txt"_** had read permission for the **_"group"_**, I entered the following commands: **_chmod g-r project_m.txt_** and **_ls -l_**.
- The **_chmod g-r project_m.txt_** command removes read (**r**) permission from the **_"group"_** (**g**) owner type.
- The **_ls -l_** command was used to review the updates I made. The output of this command confirms that the **_"group"_** no longer had read access to the **_"project_m.txt"_** file as shown in the screenshot below:

![change file permision without hidden file 2](https://github.com/user-attachments/assets/f0ae72aa-eb4f-4e1f-8a41-850de521900d)
*Ref 4: Change file permissions*
  
### 3. Change File Permissions on a Hidden File:
The organization stated that **_".project_x.txt"_**, a hidden archived file, should not be writable by anyone. However, both the **_"user"_** and **_"group"_** owner type should still have read access to it.
I first checked the current permissions on the hidden file using the following command:

![check files and directories including hidden ones](https://github.com/user-attachments/assets/11ce5f1e-b776-401a-8c41-a03eec793ee6)
*Ref 5: checked the current permissions on the hidden file*

- The first line in the screenshot shows the command **_ls -la_**, which lists all files and directories (including hidden ones) with their permissions.
- The output of my command indicates that **_".project_x.txt_"** had write permission for both the **_"user"_** and **_"group"_**, but the **_"group"_** did not have read permission.

To modify the permissions, I entered the following command:

![change permission on hidden file](https://github.com/user-attachments/assets/62e1c941-38c4-4d6b-87f6-39e9b117a83d)
*Ref 6: Change file permissions on a hidden file*

- The **_chmod u-w,g-w,g+r .project_x.txt_** removes write permission from the **_"user"_** (**u-w**) and **_"group"_** (**g-w**) while adding read permission for the **_"group"_** (**g+r**) to the **_".project_x.txt_** file".
- The **_ls -l_** command was used to review the updates I made.

### 4. Change Directory Permissions:
The organization requested that the execute permission for the **_"group"_** owner type be removed from the **_"drafts"_** directory.

![change directory permission](https://github.com/user-attachments/assets/0020e42d-7915-4033-a9be-4defd1a7f222)
*Ref 7: Change directory permissions*

- To remove the execute (**x**) permission, I used the command: **_chmod g-x drafts_**. The **g** represents the **_"group"_**, and **-x** removes execute permission from the **_"draft"_** directory.
- I used the **_ls -l_** command to review the updates I made. The output of my command confirms that the execute permission for the **_"group"_** had been removed from the **_"drafts"_** directory.


## Summary

I successfully updated the permissions of various files and directories in the **_projects_** directory to match the organization’s security requirements. I began by using the **_ls -l_** and **_ls -la_** commands to audit existing permissions and then applied the **_chmod_** command multiple times to implement the necessary permission changes for files and directories.
