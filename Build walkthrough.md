
## Build Walkthrough


# 1. Project Structure
The project was organised into separate Terraform configuration files to keep the infrastructure configuration easy to understand and maintain.

wordpress-terraform/
├── main.tf
├── variables.tf
├── outputs.tf
├── userdata.sh

    •    main.tf – Defines the AWS infrastructure and EC2 instance.

    •    variables.tf – Defines variables used by the Terraform configuration.

    •    outputs.tf – Displays useful information after deployment.

    •    userdata.sh – Installs and configures the software required for WordPress.








# 2. Defining Variables
Variables were created so that values such as the , AMI ID and EC2 instance type could be changed without modifying the main infrastructure configuration.
This makes the Terraform configuration more reusable and avoids hard-coding configuration values directly into the resources.


<img width="489" height="414" alt="tf main part 1 screenshot" src="https://github.com/user-attachments/assets/ffa9e558-1bc6-4125-abad-60b621646b23" />





# 3. Creating the EC2 Instance
The EC2 instance was created using the AWS provider and an Ubuntu AMI.
The instance was configured with the required instance type and attached to the WordPress security group.





# 4. Configuring the Security Group
A security group was created to control traffic to and from the WordPress server.
Inbound traffic was configured to allow:
    •    HTTP on port 80 so users can access the WordPress website.
    •    SSH on port 22 so the instance can be accessed for administration and troubleshooting.
Outbound traffic was also allowed so that the EC2 instance could access the internet.
This was particularly important because the WordPress installation script needs internet access to update packages and download WordPress.


<img width="489" height="414" alt="tf main part 1 screenshot" src="https://github.com/user-attachments/assets/f6f053f8-6ec2-4dc1-9b00-7c76d74c4459" />
<img width="479" height="600" alt="tf main part 2 screenshot" src="https://github.com/user-attachments/assets/de322753-1a2d-4e71-bd3a-16600beacb38" />



# 6. WordPress Installation with User Data
A userdata.sh script was used to automatically configure the EC2 instance when it was launched.
The script:
    1.    Updates the Ubuntu package lists.
    2.    Installs Apache, PHP, MariaDB and required utilities.
    3.    Starts and enables Apache.
    4.    Downloads the latest WordPress package.
    5.    Extracts WordPress into /var/www/html.
    6.    Removes the default Apache web files.
    7.    Sets the correct ownership for the WordPress files.
    8.    Restarts Apache.
The script allows the EC2 instance to configure itself automatically after Terraform creates it.

<img width="651" height="440" alt="tf userdata screenshot" src="https://github.com/user-attachments/assets/22534250-a816-40e2-a611-ee346a3d5f41" />


# 7. Terraform Deployment
After creating the configuration, Terraform was initialised:
terraform init
The configuration was then checked with:
terraform plan
This allowed the resources Terraform intended to create or modify to be reviewed before deployment.
The infrastructure was then deployed with:
terraform apply
Terraform created the required AWS resources and displayed the configured outputs after the deployment completed.



# 8. Verifying the Deployment
After the EC2 instance was created, the instance’s public IP address was used to access the server.
The WordPress configuration page was successfully reached through the browser.
This confirmed that:
    •    The EC2 instance was running.
    •    Apache was successfully installed.
    •    PHP was available.
    •    WordPress had been downloaded.
    •    Port 80 was accessible.
    •    The EC2 instance had working outbound internet connectivity.


<img width="471" height="214" alt="tf outputs code screenshot" src="https://github.com/user-attachments/assets/bf0b49a6-ee10-40d6-a7f6-f9085a2231fd" />




# 10. Verification Result

The final result was a working WordPress installation deployed using Terraform.
The deployment demonstrated how Terraform can be used to provision an EC2 instance, configure networking and security, generate SSH access, and automatically install software using EC2 user data.

<img width="409" height="63" alt="tf output screenshot" src="https://github.com/user-attachments/assets/29774f12-415b-43b0-89ea-ad5e9cdae8c3" />

<img width="1263" height="678" alt="tf wordpress screenshot" src="https://github.com/user-attachments/assets/0b565ad4-69e9-4aa5-90e4-51e3ce1beb46" />




