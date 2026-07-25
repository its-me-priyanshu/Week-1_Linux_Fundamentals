# Task 1 - User and Group Managment by a Password.

## Objective
The first task regarding User and Group Management, with configure password policies, the specific objective is to perform user and group administration using standard Linux commands.

# Commands used

## 1. Print the Current directory
```bash
pwd
```

**Explanation**

- `pwd `   Shows the current working directory.

---
## Adding user with two approches

**1. sudo useradd "Name"***
```bash
sudo useradd (Name) 
```
**Explanation**

- Create a user, By default, it may not create a home directory or set a password unless you specify additional options.

**2.  sudo adduser "Name"**

```bash
sudo adduser Ram
```
**Explanation**
-  Creates the user, home directory, default shell, and prompts for a password.

## Verify
```bash
id Ram
```
**Output**

> uid=1003(Ram) gid=1003(Ram) groups=1003(Ram) 100(users)

---

## Adding the Group

```bash
sudo groupadd Dev
```

**Explanation**
- Create the group

## Verify
```bash
grep Dev /etc/group
```
**Output**

> Dev:x:1004:
---

## Adding the user to group
```bash
sudo usermod -aG Dev Ram
```
- usermod → Modify an existing user.
- -a → Append (don't remove existing groups).
- -G → Supplementary groups.
- Dev → Group to add.
- Ram → User.

> Without -a, the user would be removed from other supplementary groups.

## Verify

```bash
id Ram
```
**Output**

> uid=1003(Ram) gid=1003(Ram) groups=1003(Ram),100(users),1004(Dev)
---

## Configure password expire in Days

```bash
sudo chage -M 30 Ram
```
> We can set the password expiry limit.
- chage → Change password aging information.
- -M → Maximum number of days before password expires.
- 30 → Password expires after 30 days.

## Verify

```bash
sudo chage -l Ram
```
- Last password change                                    : * **, **
- Password expires                                        : ** **, ****
- Password inactive                                       : never
- Account expires                                         : never
- Maximum number of days between password change          : 30
- Minimum number of days between password change          : 0
- Number of days of warning before password expires       : 7

---

## Force password change on first login.

```bash
sudo change -d 0 Ram
```
- -d → Sets the last password change date.
- 0 → Makes the password immediately expire.
> User must change the password at next login.

## Verify

```bash
sudo chage -l Ram
```
**Output**

> Last password change : password must be changed
---