# Active Directory (AD)

# Introduction

Before Active Directory existed, managing users and computers in a company network was difficult. Every computer had its own user accounts, passwords, and settings. As organizations grew, managing thousands of users and devices became time-consuming and insecure.

Microsoft introduced **Active Directory (AD)** to solve these problems by providing a centralized system for managing users, computers, security, and network resources.

---

# What is Active Directory?

**Active Directory (AD)** is a **Microsoft directory service** that stores, organizes, and manages information about network resources such as users, computers, servers, printers, groups, and shared folders.

It provides a **centralized database** that allows administrators to manage an entire Windows network from one location.

### Example

A company has:

- 5,000 employees
    
- 3,000 computers
    
- 200 printers
    
- Multiple servers
    
- Shared folders
    
- Company applications
    

Without Active Directory, the administrator would have to manage every computer separately.

With Active Directory:

1. Create a user account once.
    
2. Join computers to the domain.
    
3. Manage permissions from a central location.
    
4. Apply security policies to all computers.
    

Everything is managed from one place.

---

# Why was Active Directory created?

Before Active Directory, Windows computers used **local user accounts**.

Each computer stored its own:

- Users
    
- Passwords
    
- Permissions
    

If a company had 500 computers, the administrator had to create and manage user accounts on each computer individually.

### Example

A new employee named John joins the company.

Without Active Directory:

```
PC001
Create John

PC002
Create John

PC003
Create John

...

PC500
Create John
```

The administrator must repeat the same task hundreds of times.

With Active Directory:

```
Active Directory
       |
       └── Create John Once
               |
               ├── PC001
               ├── PC002
               ├── PC003
               └── PC500
```

John can use the same username and password to log in to any domain-joined computer.

---

# What problems does Active Directory solve?

Active Directory solves many problems found in large networks.

### 1. Centralized User Management

Instead of creating users on every computer, administrators create user accounts only once.

Example:

```
Create User: John

↓

John can log in to every domain computer.
```

---

### 2. Centralized Authentication

Users only need one username and password.

Example:

```
Username: john
Password: ******

↓

Domain Controller verifies the credentials.
```

The user does not need separate accounts for different computers.

---

### 3. Centralized Policy Management

Administrators can apply security settings to all computers at once.

Example:

```
Company Policy

↓

- Password must be 12 characters
- Disable USB storage
- Install Microsoft Office
- Enable Firewall
```

Every computer receives the same policy automatically.

---

### 4. Resource Management

Active Directory stores information about:

- Users
    
- Computers
    
- Groups
    
- Printers
    
- Shared folders
    
- Servers
    

Making resources easy to find and manage.

---

### 5. Scalability

Active Directory is designed to support both small and very large organizations.

Example:

```
Small Company

50 Users
20 Computers

↓

Large Enterprise

100,000 Users
50,000 Computers
```

The same system can manage both environments.

---

# What are the main functions of Active Directory?

Active Directory performs several important functions.

### Authentication

Verifies the identity of a user or computer.

Simple question:

```
"Who are you?"
```

Example:

```
Username: john
Password: ******

↓

AD checks if the credentials are valid.
```

---

### Authorization

Determines what a user is allowed to access after authentication.

Simple question:

```
"What are you allowed to access?"
```

Example:

```
John

↓

✔ Shared Folder
✔ Printer
✖ HR Database
```

---

### Centralized Management

Allows administrators to manage:

- Users
    
- Computers
    
- Groups
    
- Servers
    

from a single location.

---

### Policy Management

Applies security settings using **Group Policy**.

Example:

```
Group Policy

↓

- Disable USB
- Change password every 60 days
- Install company software
```

---

### Resource Organization

Stores network resources in an organized directory.

Example:

```
Active Directory

├── Users
├── Computers
├── Groups
├── Printers
└── Shared Folders
```

---

### Security Management

Helps protect the network by enforcing:

- Password policies
    
- Account lockout rules
    
- User permissions
    
- Access control
    

---

# What is Active Directory Domain Services (AD DS)?

**Active Directory Domain Services (AD DS)** is the **core server role of Active Directory** that stores directory information and provides authentication, authorization, and centralized management for a Windows domain.

AD DS is the part of Active Directory that most administrators work with every day.

It stores information about:

- Users
    
- Computers
    
- Groups
    
- Organizational Units (OUs)
    
- Domains
    
- Security policies
    

It also authenticates users when they log in to the domain.

### Example

```
User Login

Username: john
Password: ******

        |
        v

Active Directory Domain Services (AD DS)

        |
        ├── Check username
        ├── Check password
        ├── Check group membership
        └── Return login result
```

Without AD DS, users cannot log in to a Windows domain or access domain resources.

---

# What is the difference between Active Directory and AD DS?

Many people use **Active Directory** and **AD DS** as if they mean the same thing, but they are not exactly the same.

**Active Directory** is the overall directory service platform provided by Microsoft.

**AD DS** is the core component (server role) that provides domain services such as storing directory data, authenticating users, and managing domains.

Think of Active Directory as a family of directory-related services, while AD DS is the main service responsible for domain management.

### Example

```
Active Directory

├── Active Directory Domain Services (AD DS)
├── Active Directory Certificate Services (AD CS)
├── Active Directory Federation Services (AD FS)
└── Active Directory Lightweight Directory Services (AD LDS)
```

