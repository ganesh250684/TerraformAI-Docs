# ⚠️ Terraform Plan Basic Report

**Generated:** 2025-12-07 00:42:19  
**Status:** ⚠️ AI Analysis Not Available - Basic Report Generated

---

## 📊 Plan Summary

This Terraform plan proposes **6 infrastructure changes**:

- **4 resources to add** ✅
- **2 resources to change** 🔄
- **0 resources to destroy** ❌

---

## 📝 Changes Breakdown

### ✅ Resources to Add (4)

1. `aws_internet_gateway.igw`
2. `aws_nat_gateway.nat`
3. `aws_secretsmanager_secret.db_password`
4. `aws_secretsmanager_secret_version.db_password`

### 🔄 Resources to Change (2)

1. `aws_launch_template.app_lt`
2. `aws_autoscaling_group.app_asg`

### ❌ Resources to Destroy (0)

*No resources to destroy*

---

## 🔍 Raw Terraform Plan Output

```terraform
Terraform v1.9.0
on linux_amd64

Initializing provider plugins...
- Finding hashicorp/aws versions matching "~> 5.0"...
- Installing hashicorp/aws v5.55.0...
- Installed hashicorp/aws v5.55.0

Terraform has been successfully initialized!

module.network.aws_vpc.main: Refreshing state...
module.network.aws_subnet.public[0]: Refreshing state...
module.network.aws_subnet.private[0]: Refreshing state...
module.app.aws_autoscaling_group.app_asg: Refreshing state...
module.data.aws_rds_cluster.app: Refreshing state...

------------------------------------------------------------------------

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create
  ~ update in-place
  - destroy
  +/- create replacement and then destroy

Terraform will perform the following actions:

  # module.network.aws_internet_gateway.igw will be created
  + resource "aws_internet_gateway" "igw" {
      + vpc_id = module.network.aws_vpc.main.id

      + tags = {
          "Name" = "main-igw"
        }
    }

  # module.network.aws_nat_gateway.nat[0] will be created
  + resource "aws_nat_gateway" "nat" {
      + allocation_id = aws_eip.nat[0].id
      + subnet_id     = module.network.aws_subnet.public[0].id

      + tags = {
          "Name" = "nat-gw-1"
        }
    }

  # module.app.aws_launch_template.app_lt will be updated in-place
  ~ resource "aws_launch_template" "app_lt" {
        name_prefix   = "app-lt-"
      ~ image_id      = "ami-01abcdef123456789" -> "ami-0fedcba9876543210"
      ~ instance_type = "t3.small" -> "t3.medium"
      ~ user_data     = (sensitive value)

      ~ tag_specifications {
          ~ tags = {
              "Name"        = "app-server"
              "Environment" = "staging"
            } -> {
              "Name"        = "app-server"
              "Environment" = "prod"
            }
        }
    }

  # module.app.aws_autoscaling_group.app_asg will be updated in-place
  ~ resource "aws_autoscaling_group" "app_asg" {
        name                      = "app-asg"
      ~ desired_capacity          = 2 -> 4
      ~ min_size                  = 1 -> 2
      ~ max_size                  = 4 -> 8
      ~ health_check_grace_period = 300 -> 120

      ~ tag {
          ~ key                 = "Environment"
          ~ value               = "staging" -> "prod"
            propagate_at_launch = true
        }
    }

  # module.data.aws_rds_cluster.app must be replaced
 +/- resource "aws_rds_cluster" "app" {
        cluster_identifier = "app-cluster"
      ~ engine_version     = "14.7" -> "15.4" # forces replacement
      ~ storage_encrypted  = false -> true
      ~ backup_retention_period = 3 -> 7
      + copy_tags_to_snapshot    = true
    }

  # module.data.aws_rds_cluster_instance.app[0] will be replaced
 +/- resource "aws_rds_cluster_instance" "app" {
        identifier         = "app-cluster-1"
      ~ instance_class     = "db.r6g.large" -> "db.r6g.xlarge" # forces replacement
      ~ publicly_accessible = true -> false
    }

  # module.data.aws_secretsmanager_secret.db_password will be created
  + resource "aws_secretsmanager_secret" "db_password" {
      + name = "app/db-password"
    }

  # module.data.aws_secretsmanager_secret_version.db_password will be created
  + resource "aws_secretsmanager_secret_version" "db_password" {
      + secret_id     = aws_secretsmanager_secret.db_password.id
      + secret_string = (sensitive value)
    }

Plan: 4 to add, 2 to change, 0 to destroy, 2 to replace.

─────────────────────────────────────────────────────────────────────────────

```

---

## 💡 Recommendations

Since this is a basic report without AI analysis:

1. Review the raw plan output carefully
2. Try generating an AI-powered report again later
3. Manually review each resource change for security and data-loss risks