# ⚠️ Terraform Plan Basic Report

**Generated:** 2025-12-07 00:42:20  
**Status:** ⚠️ AI Analysis Not Available - Basic Report Generated

---

## 📊 Plan Summary

This Terraform plan proposes **6 infrastructure changes**:

- **3 resources to add** ✅
- **2 resources to change** 🔄
- **1 resources to destroy** ❌

---

## 📝 Changes Breakdown

### ✅ Resources to Add (3)

1. `google_compute_firewall.ssh`
2. `google_container_node_pool.system`
3. `google_sql_user.readonly`

### 🔄 Resources to Change (2)

1. `google_compute_subnetwork.private`
2. `google_sql_database_instance.primary`

### ❌ Resources to Destroy (1)

1. `google_pubsub_topic.audit`

---

## 🔍 Raw Terraform Plan Output

```terraform
Terraform v1.9.0
on linux_amd64
Configuring remote state backend...

Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/google versions matching "~> 5.0"...
- Installing hashicorp/google v5.12.0...
- Installed hashicorp/google v5.12.0 (signed by HashiCorp)
- Finding hashicorp/random versions matching "~> 3.0"...
- Installed hashicorp/random v3.6.0 (signed by HashiCorp)

Terraform has been successfully initialized!

module.project.module.network.google_compute_network.main: Refreshing state...
module.project.module.network.google_compute_subnetwork.public[0]: Refreshing state...
module.project.module.network.google_compute_subnetwork.private[0]: Refreshing state...
module.project.module.gke.google_container_cluster.primary: Refreshing state...
module.project.module.sql.google_sql_database_instance.primary: Refreshing state...

------------------------------------------------------------------------

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create
  ~ update in-place
  - destroy
  +/- create replacement and then destroy

Terraform will perform the following actions:

  # module.project.module.network.google_compute_firewall.ssh will be created
  + resource "google_compute_firewall" "ssh" {
      + name    = "allow-ssh-from-bastion"
      + network = module.project.module.network.google_compute_network.main.name
      + project = "sample-project"

      + allow {
          + protocol = "tcp"
          + ports    = ["22"]
        }

      + source_ranges = [
          "10.0.10.0/24",
        ]
      + target_tags = ["bastion"]
    }

  # module.project.module.network.google_compute_subnetwork.private[0] will be updated in-place
  ~ resource "google_compute_subnetwork" "private" {
        name          = "private-subnet-1"
        ip_cidr_range = "10.0.2.0/24"
      ~ secondary_ip_range = [
          + {
              range_name    = "pods-range"
              ip_cidr_range = "10.16.0.0/14"
            },
          + {
              range_name    = "services-range"
              ip_cidr_range = "10.20.0.0/20"
            },
        ]
    }

  # module.project.module.gke.google_container_cluster.primary must be replaced
 +/- resource "google_container_cluster" "primary" {
        name                     = "primary-gke-cluster"
        location                 = "us-central1"
        initial_node_count       = 1
      ~ networking_mode          = "VPC_NATIVE" -> "VPC_NATIVE"
      ~ enable_autopilot         = false -> true # forces replacement
      ~ remove_default_node_pool = true -> true

        ip_allocation_policy {
          cluster_secondary_range_name  = "gke-pods"
          services_secondary_range_name = "gke-services"
        }

      - master_authorized_networks_config {
          - cidr_blocks {
              - cidr_block   = "0.0.0.0/0"
              - display_name = "public-access"
            }
        }

      + release_channel {
          + channel = "REGULAR"
        }
    }

  # module.project.module.gke.google_container_node_pool.system will be created
  + resource "google_container_node_pool" "system" {
      + name       = "system-pool"
      + cluster    = google_container_cluster.primary.name
      + location   = "us-central1"
      + node_count = 3

      + node_config {
          + machine_type = "e2-standard-4"
          + disk_size_gb = 100
          + oauth_scopes = ["https://www.googleapis.com/auth/cloud-platform"]

          + labels = {
              "role" = "system"
            }
        }

      + management {
          + auto_repair  = true
          + auto_upgrade = true
        }
    }

  # module.project.module.sql.google_sql_database_instance.primary will be updated in-place
  ~ resource "google_sql_database_instance" "primary" {
        name             = "orders-db"
        database_version = "POSTGRES_13"
      ~ settings {
          ~ tier = "db-custom-2-7680" -> "db-custom-4-15360"
          ~ backup_configuration {
              ~ enabled = false -> true
                binary_log_enabled = false
            }
          + insights_config {
              + query_insights_enabled  = true
              + query_string_length     = 1024
              + record_application_tags = true
            }
        }
    }

  # module.project.module.sql.google_sql_user.readonly will be created
  + resource "google_sql_user" "readonly" {
      + instance = google_sql_database_instance.primary.name
      + name     = "readonly_user"
      + password = (sensitive value)
      + type     = "BUILT_IN"
    }

  # module.project.google_pubsub_topic.audit will be destroyed
  - resource "google_pubsub_topic" "audit" {
      - name  = "legacy-audit-topic" -> null
      - labels = {
          - "system" = "legacy"
        }
    }

Plan: 3 to add, 2 to change, 1 to destroy, 1 to replace.

─────────────────────────────────────────────────────────────────────────────

```

---

## 💡 Recommendations

Since this is a basic report without AI analysis:

1. Review the raw plan output carefully
2. Try generating an AI-powered report again later
3. Manually review each resource change for security and data-loss risks