# Active Directory Structure

Active Directory stores information in a **hierarchical structure**.

A hierarchy means everything is organized from the **largest container to the smallest container**.

Think of it like folders inside folders on your computer.

The Active Directory hierarchy looks like this:

```text
Forest
│
├── Tree
│    │
│    ├── Domain
│    │      │
│    │      ├── Organizational Unit (OU)
│    │      │      ├── Users
│    │      │      ├── Computers
│    │      │      └── Groups
│    │      │
│    │      └── Another OU
│    │
│    └── Another Domain
│
└── Another Tree
```

The four main components are:

- Forest
    
- Tree
    
- Domain
    
- Organizational Unit (OU)
    

Each level helps organize resources more efficiently.

---

# What is a Forest?

A **Forest** is the **highest level container** in Active Directory.

It is the top-most structure that contains one or more trees.

All trees inside a forest share:

- A common Active Directory schema
    
- A common configuration
    
- A Global Catalog
    
- Automatic trust relationships
    

You can think of a forest as the entire Active Directory environment of an organization.

### Example

A company owns two different businesses.

One business uses:

```
company.com
```

Another business uses:

```
subsidiary.com
```

Both belong to the same organization.

They can exist inside one forest.

```text
Forest
│
├── company.com
│
└── subsidiary.com
```

Even though the domain names are different, they are managed under the same forest.

---

# What is a Tree?

A **Tree** is a collection of one or more domains that share the **same DNS namespace**.

The first domain is called the **root domain**.

Additional domains are called **child domains**.

### Example

Suppose a company owns the domain:

```
company.com
```

Later, the company creates separate domains for different locations.

```text
company.com
│
├── usa.company.com
├── india.company.com
└── uk.company.com
```

All these domains belong to the same tree because they share the root domain:

```
company.com
```

Since they share the same DNS namespace, they form one tree.

---

# What is a Domain?

A **Domain** is the **basic administrative and security boundary** in Active Directory.

It is a logical group of users, computers, groups, and other resources that are managed together.

Each domain has:

- User accounts
    
- Computer accounts
    
- Groups
    
- Password policies
    
- Security settings
    

A domain is managed by one or more **Domain Controllers (DCs)**.

### Example

A company creates a domain called:

```
company.com
```

Inside the domain:

```text
company.com

Users
- John
- Mary
- Alex

Computers
- PC001
- PC002
- Laptop01
```

All these resources belong to the same domain.

The administrator manages everything from one place.

---

# How are Forest, Tree, Domain, and OU related?

These components are related through a hierarchy.

A **Forest** contains one or more **Trees**.

A **Tree** contains one or more **Domains**.

A **Domain** contains one or more **Organizational Units (OUs)**.

An **OU** contains Active Directory objects such as users, computers, and groups.

```text
Forest
│
├── Tree
│     │
│     ├── Domain
│     │      │
│     │      ├── OU
│     │      │     ├── Users
│     │      │     ├── Computers
│     │      │     └── Groups
│     │      │
│     │      └── Another OU
│     │
│     └── Another Domain
│
└── Another Tree
```

### Real-World Example

A company called **ABC Corporation** operates in multiple countries.

```text
Forest
│
├── abc.com (Tree)
│      │
│      ├── usa.abc.com (Domain)
│      │      ├── HR OU
│      │      ├── IT OU
│      │      └── Finance OU
│      │
│      └── india.abc.com (Domain)
│             ├── HR OU
│             ├── Sales OU
│             └── Support OU
│
└── xyz.com (Another Tree)
       │
       └── xyz.com (Domain)
              ├── HR OU
              └── IT OU
```

In this example:

- **Forest** contains the entire Active Directory environment.
    
- **abc.com** and **xyz.com** are separate trees.
    
- **usa.abc.com** and **india.abc.com** are domains.
    
- **HR**, **IT**, **Sales**, and **Support** are Organizational Units (OUs).
    
- Users, computers, and groups are stored inside the OUs.
    

This keeps the Active Directory environment organized, scalable, and easy to manage.

# Domain Controller

## What is a Domain Controller (DC)?

A **Domain Controller (DC)** is a **server that runs Active Directory Domain Services (AD DS)** and manages a Windows domain.

It stores the Active Directory database and is responsible for authenticating users, authorizing access, and managing domain resources.

Simple definition:

**Domain = the Active Directory environment**  
**Domain Controller = the server that stores and manages that environment**

The Active Directory database is stored in the following file:

```text
NTDS.dit
```

This database contains information about:

- Users
    
- Computers
    
- Groups
    
- Organizational Units (OUs)
    
- Password hashes
    
- Security policies
    

### Example

```text
User Login

Username: john
Password: ******

        |
        v

Domain Controller

        |
        ├── Verify username
        ├── Verify password
        ├── Check group membership
        └── Allow or deny access
```

The Domain Controller decides whether a user is allowed to log in and what resources they can access.

---

## What are the responsibilities of a Domain Controller?

A Domain Controller performs several important tasks in an Active Directory environment.

Its responsibilities include:

- Authenticating users and computers
    
- Authorizing access to resources
    
- Storing the Active Directory database
    
- Applying Group Policies
    
- Managing user, computer, and group accounts
    
- Replicating Active Directory data with other Domain Controllers
    

