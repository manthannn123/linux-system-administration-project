User Managemen -- Manual configuration

1.  Objective 

The objectiv of this task was to manually configure linux user and group management

The following activities were performed

1) Create linux users
2) Create linux group
3) Assign users to group
4) Configure user privileges
5) Configure user privileges
6) Configure files and directory ownership
7) Configure files and directory  permissions
8) Verify user and group configuration
9) Verify access control

2) Environment

Item                                    Details

Operating System                       OS= Red Hat Enterprice  Version = 10.0
Server Type                             VM (Virtual Machine)
Hostname                                controller
IP Address                              192.168.0.19
Administrative user                     root

Verify Environment

The following commands were used to verify the server environment

cat /etc/os-release
hostname
hostname -I
whoami

3) User Created

The following user were created as part of the project

username    purpose     primary group       shell       home directory

alice       developer   alice               /bin/bash   /home/alice
developer1  developer   developer1          /bin/bash   /home/developer


Usere Creation

users were created manually using Linux useradd command

Example
useradd -m -s /bin/bash alice

Passwd were configured separately using
passwd alice

User verification

Each user was verified using

id alice
getent passwd alice

The verification confirmed

1) UID
2)primary GID
3) Summpplemtary groups
4) Home directory
5) Login Shell

4) Groups Created 

The following group were created

Group           purpose         member
developers      developer       alice,developers

Group Creation

Group were created using

Users were added to supplemtary group using 

usermod -aG developers alice
usermod -aG developers developer1

Group Verification

Groups were verified using:

getent group developers
groups alices
id alices

5) Permissions and Privileges Assigned

Group Membership

Users were assigned to groups according to the access requirement of the project
Group memebership was verified using
id alice

The output was checked to confirm that the expected supplementary groups were present

File and Directory permissions

A project directoy was created for testing linux ownership and permission

Example
mkdir /Project

chown alice:alice /Project

Permission were configured using
chmod 750 /Project

The resulting ownership and permissions were verfied using

ls -ld /Project

The objective was to ensure that

1) The correct user owned the resource
2) The correct group owned the resource
3) Authorized user had the required access
4) Unauthorized users were denied access where required

Administrative Privileges
Administrative privileges were assigned only where requried by the project

The privileges assigned to a user were verified using

sudo -l -U alice

6) Verification
The configuration was verifed after completing the user and group setup

Verify Users

id alice
getent passwd alice

Result
The user existed with the expected UID,GID,home directoy,and login shell

Verify Group
getent group alice
id alice

Result
The expected users were members of the required groups

Verfy file owership
ls -ld /Project

Result 
The directory had the expected owner and group

Verify file Permissions
ls -ld /Project

The permission bits were checked to confirm that the configured access matched the prokect requirements

Access Testing
Access was tested using the configured users

Authorized User

The authorized user was able to perform the expected operation

Unauthorized User

The unauthorized user was denied access to the restricted resource

Result
The configured ownership and permission model behaved as expected  

7) What I Learned

Through this task, i learned

1) How linux users are created and managed
2) How linux groups are created and managed
3) The difference between primary and supplementary groups
4) How UID and GID identify users and groups
5) How file ownership affects access
6) How linux permission bits control access
7) How chmod and chown are used to manage permissions and ownership
8) How to verify users and group using id and getent
9) The importance of verifying configuratin after making changes

8) Final Result
The linux user and group management requirement were configured manually

users and groups were created group memberships and privileges were assigned file ownership and permissions were configured and the resulting congiguration was verifed

This manual implementation will later be reproduced using Ansible to demostarte configuration automation and idempotency
