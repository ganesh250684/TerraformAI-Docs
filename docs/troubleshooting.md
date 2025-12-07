# Troubleshooting Guide

## 🔍 Common Issues & Solutions

### Issue: Extension Not Found in Marketplace

**Symptoms:**
- Can't find "TerraformAI" when searching
- Search returns other extensions

**Solutions:**
1. **Search for exact name:** `TerraformAI`
2. **Try publisher name:** `cloudcraft`
3. **Use direct link:** [Install TerraformAI](https://marketplace.visualstudio.com/items?itemName=cloudcraft.terraformai)
4. **Check VS Code version:** Requires VS Code 1.80.0 or higher

---

### Issue: Report Generation Fails

**Symptoms:**
- Error message when generating report
- No output file created
- Extension crashes

**Solutions:**

#### 1. Verify Terraform Plan Format

```bash
# ✅ CORRECT - Use -no-color
terraform show -no-color plan.tfplan > plan.txt

# ❌ WRONG - Colored output causes parsing errors
terraform show plan.tfplan > plan.txt
```

#### 2. Check File Extension

File must have `.txt` extension:
```bash
# ✅ CORRECT
terraform show -no-color plan.tfplan > plan.txt

# ❌ WRONG
terraform show -no-color plan.tfplan > plan
```

#### 3. Verify Plan Contains Changes

```bash
# Check file isn't empty
ls -lh plan.txt  # Should be > 0 bytes

# View content
head -20 plan.txt  # Should show Terraform output
```

#### 4. Check PowerShell Installation (Windows)

```powershell
# Verify PowerShell is available
pwsh --version

# If not installed, download from:
# https://github.com/PowerShell/PowerShell/releases
```

#### 5. Reload VS Code

```
Ctrl+Shift+P → Type "Reload Window" → Enter
```

---

### Issue: Context Menu Not Appearing

**Symptoms:**
- Right-click doesn't show "Terraform: Generate Plan Report"
- Extension seems inactive

**Solutions:**

1. **Verify File Extension**
   - File must be `.txt`
   - Right-click **inside the file editor**, not in file explorer

2. **Check Extension is Enabled**
   ```
   Extensions → Search "TerraformAI" → Ensure enabled
   ```

3. **Verify Extension Activation**
   - Look for "TerraformAI" in status bar (bottom right)
   - If not visible, extension may not be activated

4. **Use Command Palette Instead**
   ```
   Ctrl+Shift+P → "Terraform: Generate Plan Report"
   ```

5. **Reinstall Extension**
   ```
   Extensions → TerraformAI → Uninstall
   Reload VS Code
   Extensions → Search "TerraformAI" → Install
   ```

---

### Issue: PDF Export Not Working

**Symptoms:**
- Only Markdown report generated
- No PDF file created
- PDF generation error

**Solutions:**

1. **Check Markdown Report First**
   - Markdown `.md` file is always generated
   - PDF is optional enhancement

2. **PDF Dependencies** (Automatic)
   - Extension handles PDF conversion automatically
   - If PDF fails, Markdown report is still available

3. **Use Markdown Instead**
   ```json
   {
     "terraformReport.defaultExport": "markdown"
   }
   ```

4. **Manual PDF Conversion**
   - Open `.md` file in VS Code
   - Right-click → "Markdown: Export to PDF" (if you have Markdown extensions)
   - Or use online converters: markdown-to-pdf.com

---

### Issue: Extension Slow or Hangs

**Symptoms:**
- Report generation takes very long
- VS Code becomes unresponsive
- Extension freezes

**Solutions:**

1. **Check Plan File Size**
   ```bash
   ls -lh plan.txt
   ```
   - Files > 10MB may take longer
   - Consider filtering plan with `-target`

2. **Use Basic Mode for Large Plans**
   ```json
   {
     "terraformReport.mode": "basic"
   }
   ```

3. **Close Other Extensions**
   - Temporarily disable other extensions
   - Check if conflict exists

4. **Increase VS Code Memory**
   ```bash
   code --max-memory=4096
   ```

5. **Filter Large Plans**
   ```bash
   # Target specific resources
   terraform plan -target=aws_instance.example -no-color > plan.txt
   ```

---

### Issue: "No Changes Detected" Error

**Symptoms:**
- Error: "No Terraform changes found in file"
- Empty report generated

**Solutions:**

1. **Verify Plan Has Changes**
   ```bash
   terraform plan  # Should show changes
   terraform plan -out=plan.tfplan
   terraform show -no-color plan.tfplan > plan.txt
   ```

2. **Check File Content**
   ```bash
   cat plan.txt  # Should contain Terraform output
   head -50 plan.txt  # View first 50 lines
   ```

3. **Ensure Plan File is Fresh**
   ```bash
   # Regenerate plan
   rm plan.txt
   terraform plan -out=plan.tfplan
   terraform show -no-color plan.tfplan > plan.txt
   ```

4. **Check for Parse Errors**
   - Look for unusual characters in plan.txt
   - Remove ANSI color codes: use `-no-color` flag

---

### Issue: AI Features Not Working

**Symptoms:**
- AI report option disabled
- "AI features coming soon" message
- Can't access AI analysis

**Solutions:**

**AI features are launching December 2025**

Current status:
- ✅ Basic reports: Available now (free)
- 🔮 AI reports: Coming December 2025

To be notified:
- ⭐ Star the extension on Marketplace
- 📧 Subscribe to updates (coming soon)

---

### Issue: Configuration Not Working

**Symptoms:**
- Settings not taking effect
- Changes ignored

**Solutions:**

1. **Check Settings Scope**
   ```
   User Settings (global) vs Workspace Settings (project-specific)
   ```

2. **Reload After Changes**
   ```
   Ctrl+Shift+P → "Reload Window"
   ```

3. **Verify JSON Syntax**
   ```json
   // ✅ CORRECT
   {
     "terraformReport.mode": "basic"
   }

   // ❌ WRONG (missing comma, quotes)
   {
     "terraformReport.mode": basic,
   }
   ```

4. **Reset to Defaults**
   ```
   Settings → Search "terraformReport" → Click reset icon on each setting
   ```

---

### Issue: Extension Not Activating

**Symptoms:**
- Extension installed but doesn't work
- No commands available
- No status bar item

**Solutions:**

1. **Check Activation Events**
   - Open a `.txt` file
   - Extension activates on .txt file open

2. **View Extension Logs**
   ```
   Help → Toggle Developer Tools → Console tab
   Filter: "TerraformAI"
   ```

3. **Check for Conflicts**
   - Disable other Terraform-related extensions temporarily
   - Test if TerraformAI works alone

4. **Clean Reinstall**
   ```bash
   # Uninstall
   code --uninstall-extension cloudcraft.terraformai
   
   # Clear cache (optional)
   # Windows: %USERPROFILE%\.vscode\extensions
   # Mac/Linux: ~/.vscode/extensions
   
   # Reinstall
   code --install-extension cloudcraft.terraformai
   ```

---

### Issue: Plan File Not Recognized

**Symptoms:**
- "Invalid Terraform plan format"
- Parser errors

**Solutions:**

1. **Use Standard Terraform Commands**
   ```bash
   # Correct workflow
   terraform init
   terraform plan -out=plan.tfplan
   terraform show -no-color plan.tfplan > plan.txt
   ```

2. **Avoid Direct `terraform plan` Output**
   ```bash
   # ❌ DON'T DO THIS (unstable format)
   terraform plan > plan.txt
   
   # ✅ DO THIS (stable format)
   terraform plan -out=plan.tfplan
   terraform show -no-color plan.tfplan > plan.txt
   ```

3. **Check Terraform Version**
   ```bash
   terraform version  # Supports 0.12+
   ```

4. **Validate Terraform State**
   ```bash
   terraform validate
   terraform fmt -check
   ```

---

## 🆘 Still Having Issues?

### Getting Help

1. **Check Documentation**
   - [Getting Started](getting-started.md)
   - [Configuration Guide](configuration.md)
   - [FAQ](faq.md)

2. **Search Existing Issues**
   - [GitHub Issues](https://github.com/ganesh250684/TerraformReportExtension/issues)
   - Someone may have solved your problem!

3. **Open a New Issue**
   - [Report Bug](https://github.com/ganesh250684/TerraformReportExtension/issues/new)
   - Include:
     - Extension version
     - VS Code version
     - Operating system
     - Sample plan file (sanitized)
     - Error messages
     - Steps to reproduce

4. **Join Discussion**
   - [GitHub Discussions](https://github.com/ganesh250684/TerraformReportExtension/discussions)
   - Ask questions, share tips

---

## 📋 Debug Information Checklist

When reporting issues, provide:

```bash
# 1. Extension version
code --list-extensions --show-versions | grep terraformai

# 2. VS Code version
code --version

# 3. Operating system
uname -a  # Mac/Linux
systeminfo  # Windows

# 4. Terraform version
terraform version

# 5. PowerShell version (Windows)
pwsh --version

# 6. Plan file info
ls -lh plan.txt
head -50 plan.txt

# 7. Extension logs
# Help → Toggle Developer Tools → Console
```

---

## 🔧 Advanced Troubleshooting

### Enable Debug Logging

```json
{
  "terraformReport.debug": true
}
```

View logs: `Output` panel → Select "TerraformAI" from dropdown

### Test Extension Directly

```javascript
// Run in VS Code Developer Tools Console
vscode.commands.getCommands().then(commands => {
  console.log(commands.filter(c => c.includes('terraform')));
});
```

### Verify Extension Files

```bash
# Extension location
# Windows: %USERPROFILE%\.vscode\extensions\cloudcraft.terraformai-*
# Mac: ~/.vscode/extensions/cloudcraft.terraformai-*
# Linux: ~/.vscode/extensions/cloudcraft.terraformai-*

# Check files exist
ls ~/.vscode/extensions/cloudcraft.terraformai-*/
```

---

**Need more help?** [Open an issue](https://github.com/ganesh250684/TerraformReportExtension/issues) with debug information!
