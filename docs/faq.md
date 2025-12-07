# Frequently Asked Questions (FAQ)

## 📦 Installation & Setup

### Q: How do I install TerraformAI?

**A:** Open VS Code → Extensions (`Ctrl+Shift+X`) → Search "TerraformAI" → Install

Or via command line:
```bash
code --install-extension cloudcraft.terraformai
```

### Q: Do I need to install anything else?

**A:** No! TerraformAI works out of the box. Basic reports are 100% self-contained.

### Q: Does it work on Mac/Linux/Windows?

**A:** Yes! TerraformAI works on all platforms where VS Code runs.

---

## 🚀 Usage

### Q: How do I generate a report?

**A:** 
1. Generate Terraform plan: `terraform plan -out=plan.tfplan`
2. Convert to text: `terraform show -no-color plan.tfplan > plan.txt`
3. Right-click `plan.txt` in VS Code → "Terraform: Generate Plan Report"

### Q: Can I use it with `terraform plan` output directly?

**A:** Yes! Just redirect output to a file:
```bash
terraform plan -no-color > plan.txt
```
Then generate report from `plan.txt`

### Q: How long does it take to generate a report?

**A:** 
- **Basic reports:** 1-3 seconds (instant!)
- **AI reports:** 30-60 seconds (when available)

### Q: Can I generate reports in CI/CD pipelines?

**A:** Absolutely! Use the extension via VS Code CLI or use our standalone CLI tool (coming soon).

---

## 📊 Report Features

### Q: What's the difference between Basic and AI reports?

**A:**

| Feature | Basic (Free) | AI (Coming Soon) |
|---------|-------------|------------------|
| Speed | 2 seconds | 30-60 seconds |
| Resource listing | ✅ | ✅ |
| Attribute details | ✅ | ✅ |
| Color coding | ✅ | ✅ |
| Risk assessment | ❌ | ✅ |
| Cost analysis | ❌ | ✅ |
| Security recommendations | ❌ | ✅ |
| Deployment checklists | ❌ | ✅ |

### Q: Can I export reports to PDF?

**A:** Yes! Reports can be exported to:
- PDF (default)
- Markdown
- HTML
- Both PDF and Markdown

### Q: Can I customize the report format?

**A:** Yes! Choose from 3 styles in settings:
- `professional` - Business-ready (default)
- `minimal` - Compact, essential info only
- `detailed` - Comprehensive, all attributes

---

## 💰 Pricing & AI Features

### Q: Is TerraformAI free?

**A:** 
- ✅ **Basic reports:** 100% FREE forever, unlimited
- 🔮 **AI reports:** 5 free reports, then pay-per-use (coming Dec 2025)

### Q: When will AI features be available?

**A:** AI-enhanced reports are launching in **December 2025**. Subscribe to updates to be notified!

### Q: How much will AI reports cost?

**A:** Usage is measured in credits based on plan complexity:
- Simple plans (~10 resources): ~1 credit
- Medium plans (~50 resources): ~2-3 credits
- Large plans (100+ resources): ~5-8 credits
- 5 free reports included for all users

### Q: Can I use my own OpenAI API key?

**A:** Not currently, but this feature is planned for future releases.

---

## 🔒 Privacy & Security

### Q: Where is my Terraform data sent?

**A:** 
- **Basic reports:** 100% LOCAL. Nothing is sent anywhere!
- **AI reports:** Sent to our API for AI analysis (when you choose AI mode)

### Q: Is my infrastructure data secure?

**A:** Yes! We use:
- TLS encryption in transit
- No data retention (deleted after analysis)
- SOC 2 compliant infrastructure (coming soon)
- Optional self-hosted deployment (enterprise)

### Q: Can I use this offline?

**A:** Yes! Basic reports work 100% offline. No internet required.

---

## 🛠️ Cloud Providers

### Q: Which cloud providers are supported?

**A:** ALL of them! Including:
- ✅ AWS (Amazon Web Services)
- ✅ Azure (Microsoft Azure)
- ✅ GCP (Google Cloud Platform)
- ✅ Oracle Cloud
- ✅ Digital Ocean
- ✅ Heroku
- ✅ Kubernetes
- ✅ Any Terraform provider

### Q: Do I need different settings for each cloud?

**A:** No! TerraformAI automatically detects the cloud provider and optimizes the report format.

---

## 🐛 Troubleshooting

### Q: Report generation failed. What should I do?

