# ⚙️ Create New VPC with Subnets, Route Tables, Security Groups, NACL and EC2 Instance

- Link: https://www.youtube.com/watch?v=gUesnoDzNr4
- Link: https://www.youtube.com/watch?v=b1b6JTYnbjU

## 📕 Launch VPC

- 🟡 Go to **Services**
- 🟡 Search for VPC and then VPC Dashboard
- 🟡 Go to **Your VPC** from left Navbar or You can Click **Launch Wizard** where you can find guided instructions step by step to create VPC.
- 🟡 Click **Create VPC**
  - `Name Tag:` Your VPC Name (eg. my_demo_vpc)
  - `Ipv4 CIDR  block*:` Specify your IP Range (eg. 10.0.0.0/16)
  - `Ipv6 CIDR block:` Choose **No Ipv6 CIDR Block**
  - `Tenancy:` Default
- 🟢 Finally, Click **Create** to finish, You'll see success message with your **VPC ID**.



## 📕 Subnets
We need two subnets Public and Private. Public Subnet for the resources which are accessible from the internet and Private Subnet for which are not.

- 🟡 Go to **Subnets** from left Navbar(VPC Dashboard)
- 🟡 Click **Create subnet**

  - For Public Subnet:
    - `Name Tag:` Public Subnet
    - `VPC*:` Select the VPC from dropdown
    - `Availability Zone:` Choose your preferred zone or choose **No Preference**
    - `Ipv4 CIDR Block*:` Give your public subnet range(eg. 10.0.1.0/24)
 
  - For Private Subnet:
    - `Name Tag:` Private Subnet
    - `VPC*:` Select the VPC from dropdown
    - `Availability Zone:` Choose your preferred zone or choose **No Preference**
    - `Ipv4 CIDR Block*:` Give your public subnet range(eg. 10.0.2.0/24)
- 🟢 Finally, Click **Create** to finish, You'll see success message with your **Subnet ID**.
 


 
## 📕 Internet Gateway
It helps to connect to EC2 instance through amazon public network.
- 🟡 Go to **Internet Gateway** from left Navbar(VPC Dashboard)
- 🟡 Click **Create internet gateway**
- 🟡 Give `Name Tag:` Your internet gateway name(eg. my_demo_igw)
- 🟢 Finally, Click **Create** to finish, You'll see success message with your **Internet Gateway ID**.

      📌 ⚠️ After finishing the above steps, you can see that your Internet Gateway's **state** is `detached`.
            Follow belows steps to attach this with the VPC:

            - 🟡 Right click on your given internet gateway name (eg. my_demo_igw)
            - 🟡 Click **Attach to VPC**
            - 🟡 Select your created VPC from dropdown.
            - 🟢 Finally, Click **Attach** and you'll see that your Internet Gateway's **state** is now `attached`.

 
 
## 📕 Route Tables
By default, AWS will create a Route Table at the time of creating a VPC.
  
- 🟡 Simply rename the default one to **Public RT** by clicking the 🖋 (Pen Icon) under Name Column.
- 🟡 Then create another one for private route table.
  - `Name Tag`: **Private RT**
  - `VPC*`: Choose your created VPC
- 🟢 Finally, Click **Create** to finish.
   
Now, there will be two Route tables:
- Public RT
- Private RT
  
  ### Public RT
    Attach the Internet Gateway to **Public RT**
    - 🟡 Select the **Public RT**
    - 🟡 Select **Routes** Tab
    - 🟡 Click **Edit routes** then click **Add route**
      - `Destination`: 0.0.0.0/0 (This means you can access this from any IP)
      - `Targets`: Select your created Internet Gateway from the dropdown.
      - 🟢 Finally, click **Save routes**

    Attach the Public Subnet to **Public RT**
    - 🟡 Select  **Public RT**
    - 🟡 Select **Subnet Associations** and click **Edit Subnet Associations**
    - 🟡 You'll see two subnets that you created earilier. Select the Public Subnet.
    - 🟢 Click **Save**
    
   ### Private RT
    We dont need any Internet Gateway here as it is a private route table, just attach the Private Subnet to **Private RT**
    - 🟡 Select  **Private RT**
    - 🟡 Select **Subnet Associations** and click **Edit Subnet Associations**
    - 🟡 You'll see two subnets that you created earilier. Select the Private Subnet.
    - 🟢 Click **Save**
    

## 📕 EC2 Instance
Now create two EC2 Instances, One for Public and another one for Private.

- 🟡 Go to **Services**
- 🟡 Select **EC2** under Compute section.
- 🟡 Click **Instances** from left Navbar (EC2 Dashboard)
- 🟡 Click **Launch Instances** then choose your preferred Instance and continue the next steps...
- 🟡 On the **Configure Instance Details** page:
  - `Number of instances`: 
  - `Purchasing Option`:
  - `Network`: Your Created VPC
  - `Subnet`: Public Subnet
  - `Auto-assign Public IP`: Enable
- 🟡 On the **Configure Security Group** page:
  - `Assign a security group`: Select the existing one that you've created already
- 🟡 Review and launch
- 🟡 Create and download the key pair(.pem file) to access the instance in future.
- 🟢 Finally, Launch Instances.

📌 You'll see that Instance is initializing, in the meantime give your instance a name (eg. ec2-public)
Following the same procedure create another instance for private. Make sure that you choose your **Private Subnet** and **Security Group**. Choose the same key pair that you've created for public instance. 


    
## 📕 Security Groups
By default, AWS will create a Security Group at the time of creating a VPC. Just Rename it (eg. my_demo_sg)

Now set Inbound Rules:
  - 🟡 Select **Inbound Rules** Tab
  - 🟡 Click **Edit rules**
  - 🟡 Click **Add Rule**
    - `Type`: Select **All Traffic** from dropdown (You may choose SSH or others)
    - `Protocol`: **All**
    - `Port Range`: **All**
    - `Source`: **My IP** (Only you can access the instances from this IP. Copy the IP for using in in NACL)
    - `Description`: Give an identical name.
  - 🟢 Click **Save Rules**
 
 
 
## 📕 Network ACLs (NACL)
By default, AWS will create a NACL at the time of creating a VPC. Just Rename it (eg. my_demo_nacl)

Select **Inbound Rules**

By default there allowing all traffic (0.0.0.0/0) which is not safe. So change it.
  - 🟡 Click **Edit inbound rules**
    - `Source`: Paste the **copied IP** from Security Group.
  - 🟢 Click **Save**
  

