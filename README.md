Landing Page Deployment on EC2

## **Overview**  
This repository documents my journey of deploying a simple HTML landing page to an AWS EC2 instance. It’s a practical demonstration of provisioning a server, configuring it to serve a webpage, and overcoming challenges along the way.  

👉 **Check out the live site here**: [http://3.89.126.104](http://3.89.126.104)  

---

## **Steps to Launch the Landing Page**  

### 1. **Provisioning the EC2 Instance**  
I started by creating an Amazon EC2 instance using the following steps:  
- Selected an Ubuntu Server 22.04 AMI.  
- Chose a t2.micro instance type (free tier eligible).  
- Configured a security group to allow HTTP (port 80) and SSH (port 22) access.  
- Used the default user data script to install Apache and serve a basic HTML page.  

### 2. **User Data Script**  
The initial user data script installed Apache and deployed a simple “Hello World” HTML page:  
```bash
#!/bin/bash
sudo apt update -y
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
echo "<h1>Hello World</h1>" | sudo tee /var/www/html/index.html
```

After confirming the setup worked, I replaced the "Hello World" page with a custom HTML landing page containing details about myself and the project.  

### 3. **Creating the Landing Page**  
I crafted a custom `index.html` file using HTML and CSS. The page introduces my technical skills, interests, and a bit about my personal journey.  

### 4. **Deploying the Landing Page**  
To replace the "Hello World" page:  
- I used the EC2 instance’s **Instance Connect** to access the server.  
- Edited the `index.html` file at `/var/www/html/` using `nano`.  
- Pasted the custom landing page code and saved the file.  
- Restarted Apache to apply the changes:  
  ```bash
  sudo systemctl restart apache2
  ```

### 5. **Testing the Website**  
I opened my browser and navigated to (http://3.89.126.104) to verify the deployment.

---

## **Challenges and How I Solved Them**  

### **1. The “Refused to Connect” Error**  
At one point, the browser refused to connect to the instance. After troubleshooting, I realized Apache wasn’t installed. Running `sudo systemctl status apache2` helped me confirm this. The solution was to install Apache manually.  

### **2. Overwriting the Landing Page**  
Initially, the user data script included the server setup commands and the HTML page content. Unfortunately, this caused the page to display unwanted script text. To fix this:  
- I separated the HTML content and manually deployed it to `/var/www/html/index.html`.  

### **3. Debugging User Data**  
When updating the user data, I learned that it only runs on the instance’s first boot. I had to restart the instance or manually apply changes for further updates.  

---

## **Lessons Learned**  
- **User Data Behavior**: It’s executed only during the first instance launch, so planning the script carefully is crucial.  
- **Importance of Testing**: Debugging with tools like `systemctl` and ensuring proper permissions saved me from hours of frustration.  
- **Patience and Perseverance**: Not everything works on the first try, and that’s okay!  

---

## **About the Landing Page**  
This project highlights my interest in cloud technology and web development. It’s part of my journey to becoming a skilled DevOps engineer.  

---

### **Live Demo**  
Visit the live site here: [http://3.89.126.104](http://3.89.126.104)  
