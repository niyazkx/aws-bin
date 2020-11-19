# ⚙️ Create New VPC with Subnets, Route Tables, Security Groups, NACL and EC2 Instance
https://www.youtube.com/watch?v=gUesnoDzNr4

## 📕 Launch VPC

- 🟡 Go to **Services**
- 🟡 Search for VPC and then VPC Dashboard
- 🟡 Go to **Your VPC** from left Navbar
- 🟡 Click **Create VPC**
  - `Name Tag:` Your VPC Name (eg. my_demo_vpc)
  - `Ipv4 CIDR  block*:` Specify your IP Range (eg. 10.0.0.0/16)
  - `Ipv6 CIDR block:` Choose **No Ipv6 CIDR Block**
  - `Tenancy:` Default
- 🟢 Finally, Click **Create** to finish, You'll see success message with your **VPC ID**.
 
 
## 📕 Internet Gateway
It helps to connect to EC2 instance through amazon public network.
- 🟡 Go to **Internet Gateway** from left Navbar(VPC Dashboard)
- 🟡 Give `Name Tag:` Your internet gateway name(eg. my_demo_igw)
- 🟢 Finally, Click **Create** to finish, You'll see success message with your **Internet Gateway ID**.

      📌 ⚠️ After finishing the above steps, you can see that your Internet Gateway's **state** is `detached`.
            Follow belows steps to attach this with the VPC:

            - 🟡 Right click on your given internet gateway name (eg. my_demo_igw)
            - 🟡 Click **Attach to VPC**
            - 🟡 Select your created VPC from dropdown.
            - 🟢 Finally, Click **Attach** and you'll see that your Internet Gateway's **state** is now `attached`.


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
  
  Attach the Internet Gateway to **Private RT**
  - Select the **Public RT**
  - Select **Routes** Tab
  - Click **Edit routes** then click **Add route**
    - `Destination`: 0.0.0.0/0 (This means you can access this from any IP)
    - `Targets`: Select your created Internet Gateway from the dropdown.
    - Finally, click **Save routes**