### Example

When John logs in:

```text
John

↓

Domain Controller

↓

Check Username
Check Password
Check Groups
Check Permissions

↓

Login Allowed
```

The Domain Controller verifies John's identity before allowing access to company resources.

---

## Can a Domain have multiple Domain Controllers?

Yes.

A single domain can have **one or more Domain Controllers (DCs)**.

Every Domain Controller stores a copy of the Active Directory database.

### Example

```text
company.com

        |
   -----------------
   |               |
  DC1             DC2
   |               |
   -----------------
        |
  Same AD Database
```

If a new user is created on one Domain Controller, the information is automatically replicated to the other Domain Controllers.

---

## Why are multiple Domain Controllers used?

Organizations use multiple Domain Controllers to improve **availability, reliability, and performance**.

### High Availability

If one Domain Controller fails, another Domain Controller continues providing Active Directory services.

### Example

```text
DC1 (Offline)
      X

      |

DC2 (Online)

↓

Users can still log in.
```

---

### Load Balancing

When many users log in at the same time, authentication requests are shared between multiple Domain Controllers.

### Example

```text
Users

      |

-------------------------
|           |           |
DC1        DC2        DC3
```

This reduces the workload on a single server and improves login performance.

---

### Fault Tolerance

If a Domain Controller is shut down for maintenance or experiences a hardware failure, another Domain Controller continues serving users.

This helps prevent downtime.

---

### Replication

All Domain Controllers keep their Active Directory databases synchronized.

### Example

```text
Create User: John

      |

     DC1

      |

Replication

      |

     DC2

      |

     DC3
```

Every Domain Controller receives the updated information, ensuring that users can log in from anywhere in the domain using the same credentials.

# Organizational Units (OU)

## What is an OU?

An **Organizational Unit (OU)** is a **container inside a domain** used to organize and manage Active Directory objects.

An OU can contain:

- Users
    
- Computers
    
- Groups
    
- Other OUs
    

OUs help administrators organize resources based on departments, locations, or teams.

### Example

```text
company.com
│
├── HR OU
│      ├── Mary (User)
│      └── HR-PC01 (Computer)
│
├── IT OU
│      ├── John (User)
│      └── Server01
│
└── Finance OU
       └── Alex (User)
```

Instead of storing all users and computers together, they are organized into separate OUs.

---

## Why are OUs used?

OUs make Active Directory easier to manage.

They are used to:

- Organize users and computers
    
- Apply Group Policies (GPOs)
    
- Delegate administrative control
    
- Separate departments or locations
    

### Example

The IT department should not be allowed to use USB drives.

The administrator applies the policy only to the IT OU.

```text
IT OU

↓

Disable USB Storage
```

Only users and computers inside the IT OU receive this policy.

The HR and Finance departments are not affected.

---

## Can OUs contain other OUs?

Yes.

An **Organizational Unit (OU)** can contain **other OUs**. These are called **nested OUs**.

Nested OUs help organize large organizations into smaller departments or teams.

### Example

A company has an IT department with different teams.

```text
company.com
│
└── IT OU
      │
      ├── Servers OU
      │      ├── Server01
      │      └── Server02
      │
      ├── Support OU
      │      ├── John
      │      └── Mary
      │
      └── Development OU
             ├── Alex
             └── David
```

The **IT OU** contains three smaller OUs.

This makes the Active Directory structure easier to organize and manage.

---

## How are OUs different from Domains?

Although both **Domains** and **Organizational Units (OUs)** are used to organize Active Directory, they serve different purposes.

A **Domain** is a **security and administrative boundary**.

An **OU** is a **container used to organize objects inside a domain**.

### Example

```text
company.com (Domain)
│
├── HR OU
├── IT OU
└── Finance OU
```

The **Domain** is the main boundary.

The **OUs** organize users, computers, and groups within that domain.

### Differences

|Domain|Organizational Unit (OU)|
|---|---|
|Security and administrative boundary|Logical container inside a domain|
|Contains users, computers, groups, and OUs|Contains users, computers, groups, and other OUs|
|Can have one or more Domain Controllers|Does not have a Domain Controller|
|Has its own security policies and database|Used to organize objects, apply Group Policy, and delegate administration|
|Can contain multiple OUs|Cannot contain Domains|

# Active Directory Objects

## What is an AD Object?

An **Active Directory (AD) Object** is **anything stored inside the Active Directory database**.

Every user, computer, group, printer, or shared folder is stored as an object.

Think of an object as a **record** that represents a resource in Active Directory.

### Examples of AD Objects

- User
    
- Computer
    
- Group
    
- Printer
    
- Shared Folder
    
- Organizational Unit (OU)
    
- Domain
    

### Example

```text
Active Directory

├── John (User)
├── PC001 (Computer)
├── IT-Team (Group)
├── Printer01
└── HR OU
```

Everything stored in Active Directory is an object.

---

## What types of objects exist?

Active Directory contains many different object types.

The most common object types are:

### User Object

Represents a person who needs access to network resources.

Example:

```text
John
Mary
Alex
```

---

### Computer Object

Represents a computer that has joined the domain.

Example:

```text
PC001
Laptop01
Server01
```

---

### Group Object

Represents a collection of users or computers.

Example:

```text
IT-Team
HR-Team
Finance-Team
```

