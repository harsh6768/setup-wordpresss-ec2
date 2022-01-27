# SETUP WORDPRESS IN AWS EC2 INSTANCE


## STEP 1. SETUP EC2 INSTANCE

Follow the readme file for below mentioned git repository 

https://github.com/harsh6768/deploy-in-ec2

## STEP 2. INSTALL LAMP(LINUX , APACHE , MYSQL/MARIA_DB ,PHP) in Ec2 instace

   
   ### Step A. Install Apache
   
        sudo apt install apache2 -y 
        
        or 
        
        sudo apt-get install apache2 -y 
  
  
<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%204.49.38%20PM.png"/>


  #### You can copy the PUBLIC_IP of EC2 Instance  and make sure you open the HTTP port 80 in In-Bound Security Group.
        
<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%206.07.25%20PM.png"/>  

  
  Optional Commands to start,restart,stop and check the status of Apache2
  
     sudo systemctl start apache2

     sudo systemctl restart apache2

     sudo systemctl stop apache2

     sudo systemctl status apache2
  
  Run bellow command required/optional 
  
    sudo systemctl enable apache2
      
 
 ##### It will keep apache service running even if you reboot the EC2 instance machine
  
  
       
  ### Step B. Install MySQL database.
  
  
    sudo apt install mysql-server

    or 

    sudo apt-get install mysql-server
        
     
 <img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%205.26.16%20PM.png"/>
          
          
          
  ### MYSQL SECURE INSTALLATION
        
         sudo mysql_secure_installation
              
 
 <img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%206.36.13%20PM.png"/>
 
   
   Restart mysql database
   
       sudo systemctl  restart mysql
       
       
   ### Step C. Install PHP and dependency Install
   
      sudo apt install php php-mysql php-gd php-cli php-common
       
       
<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%206.51.46%20PM.png"/>


## STEP 3 : Install Wordpress and connect with Database

Go to wordpress website to download 

https://wordpress.org/download/


<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%2010.29.22%20PM.png"/>


Double click or right click on download button to get the option and copy the copy link address


Run below command to download wget and unzip to donwload wordpress and unzip it.

       sudo apt install wget unzip -y
       
       sudo wget https://wordpress.org/latest.zip
       
       sudo unzip latest.zip
       
       
<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%2010.57.17%20PM.png"/>

### Copy content of wordpress into the apache server /var/www/html file 

       sudo cp -r wordpress/* /var/www/html/
       
       -r  : for recursive copy
       
### Modify the ownership of all the file inside /var/www/html/ to user www-data:www-data 

       sudo chown www-data:www-data -R  /var/www/html/ 
    
       -R : for recursive 

<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%2011.15.11%20PM.png"/>


You have copied all the data of wordpress It you see the apache server's default page.

<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%206.07.25%20PM.png"/>  

### You need to delete index.html  so that you can see the wordpress 

      sudo rm -rf index.html 
    
Now you go to the web browser using your EC2 public ip address ,you will be able to see the wordpress setup starting page

<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%2011.30.13%20PM.png"/>
    

### We need to create database and new user for wordpress specific 

<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-22%20at%2012.08.47%20AM.png"/>


### Create new user in mysql database to handle wordpress stuff .
   
   A. Login to mysql 
   
      mysql -u root -p 
  
  B. create new database 
  
      create database wordpress;
      

<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%2011.56.57%20PM.png"/>
      
  C. You can see the Password policy in mysql ,
  
     this option  you select while mysql_secure_installation part , as I have selected the medium policy , I can not enter the normal password  
     
         SHOW VARIABLES LIKE 'validate_password%';
     
     Follow below stack overflow link to modify the password policy 
     
     https://stackoverflow.com/questions/43094726/your-password-does-not-satisfy-the-current-policy-requirements
     
  D. create new user to handle wordpress database.
  
       create user "wpadmin"@"%" identified by "786Hh@786";      //password policy was medium to I need to enter the mixed password
     
  E. Grant the permission to the created user 
  
       grant all privileges on wordpress.* to "wpadmin"@"%";
      
 <img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-21%20at%2011.57.03%20PM.png"/>
 
 
 ### Now just fill the database and user creds and enter submit button 
 
 <img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-22%20at%2012.12.05%20AM.png"/>
 
 ### Click on Run Installation button to setup Wordpress.
 
 <img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-22%20at%2012.12.33%20AM.png"/>
 
 
 
 <img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-22%20at%2012.30.18%20AM.png"/>
 
 <img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-22%20at%2012.30.46%20AM.png"/>
 
 <img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-22%20at%2012.30.58%20AM.png"/>
 
 <img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-22%20at%2012.31.13%20AM.png"/>
 


## If You have stopped the ec2 for any reason and again start the Instance then you won't see the styling and other functionality to you as IP has been changed now. To fix this issue we need to add the new ip to the mysql database.

   ### Step 1 . login to mysql database .
              
               sudo mysql 
               
               or 
               
               sudo mysql -u root -p
               
  ### Step 2.  check databases
  
              show databases;
              
 ### Step 3.  Select database ;
 
             use wordpress;      //this is the datbase that we have crated earlier
 
 ### Step 4. Show all the tables in databases;
 
            show tables;
            
            
   <img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-24%20at%208.09.28%20PM.png"/>
   
   
### Step 5. Update the ip in wp_options tables;

     
           update wp_options set option_value="http://PUBLIC_IP" where option_id=1;
           
           update wp_options set option_value="http://PUBLIC_IP" where option_id=2;
           
     
<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-24%20at%208.07.26%20PM.png"/>
 
 
### Now workpress website will look the as the earlier ,visit the PUBLIC_IP of ec2 instance 


<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-24%20at%208.27.35%20PM.png"/>


##  AWS ROUTE 53  to connect ip with domain

  
<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-24%20at%208.30.19%20PM.png"/>

<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-24%20at%208.30.29%20PM.png"/>

<img src="https://github.com/harsh6768/setup-wordpresss-ec2/blob/main/Screenshots/Screenshot%202022-01-24%20at%208.31.14%20PM.png"/>




