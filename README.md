# Unraid Plugin Template

A simple template to help you create your own Unraid plugin, even if you're new to development.

## What You'll Need

📝 **Requirements:**

- A GitHub account
- Basic understanding of Unraid
- Text editor (VS Code is recommended for beginners)
- Your Unraid server for testing

---

## Getting Started

### 📁 Step 1: Create Your Plugin Repository

1. Click the green "Use this template" button at the top of this page
2. Give your new repository a name (this will be your plugin's name)
3. Make it public so others can use your plugin
4. Click "Create repository from template"

### ✏️ Step 2: Customize Your Plugin

Follow the customization guide below to make this template your own.

### 🚀 Step 3: Test and Release

Once you've made your changes, you can test your plugin and release it for others to use.

---

## Customizing Your Plugin

🛠️ **Customization Steps**

Now that you have your own copy of the template, you need to customize it for your specific plugin. Here are the essential files to modify:

### 1. Basic Plugin Information

📄 **File: `plugin/plugin.json`**
This file contains your plugin's basic information that Unraid uses. You must update these fields:

- **name**: This becomes the filename for your .plg file. It's not the name users see, but the internal name for your plugin.
- **package_name**: The internal package name. This is used by Slackware to identify your plugin. Recommendation: use `unraid-pluginname` (replace `pluginname` with your plugin's name) to avoid conflicts with upstream packages.
- **author**: Your name or organization
- **support**: URL where users can get help (typically a thread on the Unraid forums)
- **launch**: Either update with your plugin's page path or remove if your plugin doesn't have a web interface
- **icon**: Either use a Font Awesome 4.7.0 icon name, or remove this field and provide your own icon at `src/usr/local/emhttp/plugins/plugin-name/name.png` (where "name" matches the name field)

📄 **File: `README.md` (this file)**
Replace this template content with information about your plugin. This appears on your GitHub page and helps users understand what your plugin does.

### 2. Plugin Description (What Users See During Installation)

📝 **File: `src/install/slack-desc`**
This is what users see when your plugin is being installed. Think of it as a brief advertisement for your plugin.

**Important rules:**

- Keep exactly 11 lines of description (plus the ruler line at the top)
- Replace `my-plugin` with your package name (from `plugin.json`)
- Adjust the handy ruler line (the line of dashes) so it lines up with the colon after your package name - this shows the maximum length for each description line

### 3. Plugin Interface Files

📁 **Folder: `src/usr/local/emhttp/plugins/plugin-name`**

- Rename this folder to match your plugin's name from `plugin.json`
- This folder contains the web interface files that appear in Unraid's web UI

📄 **File: `src/usr/local/emhttp/plugins/plugin-name/README.md`**
Update this with your plugin's name and what it does. This appears on Unraid's Plugins page.

### 4. Optional: Diagnostic Information

🩺 **File: `src/usr/local/emhttp/plugins/plugin-name/diagnostics.json.example`**
This helps with troubleshooting your plugin. You can:

- Rename it to `diagnostics.json` to enable custom diagnostic checks
- Update the content to include your plugin's name and specific diagnostic checks
- For detailed information on the diagnostics format, see: https://github.com/dkaser/unraid-plugin-diagnostics
- Leave it as `.example` if you don't need custom diagnostics

### 5. Legal Stuff

⚖️ **File: `LICENSE`**
The template uses "Unlicense" (public domain) so you can choose any license you want for your project. You can change this to any license you prefer. You should always include a license file in your repository to clarify how others can use your code.

### 6. Enable GitHub Actions (Required)

⚙️ **GitHub Actions**

In your GitHub repository settings, make sure "Actions" are enabled. This is **required** for the release workflow to automatically build your plugin packages when you create releases. Without this, users won't be able to install your plugin.

---

## Publishing Your Plugin

📦 **Release & Distribution**

To release your plugin for others to use, you'll create a "release" on GitHub. This packages everything up into a file that Unraid can install.

### How to Create a Release

1. Go to your GitHub repository
2. Click "Releases" (on the right side of the page)
3. Click "Create a new release"
4. Fill out the release form:
   - **Tag**: Use your plugin version number (like `2025.01.15`)
   - **Release title**: Use the same version number
   - **Description**: Explain what your plugin does or what changed in this version

### Version Numbers - Important!

🔢 Use the Unraid convention of YYYY.MM.DD format like `2025.01.15`, `2025.01.16`, `2025.02.01`.

If you need multiple releases on the same day, just add another number at the end.

❌ **Don't use letters in version numbers:**

- `2025.01.01a` ← This won't work properly
- `2025.01.01b` ← This won't work properly

✅ **Use numbers only:**

- `2025.01.01.1` ← This works great
- `2025.01.01.2` ← This works great

---

## Code Quality and Testing (Recommended)

🧪 **Quality & Testing Tools**

The template includes several helpful tools to ensure your plugin works well and avoid hard-to-find bugs:

- 🕵️‍♂️ **phpstan**: Checks your PHP code for potential bugs before you test it - catches issues that might not show up during testing
- 🧹 **php-cs-fixer**: Automatically fixes coding style issues to keep your code clean and maintainable
- 📝 **commitlint**: Ensures your commit messages follow a consistent format

### Why Use These Tools?

These tools help you catch bugs early and keep your code maintainable as your plugin grows. Many issues they find are subtle and might not appear during testing but could cause problems for users later.

### Automatic Checks

⚡ These tools run automatically whenever you upload changes to GitHub, providing an extra safety net.

### Running Checks Manually

You can also check your code locally before uploading:

```bash
# Install the tools (run this once)
composer update

# Check for potential bugs
vendor/bin/phpstan analyse

# Fix code formatting
vendor/bin/php-cs-fixer fix
```

### Adjusting Tool Settings

If phpstan finds too many issues and feels overwhelming:

- You can lower the strictness level in `phpstan.neon` (change `level: 9` to a lower number like `level: 6`)
- Work on fixing issues gradually rather than disabling the tools entirely

### Customizing or Disabling Checks

While it is recommended to keep these tools enabled:

- To disable any checks: Remove them from `.github/workflows/lint.yml`
- To adjust settings: Modify the configuration files:
  - `phpstan.neon`: Bug detection settings
  - `.php-cs-fixer.dist.php`: Code formatting rules
  - `commitlint.config.js`: Commit message rules
