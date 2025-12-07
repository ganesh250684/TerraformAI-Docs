# ⚠️ Terraform Plan Basic Report

**Generated:** 2025-12-07 00:42:19  
**Status:** ⚠️ AI Analysis Not Available - Basic Report Generated

---

## 📊 Plan Summary

This Terraform plan proposes **5 infrastructure changes**:

- **3 resources to add** ✅
- **1 resources to change** 🔄
- **1 resources to destroy** ❌

---

## 📝 Changes Breakdown

### ✅ Resources to Add (3)

1. `azurerm_virtual_network_peering.hub_to_spoke`
2. `azurerm_virtual_network_peering.spoke_to_hub`
3. `azurerm_private_endpoint.sql`

### 🔄 Resources to Change (1)

1. `azurerm_linux_web_app.api`

### ❌ Resources to Destroy (1)

1. `azurerm_monitor_diagnostic_setting.api`

---

## 🔍 Raw Terraform Plan Output

```terraform
Terraform v1.9.1
on windows_amd64

Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/azurerm versions matching "~> 4.0"...
- Installing hashicorp/azurerm v4.4.0...
- Installed hashicorp/azurerm v4.4.0
- Installing hashicorp/random v3.6.0...

Terraform has been successfully initialized!

module.hub.azurerm_resource_group.hub: Refreshing state...
module.hub.azurerm_virtual_network.hub_vnet: Refreshing state...
module.spoke.azurerm_virtual_network.spoke_vnet: Refreshing state...
module.app.azurerm_linux_web_app.api: Refreshing state...
module.data.azurerm_mssql_database.appdb: Refreshing state...

------------------------------------------------------------------------

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create
  ~ update in-place
  - destroy
  +/- create replacement and then destroy

Terraform will perform the following actions:

  # module.hub.azurerm_virtual_network_peering.hub_to_spoke will be created
  + resource "azurerm_virtual_network_peering" "hub_to_spoke" {
      + name                      = "hub-to-spoke"
      + resource_group_name       = module.hub.azurerm_resource_group.hub.name
      + virtual_network_name      = module.hub.azurerm_virtual_network.hub_vnet.name
      + remote_virtual_network_id = module.spoke.azurerm_virtual_network.spoke_vnet.id
      + allow_forwarded_traffic   = true
      + allow_gateway_transit     = true
      + use_remote_gateways       = false
    }

  # module.spoke.azurerm_virtual_network_peering.spoke_to_hub will be created
  + resource "azurerm_virtual_network_peering" "spoke_to_hub" {
      + name                      = "spoke-to-hub"
      + resource_group_name       = module.spoke.azurerm_resource_group.spoke.name
      + virtual_network_name      = module.spoke.azurerm_virtual_network.spoke_vnet.name
      + remote_virtual_network_id = module.hub.azurerm_virtual_network.hub_vnet.id
      + allow_forwarded_traffic   = true
      + allow_gateway_transit     = false
      + use_remote_gateways       = true
    }

  # module.app.azurerm_linux_web_app.api will be updated in-place
  ~ resource "azurerm_linux_web_app" "api" {
        name                = "ge-api-prod"
        resource_group_name = module.app.azurerm_resource_group.app.name
        service_plan_id     = module.app.azurerm_service_plan.app_sp.id
        https_only          = true
      ~ tags                = {
          + "Environment" = "Prod"
          + "Owner"       = "PlatformTeam"
        }

      ~ site_config {
          ~ minimum_tls_version = "1.1" -> "1.2"
          ~ always_on           = false -> true
          + http2_enabled       = true
        }

      ~ app_settings = {
          ~ "ASPNETCORE_ENVIRONMENT" = "Staging" -> "Production"
          + "APPINSIGHTS_INSTRUMENTATIONKEY" = azurerm_application_insights.app.instrumentation_key
        }
    }

  # module.data.azurerm_mssql_database.appdb must be replaced
 +/- resource "azurerm_mssql_database" "appdb" {
        name           = "appdb"
        server_id      = module.data.azurerm_mssql_server.sql.id
      ~ sku_name       = "GP_Gen5_4" -> "GP_Gen5_8" # forces replacement
      ~ max_size_gb    = 250 -> 512
      ~ zone_redundant = false -> true
    }

  # module.data.azurerm_private_endpoint.sql will be created
  + resource "azurerm_private_endpoint" "sql" {
      + name                = "pep-sql-appdb"
      + location            = module.data.azurerm_resource_group.data.location
      + resource_group_name = module.data.azurerm_resource_group.data.name
      + subnet_id           = module.spoke.azurerm_subnet.app_subnet.id

      + private_service_connection {
          + name                           = "sql-connection"
          + is_manual_connection           = false
          + private_connection_resource_id = module.data.azurerm_mssql_server.sql.id
          + subresource_names              = ["sqlServer"]
        }
    }

  # module.app.azurerm_monitor_diagnostic_setting.api will be destroyed
  - resource "azurerm_monitor_diagnostic_setting" "api" {
      - name                       = "diag-api" -> null
      - target_resource_id         = module.app.azurerm_linux_web_app.api.id -> null
      - log_analytics_workspace_id = azurerm_log_analytics_workspace.law.id -> null
    }

Plan: 3 to add, 1 to change, 1 to destroy, 1 to replace (1 resource destroyed).

─────────────────────────────────────────────────────────────────────────────

```

---

## 💡 Recommendations

Since this is a basic report without AI analysis:

1. Review the raw plan output carefully
2. Try generating an AI-powered report again later
3. Manually review each resource change for security and data-loss risks