---

### Organizational Unit (OU)

Represents a container used to organize objects.

Example:

```text
HR OU
IT OU
Finance OU
```

---

### Printer Object

Represents a network printer.

Example:

```text
OfficePrinter01
```

---

### Shared Folder Object

Represents a shared network folder.

Example:

```text
\\Server01\HR
```

---

## What is an Object Class?

An **Object Class** defines **what type of object can exist in Active Directory**.

It acts like a **blueprint** for an object.

The object class determines:

- What the object represents
    
- Which attributes it can have
    

### Example

If an object belongs to the **User** class, it can have attributes like:

- Username
    
- Email
    
- Password
    
- Department
    

If an object belongs to the **Computer** class, it can have attributes like:

- Computer Name
    
- Operating System
    
- DNS Name
    

### Example

```text
Object Class

User
│
├── Username
├── Email
├── Department
└── Password

Computer
│
├── Hostname
├── DNS Name
└── Operating System
```

Each object must belong to an object class.

---

## What is an Attribute?

An **Attribute** is a **piece of information stored about an object**.

Attributes describe the properties of an object.

### Example

User object:

```text
Object: John

Attributes

Name = John Smith
Username = john
Email = john@company.com
Department = IT
Phone = 123456789
```

The object is **John**.

Everything that describes John is stored as attributes.

---

## What is the difference between an Object and an Attribute?

An **Object** is the item stored in Active Directory.

An **Attribute** is information that describes that object.

### Example

```text
Object

John
```

Attributes of John:

```text
Name = John Smith
Username = john
Email = john@company.com
Department = IT
Phone = 123456789
```

John is the object.

The name, email, department, and phone number are attributes.

Another example:

```text
Computer Object

PC001

Attributes

Hostname = PC001
Operating System = Windows 11
IP Address = 192.168.1.20
```

The computer is the object.

Its hostname, operating system, and IP address are attributes.

# Users

## What is a User object?

A **User object** is an **Active Directory object that represents a person who needs access to network resources**.

A user object stores information about a user and is used for:

- Authentication (verifying identity)
    
- Authorization (determining permissions)
    
- Accessing company resources
    

Every employee who needs to log in to the company's network has a user object in Active Directory.

### Example

A company hires a new employee named John.

The administrator creates a user object for him.

```text
User Object

Name: John Smith
Username: john
Password: ********
```

John can now use this account to:

- Log in to domain computers
    
- Access shared folders
    
- Use company applications
    
- Print documents
    
- Access email
    

---

## What information does a User object store?

A user object stores information called **attributes**.

These attributes describe the user.

Common information includes:

- Full Name
    
- Username (sAMAccountName)
    
- User Principal Name (UPN)
    
- Email Address
    
- Department
    
- Job Title
    
- Phone Number
    
- Password
    
- Group Membership
    
- Security Identifier (SID)
    

### Example

```text
User Object

Name           = John Smith
Username       = john
UPN            = john@company.com
Email          = john@company.com
Department     = IT
Job Title      = System Administrator
Phone          = +1 555-1234
```

Active Directory stores all of this information in its database.

---

## User Login Example

John enters his credentials on a company computer.

```text
Username: john
Password: ********
```

The computer sends the login request to the **Domain Controller (DC)**.

```text
John

↓

Domain Controller

↓

Check Username
Check Password
Check User Account
Check Group Membership

↓

Login Allowed
```

If everything is correct, John is allowed to log in.

Otherwise, access is denied.

---

## What types of User accounts exist?

Active Directory supports different types of user accounts.

---

### Normal User Account

A **Normal User Account** is used by employees to access company resources.

These users have limited permissions.

### Example

```text
john
mary
alex
```

A normal user can:

- Log in to domain computers
    
- Access shared folders
    
- Use company applications
    

They cannot perform administrative tasks unless permission is granted.

---

### Administrator Account

An **Administrator Account** is used by IT administrators to manage the Active Directory environment.

Administrator accounts have elevated privileges.

### Example

```text
Administrator

Domain Admin
```

Administrators can:

- Create users
    
- Delete users
    
- Reset passwords
    
- Manage computers
    
- Configure servers
    
- Change security settings
    

---

### Service Account

A **Service Account** is used by applications or services instead of people.

These accounts allow services to communicate securely with other systems.

### Example

```text
SQL_Service

Backup_Service

WebApp_Service
```

A database server may use:

```text
Username: SQL_Service
Password: ********
```

to connect to other servers automatically without requiring a person to log in.

---

### Built-in User Accounts

Active Directory also creates several built-in accounts during domain installation.

Examples include:

- Administrator
    
- Guest
    
- KRBTGT
    

These accounts are used for system administration and authentication.

They will be discussed in detail in the **Built-in Components** section.

# Groups

## What is a Group?

A **Group** is an **Active Directory object used to collect users, computers, or other groups together**.

Instead of managing permissions for every user individually, administrators assign permissions to a group.

Every member of that group automatically receives the assigned permissions.

### Example

A company has three IT employees.

```text
John
Mary
Alex
```

Instead of managing each user separately, the administrator creates a group.

```text
IT-Team

Members

- John
- Mary
- Alex
```

Now the administrator can manage all three users through one group.

---

## Why are Groups used?

Groups make Active Directory easier to manage.

They are used to:

