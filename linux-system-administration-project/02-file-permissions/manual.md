# Phase 2 - File Permissions and Access Control

## 1. objective

configure a simulated application directory with role-based Linux permission 
The objective is to:

- Create the application directory structure.
- Configure appropriate ownership.
- Configure Linux file and directory permissions.
- Provide developers with required appllication access.
- Provide operations with required operational access.
- Prevent normal users from modifying sensitive configuration.
- Use ACLS where additional access control is required.
- Verify the final permission model usinng different users.
- Document the final manual coniguration for later Ansible automation

2. Environmetn

Item                    Details
operating system        NAME="Red Hat Enterprise Linux" VERSION="10.0 (Coughlan)"
Hostname                node1
Ip Address              192.168.0.19
Administrative user     root
Application Directory   '/opt/company-app'

### Command Used
'''  bash
whoami
hostname
hostname -I
cat /etc/os-release

3. Users and Groups

Users

user        Role        purpose

alice       Developer   software-engineer
developer1  Developer   software-engineer
operator1   Operations  operator 
operator2   Operations  operator
sam         Normal User normal user
bob         Normal User normal user

Groups

Group           Purpose             Members

developers   Deverloper access      alice,developer1
operations   Operations access      operator1,operator2

User Verification

id alice
groups developers
getent passwd alice

Group Verification

getent group developers
getent group operations

4. Applicaton Directory Structure

/opt/company-app
|-- app/
|-- config/
|-- logs/
|-- shared/

Directory Purpose

Directory       Purpose
app/            Application files
config/         Apllication configuration
logs/           Application logs
shared/         Shared application resources

mkdir -p /opt/company-app/app
mkdir -p /opt/company-app/config
mkdir -p /opt/company-app/logs
mkdir -p /opt/company-app/shared

Verification

ls -l /opt/company-app
find /opt/company-app -maxdepth 2 -type d

5. Ownership Configuration

Document the owner and group assigned to each resource

Resource                    Owner                   Group
/opt/company-app/app        root                    developers
/opt/company-app/config     root                    operations
/opt/company-app/logs       root                    operations
/opt/company-app/shared     root                    developers


Command Used

chown <user>:<group> <path>

Ownership Verification

ls -ld /opt/company-app
ls -ld /opt/company-app/*

6. Permission Configuration

Document the final permissions assigned to each resource.

Resource        Owner       Group       Other       Octal

app/            rwx         r-x         ---         750
config/         rwx         r-x         ---         750
logs/           rwx         r-x         ---         750
shared/         rwx         rwx         ---         770
development/    rwx         rwx         ---         770


Command Used

chmod <permissions> <path>

Permission Verification

ls -ld /opt/company-app/*


7. Developer Acsess

Developers must have the required access to application resources

Required Access
1) Read application files.
2) Modify appropriate application files.
3) Work inside the application directory.
4) Access shared resources where required.

Restrictions
1) No unnecessary access to sensitve configuration.
2) No unnecessary administrative privileges.

Testing 
su - alice

whoami
id
groups

Test application access
cd /opt/company-app/app
ls
cat <file>

Test permitted modificaton
echo "developer test" >> <file>

8. Operations Access
Operations users must have the access requried to manage the application.

Required Access
1) Read application logs.
2) Access application files where required.
3) Manage application resources where required.
4) Access shared resources where requried

Testing 

su - operator1

whoami
id
groups

Test log access

ls /opt/company-app/logs
cat <log-file>

Test application access:

ls /opt/company-app/app

9. Normal User Access
Normal users must not be able to modify sensitive application configuration.

Testing

su - bob

Verify

whoami
id
groups

10. ACL Configuration

ACLs were configured where standard Linux owner/group/other permissions

Commands Used

setfacl -m u:operator1:r-x /opt/company-app

ACL Verificaton

getfacl /opt/company-app


       
