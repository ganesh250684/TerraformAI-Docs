# Configuration Guide

## ⚙️ Extension Settings

Access settings: `File` → `Preferences` → `Settings` (or `Ctrl+,`) → Search "Terraform Report"

---

## 📋 Available Settings

### Report Generation Mode

```json
{
  "terraformReport.mode": "auto"
}
```

**Options:**
- `auto` - Automatically detect complexity and choose best mode (default)
- `basic` - Always use basic report (fast, offline)
- `ai` - Always use AI-enhanced report (when available)

**When to use:**
- **auto:** Default choice, lets extension decide
- **basic:** For quick reviews, no AI needed
- **ai:** For production changes, complex infrastructure

---

### Default Export Format

```json
{
  "terraformReport.defaultExport": "pdf"
}
```

**Options:**
- `pdf` - Export to PDF format (default)
- `markdown` - Export to Markdown (.md) format
- `both` - Generate both PDF and Markdown

**When to use:**
- **pdf:** For sharing with stakeholders, professional presentation
- **markdown:** For version control, editing, GitHub
- **both:** When you need both formats

---

### Auto-Open Report

```json
{
  "terraformReport.openAfterGenerate": true
}
```

**Options:**
- `true` - Automatically open report after generation (default)
- `false` - Just generate report, don't open

**When to use:**
- **true:** Interactive use, immediate review
- **false:** Batch processing, CI/CD pipelines

---

### Template Style

```json
{
  "terraformReport.templateStyle": "professional"
}
```

**Options:**
- `professional` - Clean, business-ready format (default)
- `minimal` - Compact, essential information only
- `detailed` - Comprehensive, includes all attributes

**When to use:**
- **professional:** Standard reports, stakeholder reviews
- **minimal:** Quick scans, daily changes
- **detailed:** Deep analysis, troubleshooting

---

### Auto-Detection Thresholds

```json
{
  "terraformReport.autoDetectThreshold": {
    "destroyCount": 1,
    "changeCount": 10,
    "totalChanges": 15
  }
}
```

**When mode is `auto`, these thresholds trigger AI analysis:**

- `destroyCount` - Number of destroy operations (default: 1)
- `changeCount` - Number of modify operations (default: 10)
- `totalChanges` - Total resource changes (default: 15)

**Example:**
If plan has 2 destroys → Triggers AI analysis (above threshold)
If plan has 5 creates, 3 changes → Uses basic report (below threshold)

---

## 🎨 Complete Configuration Example

```json
{
  // Report generation settings
  "terraformReport.mode": "auto",
  "terraformReport.defaultExport": "pdf",
  "terraformReport.openAfterGenerate": true,
  "terraformReport.templateStyle": "professional",
  
  // AI features (coming soon)
  "terraformReport.apiEndpoint": "https://api.terraformai.com/v1",
  "terraformReport.apiKey": "",
  
  // Auto-detection thresholds
  "terraformReport.autoDetectThreshold": {
    "destroyCount": 1,
    "changeCount": 10,
    "totalChanges": 15
  },
  
  // Optional audit logging
  "terraformReport.enableAuditLogging": false,
  "terraformReport.databaseConnection": {
    "host": "localhost",
    "port": 1433,
    "database": "TerraformAudit",
    "username": "",
    "password": "",
    "encrypt": true
  }
}
```

---

## 📊 Use Case Examples

### Configuration for Daily Development

```json
{
  "terraformReport.mode": "basic",
  "terraformReport.defaultExport": "markdown",
  "terraformReport.openAfterGenerate": true,
  "terraformReport.templateStyle": "minimal"
}
```

**Why:**
- Basic mode for speed
- Markdown for version control
- Auto-open for immediate review
- Minimal style for quick scans

---

### Configuration for Production Deployments

```json
{
  "terraformReport.mode": "ai",
  "terraformReport.defaultExport": "both",
  "terraformReport.openAfterGenerate": true,
  "terraformReport.templateStyle": "professional"
}
```

**Why:**
- AI mode for comprehensive analysis
- Both formats (PDF for approval, MD for history)
- Auto-open to review immediately
- Professional style for stakeholders

---

### Configuration for CI/CD Pipelines

```json
{
  "terraformReport.mode": "basic",
  "terraformReport.defaultExport": "markdown",
  "terraformReport.openAfterGenerate": false,
  "terraformReport.templateStyle": "detailed"
}
```

**Why:**
- Basic mode (no API calls needed)
- Markdown (easy to parse in pipelines)
- No auto-open (headless environment)
- Detailed for complete information

---

## 🔐 API Configuration (For AI Features)

### Get Your API Key

1. Visit: https://app.terraformai.com (coming soon)
2. Sign up / Log in
3. Go to Settings → API Keys
4. Generate new API key
5. Copy to clipboard

### Configure API Key

**Option 1: VS Code Settings (Recommended)**

```json
{
  "terraformReport.apiKey": "your-api-key-here"
}
```

**Option 2: Environment Variable**

```bash
# Linux/Mac
export TERRAFORM_REPORT_API_KEY="your-api-key-here"

# Windows (PowerShell)
$env:TERRAFORM_REPORT_API_KEY = "your-api-key-here"

# Windows (CMD)
set TERRAFORM_REPORT_API_KEY=your-api-key-here
```

---

## 🗄️ Optional Audit Logging

**Note:** Only enable if you need audit trails. Requires SQL Server.

### Enable Audit Logging

```json
{
  "terraformReport.enableAuditLogging": true,
  "terraformReport.databaseConnection": {
    "host": "your-sql-server.database.windows.net",
    "port": 1433,
    "database": "TerraformAudit",
    "username": "admin",
    "password": "your-password",
    "encrypt": true
  }
}
```

### What Gets Logged

- Timestamp of report generation
- User who generated report
- Plan file hash
- Number of resources changed
- AI analysis results (if used)

**Use cases:**
- Compliance requirements
- Audit trails
- Change tracking
- Team metrics

---

## 📝 Configuration Tips

### 1. Per-Project Settings

Create `.vscode/settings.json` in your project:

```json
{
  "terraformReport.mode": "ai",
  "terraformReport.templateStyle": "professional"
}
```

This overrides global settings for this project only.

### 2. Team Settings

Share settings via workspace file:

```json
// project.code-workspace
{
  "settings": {
    "terraformReport.mode": "auto",
    "terraformReport.defaultExport": "pdf"
  }
}
```

Commit to version control for team consistency.

### 3. Environment-Specific

Use different modes per environment:

```bash
# Development
export TERRAFORM_REPORT_MODE="basic"

# Production
export TERRAFORM_REPORT_MODE="ai"
```

---

## 🔧 Advanced Configuration

### Custom Output Directory

Reports are saved in the same directory as the plan file by default.

To change output directory, use workspace settings:

```json
{
  "terraformReport.outputDirectory": "./terraform-reports"
}
```

### File Naming Pattern

Customize report filenames:

```json
{
  "terraformReport.filenamePattern": "terraform-report-{timestamp}.{format}"
}
```

**Variables:**
- `{timestamp}` - Current datetime
- `{project}` - Project name (from folder)
- `{environment}` - Environment (from filename or var)
- `{format}` - File extension (pdf/md)

---

## ❓ Need Help?

- [Getting Started Guide](getting-started.md)
- [FAQ](faq.md)
- [Troubleshooting](troubleshooting.md)
- [Report Issues](https://github.com/ganesh250684/TerraformReportExtension/issues)
