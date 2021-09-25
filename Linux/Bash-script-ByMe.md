


> Written with [StackEdit](https://stackedit.io/).
> ### Step 1: Ensure/Double Check Permissions on Sensitive Files

1.  Permissions on /etc/shadow should allow only root read and write access.
    

-   Command to inspect permissions:
    
-   `ls -l shadow`
    
-   Command to set permissions (if needed):
    
-   `sudo chmod u=rw,g-rwx shadow be`
    
-  `sudo chmod u=rw,g=r,o=r group`
        

-     
  
  3.  Permissions on /etc/gshadow should allow only root read and write access.
    

-   Command to inspect permissions:
    
-     ls -l gshadow

    
-   Command to set permissions (if needed):
    
-   `sudo chmod u=rw,g-rwx gshadow`
    

5.  Permissions on /etc/group should allow root read and write access, and allow everyone else read access only.
    

-   Command to inspect permissions:
    
-   `ls -l group`
    
-   Command to set permissions (if needed):
    
-   `sudo chmod u=rw,g=r,o=r group`
    

7.  Permissions on /etc/passwd should allow root read and write access, and allow everyone else read access only.
    

-   Command to inspect permissions:
    
-   `ls -l passwd`
    
-   Command to set permissions (if needed):
    
-   `sudo chmod u=rw,g=r,0=r passwd`
    

### Step 2: Create User Accounts

1.  Add user accounts for sam, joe, amy, sara, and admin.
    

-   Command to add each user account (include all five users):
    
-   `sudo adduser sam`
    
-   `sudo adduser joe`
    
-   `sudo adduser sara`
    
-   `sudo adduser amy`
    
-   `sudo adduser admin`
    
-   OR
    
-   `sudo adduser sam joe sara amy admin`
    

3.  Ensure that only the admin has general sudo access.
    

-   `Command to add admin to the sudo group:`
    
-   `sudo usermod -aG sudo admin`
    
-   `groups admin`
    

### Step 3: Create User Group and Collaborative Folder

1.  Add an engineers group to the system.
    

-   Command to add group:
    
-   `sudo addgroup engineers`
    

3.  Add users sam, joe, amy, and sara to the managed group.
    

-   Command to add users to engineers group (include all four users):
    
-   `sudo addgroup managed`
    
-   `sudo usermod -aG managed amy`
    
-   `sudo usermod -aG managed sara`
    
-   `sudo usermod -aG managed joe`
    
-   `sudo usermod -aG managed sam`
    

5.  Create a shared folder for this group at /home/engineers.
    

-   Command to create the shared folder:
    
-   `sudo mount -t vboxsf Mshareddr`
    
-   `sudo mkdir sharefolder1 /home/engineers`
    
-   Change ownership on the new engineers' shared folder to the engineers group .
- `sudo mkdir -p /home/msharefolder`
    
-   `sudo chgrp engineers msharefolder`
    
-     
    

  

### Step 4: Lynis Auditing

1.  Command to install Lynis: `Sudo apt install lynis`
    
2.  Command to see documentation and instructions: `sudo lynis -c`
    
3.  Command to run an audit: `sudo lynis audit system`
    
4.  Provide a report from the Lynis output on what can be done to harden the system.![](https://lh3.googleusercontent.com/KuX7PhNVzZjjbh0hUNRPN9QtVeD4382woKkIhnBzl74BfkRlKFi9quKKJG-mUy1586Uv715s0AcKdOECNojuksZnI5CM4c4xKID_bGU_-J27twkABU_p4VTxedxTH-lxYeL2FfMP=s0)
    

  

### Bonus

1.  Command to install chkrootkit: `sudo apt install chkrootkit`
    
2.  Command to see documentation and instructions: `sudo chkrootkit`
    
3.  Command to run expert mode: `sudo chkrootkit -x`
    

> 