**A:** Check these common issues:
1. Ensure file is valid Terraform plan output
2. Use `-no-color` flag: `terraform show -no-color`
3. Verify PowerShell is installed
4. Try reloading VS Code: `Ctrl+Shift+P` → "Reload Window"

### Q: PDF export isn't working

**A:** PDF generation requires additional tools. Markdown reports always work. PDF will fallback to Markdown if tools aren't available.

### Q: Extension doesn't appear in context menu

**A:** 
1. Ensure extension is installed and enabled
2. Check file has `.txt` extension
3. Try reloading VS Code window
4. Verify extension activation: Check for "TerraformAI" in status bar

### Q: Getting "No changes detected" error

**A:** 
- Ensure plan file contains actual changes
- Try `terraform plan -out=plan.tfplan` instead of just `terraform plan`
- Verify file isn't empty: `ls -lh plan.txt`

---

## 🎯 Best Practices

### Q: Should I commit reports to Git?

**A:** 
- ✅ **YES for:** Markdown reports, documentation, change history
- ❌ **NO for:** Large PDF files (use .gitignore)

Example `.gitignore`:
```
*.pdf
plan.tfplan
```

### Q: How should I organize reports?

**A:**
```
project/
├── terraform-reports/
│   ├── 2025-12-07-production.md
│   ├── 2025-12-06-staging.md
│   └── archive/
└── terraform/
```

### Q: Can I automate report generation?

**A:** Yes! Several approaches:
1. Git pre-commit hooks
2. CI/CD pipeline step
3. Terraform wrapper script
4. VS Code tasks/launch configs

---

## 🔄 Integration

### Q: Can I integrate with Jira/ServiceNow?

**A:** Yes! Generate PDF report and attach to tickets. API integration coming soon.

### Q: Does it work with Terraform Cloud/Enterprise?

**A:** Yes! Generate plan output from TF Cloud and use TerraformAI locally.

```bash
# Download plan from Terraform Cloud
terraform show -no-color runs/run-xxx > plan.txt
# Generate report
```

### Q: Can I use it in GitHub Actions?

**A:** Yes! Example workflow:
```yaml
- name: Generate Terraform Report
  run: |
    terraform show -no-color tfplan > plan.txt
    # Use VS Code CLI to generate report
    code --install-extension cloudcraft.terraformai
    # (CLI support coming soon)
```

---

## 📚 Learning & Support

### Q: Are there video tutorials?

**A:** Coming soon! Subscribe to updates to be notified.

### Q: Where can I get help?

**A:** 
- 📖 [Documentation](https://github.com/ganesh250684/TerraformAI-Docs)
- 🐛 [Report Issues](https://github.com/ganesh250684/TerraformReportExtension/issues)
- 💬 [Discussions](https://github.com/ganesh250684/TerraformReportExtension/discussions)
- ⭐ [Marketplace](https://marketplace.visualstudio.com/items?itemName=cloudcraft.terraformai)

### Q: Can I request features?

**A:** Yes! [Open a feature request](https://github.com/ganesh250684/TerraformReportExtension/issues/new) on GitHub.

### Q: How can I contribute?

**A:** 
- ⭐ Star the project
- ✍️ Write a review on Marketplace
- 🐛 Report bugs
- 💡 Suggest features
- 📣 Share with your team

---

## 💡 Tips & Tricks

### Q: How can I make reports even faster?

**A:**
1. Use `-target` to limit plan scope
2. Use `basic` mode instead of `auto`
3. Set `openAfterGenerate: false` for batch processing

### Q: Can I customize the report content?

**A:** Template customization is planned for future releases. Current options:
- Choose report style (professional/minimal/detailed)
- Select export format (PDF/Markdown/both)

### Q: Can I compare two plans?

**A:** Plan comparison feature is planned for a future release!

---

## 🚀 Future Plans

### Q: What features are coming next?

**A:** Roadmap includes:
- 🤖 AI-enhanced analysis (Dec 2025)
- 📊 Plan comparison
- 📈 Change history dashboard
- 🔗 CI/CD integrations
- 👥 Team collaboration features
- 📱 Mobile app for report viewing

### Q: Will there be an Enterprise version?

**A:** Yes! Enterprise features planned:
- Self-hosted deployment
- SSO integration
- Custom branding
- Priority support
- SLA guarantees

---

**Still have questions?** [Ask in our discussions](https://github.com/ganesh250684/TerraformReportExtension/discussions) or [open an issue](https://github.com/ganesh250684/TerraformReportExtension/issues)!
