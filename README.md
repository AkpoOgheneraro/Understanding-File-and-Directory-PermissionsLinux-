
# Understanding File and Directory Permissions in Linux

## Introduction
File and directory permissions are a fundamental aspect of the Linux file system. They determine who can access a file and what actions they can perform. Linux offers a structured permission system to manage security and privacy, making it an essential skill for system administrators and users alike.

In this article, we will explore:
- What Linux file permissions are
- How to view file and directory permissions
- How to modify permissions using different methods
- How to change file ownership
- How to use Access Control Lists (ACLs) for more fine-grained control

Let's dive into how Linux defines and manages file permissions.

## 1. Linux File Permissions: The Basics
Each file and directory in Linux has three permission types:

- **Read (r):** Allows viewing the file content or listing a directory.
- **Write (w):** Allows modifying the file content or adding/removing files in a directory.
- **Execute (x):** Allows executing a file as a program or accessing a directory.

These permissions apply to three categories of users:

- **Owner (User - u):** The user who created the file.
- **Group (g):** A collection of users with shared access.
- **Others (o):** Everyone else on the system.

Understanding these permission structures allows for better control over file security and accessibility.

## 2. Viewing File and Directory Permissions
To check the permissions of files and directories, use the following command:

```bash
ls -l
```

### Example Output:
```bash
-rw-r--r-- 1 ec2-user ec2-user 1024 Feb 28 12:00 myfile.txt
```

### Breakdown:
| Symbol | Meaning |
|---------|-----------|
| - | Regular file (`d` for directory) |
| rw- | Owner has read (`r`) and write (`w`) permissions |
| r-- | Group has read-only (`r`) permission |
| r-- | Others have read-only (`r`) permission |

The first character (`-` or `d`) represents whether it is a file (`-`) or a directory (`d`). The next nine characters define the owner, group, and others' permissions.

## 3. Modifying Permissions with chmod
The `chmod` command is used to change file and directory permissions. Linux provides two ways to modify permissions:

### A. Absolute Mode (Using Numbers)
Each permission type is assigned a number:

- Read (r) = 4
- Write (w) = 2
- Execute (x) = 1

Sum the values to set permissions.

#### Example: Changing Permissions
```bash
chmod 640 myfile.txt  # Owner: read/write (6), Group: read-only (4), Others: no access (0)
chmod 755 myscript.sh  # Owner: full permissions (7), Group & Others: read/execute (5)
```

### B. Symbolic Mode (Using Letters)
In symbolic mode, permissions are modified using letters.

#### Syntax:
```bash
chmod [User] [Operator] [Permission] filename
```

| User Types | Operators |
|------------|----------|
| u → Owner | + → Add a permission |
| g → Group | - → Remove a permission |
| o → Others | = → Set exact permissions |
| a → All (Owner, Group, Others) |  |

#### Example: Modifying Permissions
```bash
chmod u+x myfile.txt  # Grant execute (x) permission to the owner
chmod g-w myfile.txt  # Remove write (w) permission from the group
chmod a=r myfile.txt  # Set exact read (r) permissions for all
```

### C. Changing Directory Permissions Recursively
To modify permissions for all files inside a directory:
```bash
chmod -R 644 mydir
```

## 4. Changing File Ownership with chown
The `chown` command allows changing the owner of a file or directory.

#### Syntax:
```bash
chown new_owner filename
```

#### Example:
```bash
chown ec2-user myfile.txt  # Change file owner to ec2-user
chown new_owner:new_group myfile.txt  # Change both owner and group
```

To apply ownership change to all files inside a directory:
```bash
chown -R new_owner:new_group mydir
```

## 5. Changing Group Ownership with chgrp
The `chgrp` command changes group ownership.

#### Syntax:
```bash
chgrp new_group filename
```

#### Example:
```bash
chgrp developers myfile.txt  # Change group ownership to "developers"
```

## 6. Using Access Control Lists (ACLs) for Advanced Permissions
Standard owner/group/others permissions may not always be sufficient. ACLs (Access Control Lists) allow assigning specific permissions to multiple users.

### Viewing ACLs
```bash
getfacl myfile.txt
```

### Setting ACLs
```bash
setfacl -m u:ec2-user:rw myfile.txt  # Grant read & write to ec2-user
```

### Removing ACL Entries
```bash
setfacl -x u:ec2-user myfile.txt
```

### Applying ACL Changes Recursively
```bash
setfacl -R -m u:ec2-user:rw mydir
```

## 7. Summary
✅ **File permissions** define who can read, write, or execute files and directories.<br>
✅ **View permissions** with `ls -l`.<br>
✅ **Modify permissions** using `chmod` (absolute mode & symbolic mode).<br>
✅ **Change ownership** using `chown`.<br>
✅ **Modify group ownership** with `chgrp`.<br>
✅ **Use ACLs** for advanced access control.<br>

## Next Steps
Now that you understand file and directory permissions, the next lesson will cover user and group management in Linux.

