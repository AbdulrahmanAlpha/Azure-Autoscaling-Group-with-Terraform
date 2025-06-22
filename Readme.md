# ⚙️ Azure Autoscaling Group with Load Balancer using Terraform

This project sets up an **Azure Virtual Machine Scale Set (VMSS)** with autoscaling, a load balancer, network configurations, and security rules — all provisioned using **Terraform**.

## 📌 Project Features

- ✅ Provision Azure Resource Group, Virtual Network, and Subnet  
- ✅ Create Public IP and Load Balancer with backend pool and NAT rule  
- ✅ Define Network Security Group with HTTP & SSH access  
- ✅ Deploy VM Scale Set (VMSS) with Ubuntu Server  
- ✅ Set up Autoscaling based on CPU utilization  
- ✅ Use Infrastructure as Code for easy deployment and version control  

---

## 🧱 Architecture

```

+------------------------+
\|  Load Balancer (LB)   |
\|  + NAT Rule + Probe   |
+----------+------------+
|
+-------v--------+
\| VM Scale Set   | <--- Ubuntu VMs (autoscaled)
+----------------+
\|     VNet/Subnet
+----------------+
\| Resource Group |
+----------------+

```

---

## 📁 Folder Structure

```

.
├── main.tf        # Main Terraform configuration
├── variables.tf   # (Optional) Define input variables
├── outputs.tf     # (Optional) Define outputs for use in CI/CD
├── README.md      # You're here
```
---

## 🔧 How to Use

### 1. 🔐 Prerequisites

- [Terraform](https://www.terraform.io/downloads.html) installed
- Azure subscription & Service Principal (for authentication)
- Permissions to create and manage resources on Azure

### 2. 🧾 Update Credentials

Replace the placeholders in `main.tf` with your Azure credentials:

```hcl
provider "azurerm" {
  subscription_id = "<subscription_id>"
  client_id       = "<client_id>"
  client_secret   = "<client_secret>"
  tenant_id       = "<tenant_id>"
}
```

### 3. 📦 Initialize & Apply Terraform

```bash
terraform init
terraform plan
terraform apply
```

> ☑️ Confirm the plan and wait for Terraform to complete provisioning.

---

## 📊 Autoscaling Behavior

* 📈 **Scale Out**: When CPU usage > 70% for 5 minutes → Add 1 instance
* 📉 **Scale In**: When CPU usage < threshold → Remove 20% of instances
* Minimum 2 and Maximum 5 instances in the VMSS

---

## 🧪 Testing Your Deployment

1. Visit the public IP shown in `terraform output`.
2. SSH into a VM if needed using port 22.
3. Monitor load balancer distribution & scale set instance count via Azure Portal.

---

## 📌 Notes

* Default OS: **Ubuntu Server 16.04 LTS**
* Default admin user: `adminuser`
* Password must be set in `admin_password` field
* Load balancer listens on port 80 and routes to instances

---

## 🧼 To Destroy

```bash
terraform destroy
```

---

## 📚 Resources

* [Terraform Azure Provider Docs](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
* [Azure Virtual Machine Scale Sets](https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/)
* [Terraform Best Practices](https://developer.hashicorp.com/terraform/tutorials)

---

## 🙋 About the Author

Made with 💻 by **Abdulrahman A. Muhamad**
🔗 [GitHub](https://github.com/AbdulrahmanAlpha) | [LinkedIn](https://www.linkedin.com/in/abdulrahmanalpha)

---

> 🚀 Feel free to fork this project and customize it for your infrastructure needs!
