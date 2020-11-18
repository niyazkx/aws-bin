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
It helps to connect to EC2 instance through amazon network.
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
We need two subnets Public and Private.

- 🟡 Go to **Subnets** from left Navbar(VPC Dashboard)
- 🟡 Click **Create subnet**
  - `Name Tag:` Public Subnet
  - `VPC*:` Select the VPC from dropdown
  - `Ipv6 CIDR block:` Choose **No Ipv6 CIDR Block**
  - `Tenancy:` Default
 - 🟢 Finally, Click **Create** to finish, You'll see success message with your **VPC ID**.