- Assign permissions
    
- Control access to resources
    
- Apply security settings
    
- Simplify administration
    

Instead of assigning permissions to every user, administrators assign permissions to a group.

### Example

Without Groups

```text
Payroll Folder

John  → Read
Mary  → Read
Alex  → Read
David → Read
Sarah → Read
```

The administrator must assign permissions to every user.

With Groups

```text
Payroll-Team

Members

- John
- Mary
- Alex
- David
- Sarah

↓

Payroll-Team

↓

Read Payroll Folder
```

Every member automatically receives access.

This is much easier to manage.

---

## What is Group Membership?

**Group Membership** means a user, computer, or another group belongs to a group.

The objects inside a group are called **members**.

### Example

```text
Group

Developers

Members

- John
- Mary
- Alex
```

John is a member of the **Developers** group.

Mary is also a member of the same group.

Since they belong to the group, they receive the permissions assigned to it.

---

## What are Security Groups?

A **Security Group** is a group used to assign **permissions** to network resources.

Security Groups control who can access:

- Files
    
- Shared folders
    
- Printers
    
- Applications
    
- Servers
    

They are the most commonly used group type in Active Directory.

### Example

```text
Security Group

Finance-Team

↓

Permission

Access Finance Folder
```

Every user who belongs to the **Finance-Team** group can access the Finance folder.

---

### Another Example

```text
Finance-Team

Members

- John
- Mary

↓

Finance Server

↓

Read and Write Access
```

Instead of assigning permissions to John and Mary separately, the administrator assigns them once to the group.

---

## What are Distribution Groups?

A **Distribution Group** is used for **email distribution**.

Unlike Security Groups, Distribution Groups **do not provide security permissions**.

They are mainly used with email systems such as Microsoft Exchange.

### Example

```text
Distribution Group

All-Employees

Members

- John
- Mary
- Alex
```

When an email is sent to:

```text
all-employees@company.com
```

Every member of the group receives the email.

Distribution Groups cannot be used to control access to files or folders.

---

## Difference between Security Groups and Distribution Groups

|Security Group|Distribution Group|
|---|---|
|Used for assigning permissions|Used for sending emails|
|Controls access to resources|Does not control access|
|Can secure files, folders, printers, and servers|Used only for email distribution|
|Most common group type|Mainly used with email systems|

---

## What are the common built-in Groups?

When Active Directory is installed, several groups are created automatically.

These are called **built-in groups**.

---

### Domain Admins

The **Domain Admins** group contains administrators who have full control over the domain.

Members can:

- Create users
    
- Delete users
    
- Reset passwords
    
- Manage Domain Controllers
    
- Configure security settings
    

### Example

```text
User

Admin01

↓

Member Of

Domain Admins
```

Admin01 has administrative privileges across the entire domain.

---

### Domain Users

The **Domain Users** group is the default group for normal user accounts.

When a new user is created, they automatically become a member of this group.

### Example

```text
Domain Users

- John
- Mary
- Alex
```

Most employees belong to the **Domain Users** group.

---

### Domain Computers

The **Domain Computers** group contains all computers that have joined the domain.

### Example

```text
Domain Computers

- PC001
- Laptop01
- Server01
```

Every domain-joined computer automatically becomes a member of this group.

---

### Domain Controllers

The **Domain Controllers** group contains all Domain Controllers in the domain.

### Example

```text
Domain Controllers

- DC01
- DC02
```

Only Domain Controllers belong to this group.

---

### Enterprise Admins

The **Enterprise Admins** group has the highest administrative privileges in an Active Directory forest.

Members can manage:

- All domains in the forest
    
- Forest-wide configuration
    
- Active Directory Schema
    
- Trust relationships
    

### Example

```text
Forest

├── company.com
├── branch.company.com
└── sales.company.com

↓

Enterprise Admins

↓

Manage Entire Forest
```

Enterprise Admins are typically used only in environments with multiple domains.

---

### Schema Admins

The **Schema Admins** group can modify the Active Directory Schema.

Since schema changes affect the entire forest, only trusted administrators should belong to this group.

### Example

```text
Schema Admins

↓

Modify Active Directory Schema
```

Schema changes are rare and usually performed only when installing applications that extend Active Directory, such as Microsoft Exchange.

# Computers

## What is a Computer object?

A **Computer object** is an **Active Directory object that represents a computer joined to a domain**.

Every computer that joins an Active Directory domain gets its own computer object.

This allows Active Directory to:

- Identify the computer
    
- Authenticate the computer
    
- Apply Group Policies
    
- Manage the computer centrally
    

A computer object is created automatically when a computer joins the domain.

### Example

A company has three computers.

```text
PC001
Laptop01
Server01
```

After joining the domain:

```text
Active Directory

├── PC001
├── Laptop01
└── Server01
```

Each computer is now stored as an Active Directory object.

---

## What is a Computer Account?

A **Computer Account** is the **identity of a computer in Active Directory**.

Just as a user has a user account, every domain-joined computer has its own computer account.

The computer account allows the computer to:

- Authenticate with the Domain Controller
    
- Receive Group Policies
    
- Access domain resources
    
- Communicate securely with other computers
    

Every computer account has its own password, which is managed automatically by Windows.

### Example

A computer named **PC001** joins the domain.

