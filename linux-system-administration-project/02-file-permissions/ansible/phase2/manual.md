# Phase 2 - File permissions, Ownership & ACLs

## 1. Objective

The objective of this phase is to understand and implement Linux file and directory Permission, Group Ownership, and Access Control List (ACLs)

A simulated application directory was created at :

/opt/company-app

The directory represents a basic application environment containing

- Application files
- Configuration files
- Logs
- Shared files

The permissions were designed according to different user responsibilites

The environment contains two groups:

- operators
- developers

Users:
- sam -> operators
- andrew -> operators
- colen -> developers
- druv -> deelopers

The objective is to ensure that  users receive only the access required for their role.

# 2. Lab Environment

## server

Managed Liux server:
- node2

## Ansible Controller
- ansible controller VM

## Application Directory

/opt/company-app

## Groups 

operators
developers

## Users

sam
andrew
colen
druv

## 3. Permission Requirements

The application directory was designed with the following requirements.

## Developers

Developers should be able to :

- Read application files
- Work inside the development / application dorectory
- Read required configuration information
- Read logs where required

Developer should not be able to:

- Modify sensitive production configuration
- Modify protected application configuration

## Operators

Operators should be able to :

- Manage application files where requied
- Read application logs
- Access configuration files
- Manage operational resource

## Normal/unauthorized users

Users who are not members of the required groups should not be albe to modify sensitive application resources.

# 4 . Linux Permission model

Linux permission are divided into three basic categories:

- User/Owner
- Group 
- Other 

Each category can have

- r -> read
- w -> write
- x -> execute

For example:
owner - > rwx
Group -> r-x
others -> ---

Therfore:
750

Provides:

- owner: full access
- Group: read and execute
- Others: no access

# 5. Directory structure

The following application structure was created:

/opt/company-app
|-- app/
    |-- application.conf
|-- config/
    |-- application.conf
|-- logs/
    |-- application.log
|-- shared/

The purpose of each directory is:
## app/

contains application-related files.

## config/
Configuration may contain sensitive applications or production setting so access is restricted

## logs/
Contains application logs.

Operators require access to logs for monitoring and troubleshooting

## shared/
Used for files that need to be shared between authorized users.

# 6. Users and Groups
The following groups were created:

operators
developers

The user were assigned as following

User            Group         Role

sam             operators     Operations
andrew          operators     Operations
colen           developers    Developer
druv            developers    Developer

User and group membership was verified using

id sam
id andrew
id colen
id druv

# 7. Directory Ownership and Permissions

The application root directory was configured with restriction access.

Example:

/opt/company-app

owner: root
Group: developers
permissions: 750

Reason:  The root directory should not be writaable by every user.

Ther owner receives full control 

The authorized group can enter and read the directory

Other users receive no access

# 8. Application Directory

Path : /opt/company-app/app

owner: root
Group: developers
permissions: 770
Reason: Developers need gto work with applilcation files

The owner and devleopers group therefore receive:

- Read
- Write
- Execute

Others received no access.

The execute permission on a directory allows user to enter / traverse the directory and  access files for which they have appropriate permission



