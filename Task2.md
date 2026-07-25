# Task 2 Linux permissions

## Objective

> Task 2 is to demonstrate a practical understanding of **Linux file ownership and permission management** You will implement this by creating a secure directory structure and configuring strict access controls for specific user groups while **Restricting unauthorized users**

- ## Create the following directory structure:

```bash

company/
├── developers/
├── testers/
└── shared/
```
 ## **For Creating folder in this structure we can do that**

- ### First Option

```bash
mkdir company
```
**Note:-  Then we go inside the directory and create realted directorys.**

- ### Second Option

```bash
mkdir -p company/{developers,testers,shared}
```
## Verify 

> First install the tree packages in our device **sudo apt install tree**.

```bash
tree company
```
## Creat groups
```bash
sudo addgroup developers
sudo addgroup testers
```
- It will create **developers** or **testers** groups.

## Verify 
```bash
grep developers /etc/group
grep developers /etc/group
```

## Assign Ownership

- Set the owner to root and assign the appropriate group

```bash
sudo chown root:developers company/developers
sudo chown root:testers company/testers
sudo chown root:developers company/shared
```
-  Both groups need access to shared, so i will grant the testers group access using an Access Control List.

```bash
sudo setfacl -m g:testers:rwx company/shared
sudo setfacl -d -m g:testers:rwx company/shared
```
## Breakdown these cmd's
> - sudo setfacl -m g:testers:rwx company/shared

### Breakdown:

- sudo – Run the command as administrator.
- setfacl – Modify the ACL of a file or directory.
- -m – Modify (add or change) an ACL entry.
- g:testers:rwx
- g = group
- testers = group name
- rwx = Read, Write, Execute permissions
- company/shared – Target directory.

## Effect

- The testers group immediately gets full permissions on the company/shared directory.

> - sudo setfacl -d -m g:testers:rwx company/shared

## Breakdown:

Additional option

- -d = Set a default ACL.

This does not change permissions on existing files.

Instead, it says:

> Any new file or folder created inside company/shared should automatically give the testers group rwx permissions, subject to the file's creation mode and ACL mask. 

## Second way to share the access of shared to developers and testers group.
- We can simpaly add users to groups.
```bash
sudo usermod -aG developers priya
sudo usermod -aG testers raj
```
> So both groups to access shared without ACLs, simply make every user who needs the shared directory a member of the developers group as well.

```bash
sudo usermod -aG developers raj

````
### Then:

- priya → member of developers
- raj → member of testers and developers

> This works because Linux permissions allow only one owning group per file or directory. Without using ACLs, the common solution is to give shared users membership in that group.


## Set Permissions.

- Here we set Read, Write and Execute (rwx) permission to Owner and Group.

```bash
sudo chmod 770 comapny/developers
sudo chmod 770 comapny/testers
sudo chmod 770 company/shared
```
## Why These Permissions Were Selected
### Developers Directory (770)
- Owner (root): Full control (rwx)
- Group (developers): Full access (rwx)
- Others: No permissions (---)

### This ensures that only members of the developers group can access the directory, while testers and all other users are denied access.

### Testers Directory (770)
- Owner (root): Full control
- Group (testers): Full access
- Others: No permissions

### This allows only the testers group to access their directory.

### Shared Directory (770 + ACL)
- Owner (root): Full control
- Primary Group (developers): Full access
- ACL: Grants the testers group full access (rwx)
- Others: No permissions

> A standard Linux directory can have only one owning group. To allow both the developers and testers groups to access the same directory while denying everyone else, an Access Control List (ACL) is used. This provides additional group permissions without changing the directory's primary group.