```text
Computer Name

PC001

↓

Computer Account

PC001$
```

The Domain Controller stores this computer account in the Active Directory database.

---

## What happens when a Computer joins a Domain?

When a computer joins a domain, several things happen automatically.

### Step 1

The administrator joins the computer to the domain.

Example:

```text
Computer

PC001

↓

Join Domain

company.com
```

---

### Step 2

The Domain Controller creates a computer account.

```text
Active Directory

↓

Computer Account

PC001$
```

---

### Step 3

The computer receives a secure password.

Unlike users, computers also have passwords.

Windows creates and manages this password automatically.

Users do not know or type this password.

---

### Step 4

A secure trust relationship is established.

```text
PC001

⇄

Domain Controller
```

The computer and Domain Controller trust each other.

This secure relationship allows the computer to communicate safely with the domain.

---

### Step 5

The computer becomes part of the domain.

Now it can:

- Authenticate users
    
- Receive Group Policies
    
- Access shared folders
    
- Access printers
    
- Access company applications
    

---

### Example

```text
Join Domain

PC001

↓

Create Computer Account

↓

Create Secure Password

↓

Trust Relationship

↓

Apply Group Policy

↓

Ready to Use
```

---

## Why do Computer accounts end with `$`?

Computer accounts in Active Directory end with a **dollar sign (`$`)**.

The dollar sign tells Windows that the account belongs to a computer and not a user.

### Example

User account:

```text
john
```

Computer account:

```text
PC001$
```

Server account:

```text
SERVER01$
```

The dollar sign is added automatically by Windows.

Administrators do not need to add it manually.

---

### Why is the `$` important?

It helps Windows distinguish between user accounts and computer accounts.

### Example

Without `$`

```text
john

PC001
```

It is difficult to know which is a user and which is a computer.

With `$`

```text
john

PC001$
```

Windows immediately recognizes **PC001$** as a computer account.

---

### Can users log in with a Computer Account?

No.

Computer accounts are **not used by people**.

They are used only by computers to authenticate with the Domain Controller.

### Example

```text
User

John

↓

Logs in to Windows

✔ Allowed
```

```text
Computer

PC001$

↓

Authenticates with Domain Controller

✔ Allowed
```

The user account and the computer account work together.

- The **user account** identifies the person.
    
- The **computer account** identifies the device.
    

Both must be trusted by Active Directory for a successful domain login.

# Schema

## What is the Active Directory Schema?

The **Active Directory Schema** is a **set of rules that defines what objects can exist in Active Directory and what information those objects can store**.

Think of the schema as the **blueprint** or **rule book** for Active Directory.

It tells Active Directory:

- Which object types can be created
    
- Which attributes each object can have
    
- How objects are stored in the directory
    

Every Domain Controller in the forest uses the same schema.

### Example

Suppose you create a user.

The schema already knows that a user can have:

- Username
    
- Password
    
- Email
    
- Department
    
- Phone Number
    

It also knows that a user **cannot** have attributes that belong only to a computer.

```text
Schema

↓

User Object

├── Username
├── Password
├── Email
├── Department
└── Phone Number
```

The schema defines which information belongs to a user object.

---

## Why is the Schema important?

The schema is important because it keeps the Active Directory database organized and consistent.

Without the schema, every object could store different types of information, making the directory unreliable.

The schema ensures that:

- Every User object follows the same structure.
    
- Every Computer object follows the same structure.
    
- Every Group object follows the same structure.
    
- All Domain Controllers use the same definitions.
    

### Example

Without a schema:

```text
User 1

Name
Email

User 2

Username
Department
Phone

User 3

Password
Address
```

Every user would have a different structure.

With a schema:

```text
User

├── Username
├── Password
├── Email
├── Department
└── Phone
```

Every user object follows the same format.

This makes searching, managing, and securing Active Directory much easier.

---

## What are Classes?

A **Class** defines the **type of object** that can exist in Active Directory.

Think of a class as a **template** for creating objects.

Each class specifies:

- What the object represents
    
- Which attributes it can contain
    

### Common Classes

- User
    
- Computer
    
- Group
    
- Printer
    
- Organizational Unit (OU)
    

### Example

```text
Class

User

↓

Can create

John
Mary
Alex
```

The **User** class is used to create user objects.

---

Another example:

```text
Class

Computer

↓

Can create

PC001
Laptop01
Server01
```

The **Computer** class is used to create computer objects.

---

## What are Attributes in the Schema?

An **Attribute** is a **piece of information that belongs to a class**.

The schema defines which attributes are available for each class.

### Example

User Class

```text
User Class

├── Username
├── Password
├── Email
├── Department
├── Phone
└── Employee ID
```

When a user object is created, these attributes become part of that user.

---

Computer Class

```text
Computer Class

├── Computer Name
├── DNS Name
├── Operating System
├── IP Address
└── Operating System Version
```

Every computer object stores these attributes.

---

### Relationship between Classes and Attributes

A class defines **what an object is**.

Attributes define **what information the object stores**.

### Example

```text
Class

User

↓

Object

John

↓

Attributes

Username = john
Email = john@company.com
Department = IT
Phone = +1 555-1234
```

- **User** is the class.
    
- **John** is the object.
    
- **Username**, **Email**, **Department**, and **Phone** are the attributes.
    

---

### Real-World Analogy

