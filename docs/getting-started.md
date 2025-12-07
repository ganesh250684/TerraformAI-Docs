# Getting Started with TerraformAI

## 📦 Installation

### Method 1: VS Code Marketplace (Recommended)

1. Open **Visual Studio Code**
2. Press `Ctrl+Shift+X` (Windows/Linux) or `Cmd+Shift+X` (Mac)
3. Search for **"TerraformAI"**
4. Click **Install**
5. Reload VS Code

### Method 2: Command Line

```bash
code --install-extension cloudcraft.terraformai
```

---

## 🚀 Generate Your First Report

### Step 1: Create Terraform Plan Output

```bash
# Navigate to your Terraform project
cd /path/to/terraform/project

# Generate plan
terraform plan -out=plan.tfplan

# Convert to text format
terraform show -no-color plan.tfplan > plan.txt
```

### Step 2: Generate Report in VS Code

**Option A: Right-Click Menu (Easiest)**
1. Open `plan.txt` in VS Code
2. Right-click anywhere in the file
3. Select **"Terraform: Generate Plan Report"**
4. Report opens automatically!

**Option B: Command Palette**
1. Open `plan.txt` in VS Code
2. Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (Mac)
3. Type **"Terraform: Generate Plan Report"**
4. Press Enter

**Option C: Keyboard Shortcut**
1. Open `plan.txt` in VS Code
2. Press `Ctrl+Alt+T` (Windows/Linux) or `Cmd+Alt+T` (Mac)

---

## 📊 Report Modes

### Basic Mode (Free - Available Now)

Fast, offline report generation with:
- ✅ Resource changes summary
- ✅ Detailed attribute listing
- ✅ Color-coded actions
- ✅ Export to PDF/Markdown
- ✅ Generated in 2 seconds

**Best for:**
- Daily routine changes
- Quick peer reviews
- Simple infrastructure updates

### AI-Enhanced Mode (Coming Soon)

Intelligent analysis with:
- 🧠 Risk assessment
- 💰 Cost projections
- 🔒 Security recommendations
- 📋 Deployment checklists
- 🔄 Rollback procedures

**Best for:**
- Production deployments
- Complex multi-resource changes
- Security-critical updates
- Stakeholder presentations

---

## 🎯 Common Workflows

### Workflow 1: Pre-Deployment Review

```bash
# 1. Generate plan
terraform plan -out=plan.tfplan
terraform show -no-color plan.tfplan > plan.txt

# 2. Generate report in VS Code (right-click on plan.txt)

# 3. Review report for:
#    - Unexpected changes
#    - Destroy operations
#    - Resource counts

# 4. If approved, apply
terraform apply plan.tfplan
```

### Workflow 2: Change Request Documentation

```bash
# 1. Generate plan and report
terraform plan -out=plan.tfplan
terraform show -no-color plan.tfplan > plan.txt
# Generate report in VS Code

# 2. Export report to PDF
# 3. Attach PDF to Jira/ServiceNow ticket
# 4. Await approval
# 5. Apply changes after approval
```

### Workflow 3: Team Code Review

```bash
# 1. Create feature branch
git checkout -b feature/new-infrastructure

# 2. Make Terraform changes
# 3. Generate plan and report
terraform plan > plan.txt
# Generate report in VS Code

# 4. Commit report with code
git add plan-report.md
git commit -m "Add new infrastructure with report"

# 5. Create pull request with report visible
# 6. Team reviews changes quickly
```

---

## ⚙️ Configuration

See [Configuration Guide](configuration.md) for detailed settings.

### Quick Settings

Press `Ctrl+,` and search for "Terraform Report":

```json
{
  // Default export format
  "terraformReport.defaultExport": "pdf",
  
  // Auto-open report after generation
  "terraformReport.openAfterGenerate": true,
  
  // Report mode (auto/basic/ai)
  "terraformReport.mode": "auto"
}
```

---

## 🎓 Tips & Best Practices

### 1. Use `-no-color` Flag

Always use `-no-color` when generating plan output:
```bash
terraform show -no-color plan.tfplan > plan.txt
```

This ensures clean parsing without ANSI color codes.

### 2. Save Plan Files

Save your plan files with timestamps for history:
```bash
terraform show -no-color plan.tfplan > plan-$(date +%Y%m%d-%H%M%S).txt
```

### 3. Review Destroy Operations

Always check the report for `destroy` operations before applying:
- Look for red/highlighted destroy actions
- Verify you intend to delete those resources

### 4. Archive Reports

Keep reports for compliance and audit:
```bash
mkdir -p terraform-reports
mv *.pdf terraform-reports/
```

### 5. Share with Team

Export to PDF for easy sharing:
- Non-technical stakeholders can review
- No Terraform knowledge required
- Professional appearance

---

## ❓ Troubleshooting

See [Troubleshooting Guide](troubleshooting.md) for common issues.

### Quick Fixes

**Report Generation Fails:**
- Ensure PowerShell is installed
- Check file is valid Terraform output
- Try regenerating plan with `-no-color`

**PDF Not Generated:**
- Markdown report is always generated
- PDF requires additional tools (automatic fallback)

**Extension Not Appearing:**
- Reload VS Code: `Ctrl+Shift+P` → "Reload Window"
- Check extension is enabled
- Restart VS Code

---

## 📚 Next Steps

- [Configuration Options](configuration.md)
- [View Sample Reports](../samples/)
- [FAQ](faq.md)
- [Report Issues](https://github.com/ganesh250684/TerraformReportExtension/issues)

---

**Need help?** [Open an issue](https://github.com/ganesh250684/TerraformReportExtension/issues) or [start a discussion](https://github.com/ganesh250684/TerraformReportExtension/discussions)!
