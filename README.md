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