Think of a class as a **form template**.

```text
Student Admission Form

Fields

Name
Age
Address
Phone
```

Every student fills out the same form.

Similarly, in Active Directory:

- The **Class** is the form template.
    
- The **Object** is the completed form.
    
- The **Attributes** are the individual fields filled in on that form.
    

This ensures every object of the same type stores information in a consistent way.

# Naming

## What is a Distinguished Name (DN)?

A **Distinguished Name (DN)** is the **complete unique path of an object in Active Directory**.

It tells Active Directory **exactly where an object is located**.

Think of it as the **full address** of an object.

A Distinguished Name is made up of:

- **CN** (Common Name)
    
- **OU** (Organizational Unit)
    
- **DC** (Domain Component)
    

### Example

Suppose the Active Directory structure looks like this:

```text
company.com
│
├── IT OU
│      └── John
│
└── HR OU
       └── Mary
```

John's Distinguished Name is:

```text
CN=John,OU=IT,DC=company,DC=com
```

Mary's Distinguished Name is:

```text
CN=Mary,OU=HR,DC=company,DC=com
```

Even if two users have the same name, their Distinguished Names are different because their locations are different.

---

### Another Example

Two users are named John.

```text
company.com
│
├── IT OU
│      └── John
│
└── HR OU
       └── John
```

IT John's DN:

```text
CN=John,OU=IT,DC=company,DC=com
```

HR John's DN:

```text
CN=John,OU=HR,DC=company,DC=com
```

The Distinguished Name uniquely identifies each user.

---

## What is a User Principal Name (UPN)?

A **User Principal Name (UPN)** is the **modern logon name used by a user to sign in to Active Directory**.

It looks similar to an email address.

A UPN consists of:

```text
Username@Domain
```

### Example

```text
john@company.com
```

The user enters this name when logging in.

```text
Username

john@company.com

Password

********
```

The Domain Controller uses the UPN to identify the user during authentication.

---

### Why is UPN used?

Earlier versions of Windows used:

```text
DOMAIN\Username
```

Example:

```text
COMPANY\john
```

This was harder for users to remember, especially in environments with multiple domains.

Microsoft introduced the UPN because it is easier to use.

Example:

```text
john@company.com
```

It is simple, familiar, and works like an email address.

---

## What is the difference between DN and UPN?

Although both identify a user in Active Directory, they serve different purposes.

A **Distinguished Name (DN)** identifies **where the object is located** in Active Directory.

A **User Principal Name (UPN)** identifies **how the user logs in**.

### Example

User:

```text
John
```

Distinguished Name:

```text
CN=John,OU=IT,DC=company,DC=com
```

User Principal Name:

```text
john@company.com
```

The DN shows John's location inside Active Directory.

The UPN is the username John types when signing in.

---

### Differences

|Distinguished Name (DN)|User Principal Name (UPN)|
|---|---|
|Identifies the location of an object in Active Directory|Identifies the user during login|
|Used internally by Active Directory|Used by users to sign in|
|Includes CN, OU, and DC components|Uses `username@domain` format|
|Must be unique within Active Directory|Must be unique within the forest|
|Changes if the object is moved to another OU|Usually remains the same even if the object is moved|

---

### Example

```text
company.com
│
└── IT OU
       └── John
```

John's information:

```text
DN

CN=John,OU=IT,DC=company,DC=com

-----------------------------

UPN

john@company.com
```

- The **DN** tells Active Directory where John is stored.
    
- The **UPN** is the name John uses to log in.
  
  # Identity

## What is a Security Identifier (SID)?

A **Security Identifier (SID)** is a **unique value that Windows assigns to every security object in Active Directory**.

Security objects include:

- Users
    
- Groups
    
- Computers
    

Windows uses the SID to identify these objects instead of their names.

Every SID is unique.

Once created, a SID never changes, even if the object's name changes.

### Example

A user named John is created.

```text
User

John
```

Windows automatically assigns a SID.

```text
User

John

SID

S-1-5-21-3623811015-3361044348-30300820-1001
```

The SID becomes John's permanent security identity.

---

## Why does Windows use SID instead of usernames?

Usernames can change.

A SID never changes.

If Windows used usernames to identify users, changing a username would cause permission problems.

Using a SID ensures that permissions remain the same even after a username is changed.

### Example

A user is created.

```text
Username

john
```

Windows assigns:

```text
SID

S-1-5-21-1001
```

Later, the administrator renames the user.

```text
john

↓

john.smith
```

Although the username changed, the SID remains the same.

```text
SID

S-1-5-21-1001
```

Windows still recognizes the account as the same user.

---

### Permissions are linked to SID

Suppose John has permission to access a shared folder.

```text
Payroll Folder

↓

John

↓

Read Access
```

Windows actually stores the permission using John's SID.

```text
Payroll Folder

↓

S-1-5-21-1001

↓

Read Access
```

Even if John's username changes, the SID does not.

Therefore, John keeps the same permissions.

---

## What is an Object GUID?

An **Object GUID (Globally Unique Identifier)** is a **permanent unique identifier assigned to every object in Active Directory**.

Every object receives a GUID when it is created.

Unlike names, a GUID never changes.

Unlike a SID, a GUID is **not used for security**.

It is used to uniquely identify an object within Active Directory.

### Example

A user named John is created.

```text
User

John
```

Windows assigns a GUID.

```text
GUID

550e8400-e29b-41d4-a716-446655440000
```

This GUID permanently identifies John's object.

---

### Another Example

A computer joins the domain.

```text
Computer

PC001
```

Windows assigns another GUID.

```text
GUID

4a6b5e90-cb11-4d29-ba77-93f0d15ab321
```

Every object receives its own unique GUID.

---

## What is the difference between SID and GUID?

Both SID and GUID are unique identifiers, but they are used for different purposes.

A **SID** identifies a security object for authentication and authorization.

A **GUID** identifies the Active Directory object itself.

### Example

User:

```text
John
```

SID:

```text
S-1-5-21-1001
```

GUID:

```text
550e8400-e29b-41d4-a716-446655440000
```

Windows uses the SID when checking permissions.

Active Directory uses the GUID to uniquely identify the object internally.

---

### Differences

|SID|GUID|
|---|---|
|Security Identifier|Globally Unique Identifier|
|Used for security and permissions|Used to uniquely identify an object|
|Assigned to security objects (Users, Groups, Computers)|Assigned to every Active Directory object|
|Used during authentication and authorization|Used internally by Active Directory|
|Permissions are linked to the SID|Does not control permissions|

---

### Real-World Analogy

Think of a company employee.

```text
Employee

John Smith
```

The employee has:

```text
Employee Name

John Smith

Employee ID

1025
```

If John changes his name after marriage:

```text
John Smith

↓

John Miller
```

The employee ID remains the same.

Similarly:

- The **SID** is like an employee ID used to determine what the employee can access.
    
- The **GUID** is like a permanent record number used by the company's database to uniquely identify that employee record, regardless of changes to the employee's name or other details.

# Built-in Components

## What are Built-in Containers?

**Built-in Containers** are **special containers that Active Directory creates automatically when a domain is installed**.

They are used to store default Active Directory objects such as users, groups, and computers.

Unlike Organizational Units (OUs), built-in containers have specific purposes and are created by Windows.

Some common built-in containers are:

- Users
    
- Computers
    
- Builtin
    
- Domain Controllers
    
- ForeignSecurityPrincipals
    

### Example

```text
company.com

├── Builtin
├── Computers
├── Domain Controllers
├── Users
└── ForeignSecurityPrincipals
```

These containers exist immediately after Active Directory is installed.

---

### Users Container

The **Users** container stores:

- Default user accounts
    
- Default groups
    
- Newly created users (unless another location is specified)
    

Example:

```text
Users

├── Administrator
├── Guest
├── KRBTGT
├── John
└── Mary
```

---

### Computers Container

The **Computers** container stores newly joined computers by default.

Example:

```text
Computers

├── PC001
├── Laptop01
└── Server01
```

Many organizations move computers into Organizational Units after they join the domain.

---

### Builtin Container

The **Builtin** container stores built-in local domain groups.

Example:

```text
Builtin

├── Administrators
├── Backup Operators
├── Print Operators
└── Account Operators
```

These groups are created automatically by Windows.

---

### Domain Controllers Container

The **Domain Controllers** container stores all Domain Controllers in the domain.

Example:

```text
Domain Controllers

├── DC01
└── DC02
```

Group Policies for Domain Controllers are usually linked to this container.

---

## What are Built-in Accounts?

**Built-in Accounts** are **special user accounts that Active Directory creates automatically** during domain installation.

These accounts are required for administration and authentication.

Common built-in accounts are:

- Administrator
    
- Guest
    
- KRBTGT
    

---

## What is the Administrator account?

The **Administrator** account is the **default administrative account** in Active Directory.

It has full control over the domain.

The Administrator account can:

- Create users
    
- Delete users
    
- Reset passwords
    
- Manage computers
    
- Install software
    
- Configure security
    
- Manage Domain Controllers
    

### Example

```text
Administrator

↓

Full Control

↓

Users
Groups
Computers
Servers
```

This account is created automatically when Active Directory is installed.

---

## What is the Guest account?

The **Guest** account is a **built-in account used for temporary or limited access**.

By default, the Guest account is **disabled** for security reasons.

Guest users have very limited permissions.

### Example

```text
Guest

↓

Limited Access
```

Most organizations never enable the Guest account because it increases security risks.

---

## What is the KRBTGT account?

The **KRBTGT** account is a **special built-in account used by the Kerberos authentication protocol**.

It is created automatically when a new Active Directory domain is installed.

Users never log in with this account.

Instead, the **Key Distribution Center (KDC)** on the Domain Controller uses the KRBTGT account to generate and validate Kerberos tickets.

### Example

When John logs in:

```text
John

↓

Domain Controller

↓

KRBTGT

↓

Ticket Granting Ticket (TGT)

↓

John accesses network resources
```

The KRBTGT account helps the Domain Controller securely issue **Ticket Granting Tickets (TGTs)** for Kerberos authentication.

---

### Why is the KRBTGT account important?

Every Kerberos login depends on the KRBTGT account.

Without it:

- Users cannot receive Kerberos tickets.
    
- Domain authentication will fail.
    
- Access to domain resources becomes impossible.
    

Because of its importance, administrators should **never use this account for interactive logins** and should protect it carefully.

It is one of the most critical accounts in an Active Directory environment.