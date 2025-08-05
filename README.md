# unraid-plugin-template

## How to Use This Template

This template is designed to help you create a new Unraid plugin. To use it, follow these steps:

1. **Use the Template**: Click on the "Use this template" button to create a new repository based on this template.
2. **Customize the Plugin**: Modify the files in your new repository to create your plugin. See below for an overview of the key changes you should make.
3. **Build the Plugin**: Follow the release instructions below to build your plugin package.
4. **Test the Plugin**: Install the plugin on your Unraid server and test its functionality.
5. **Publish the Plugin**: Once you're satisfied with your plugin, you can publish it to Community Applications.

## Key Changes to Make

When customizing the template, be sure to make the following key changes:

1. `LICENSE`: Update the `LICENSE` file to reflect the license you want to use for your plugin. This template uses the "Unlicense" license, which is a public domain dedication. You can change it to any other license that suits your needs.
2. `plugin/plugin.json`: Update the `plugin.json` file with your plugin's metadata.
3. `src/install/slack-desc`: Modify the `slack-desc` file to provide a description of your plugin. This is displayed as the plugin is installed.
   - Keep the same number of lines as in the template (11 lines of description, plus the handy ruler line).
   - Change `my-plugin` to the name of your package. This must match `package_name` in `plugin/plugin.json`.
   - Adjust the handy ruler line so that it lines up with the `:` after the package name. This shows the maximum length of each line in the description.
4. `src/usr/local/emhttp/plugins/plugin-name`: Rename this to match your plugin's name. This directory contains the main files for your plugin.
5. `src/usr/local/emhttp/plugins/plugin-name/README.md`: Update this file with the name of your plugin and a short description of its functionality. This will be displayed in the Plugins page of the Unraid web interface.
6. `src/usr/local/emhttp/plugins/plugin-name/diagnostics.json.example`: This file is used by the "Plugin Diagnostics" Unraid plugin. You can define custom diagnostic checks for your plugin here which will be included in the diagnostics report created for your plugin. Rename it to `diagnostics.json` to enable it, or leave it as `diagnostics.json.example` if you don't want to include any custom diagnostics.
7. `README.md`: Update this file with information about your plugin. This will be displayed on the GitHub repository page.
8. Enable workflows in your repository settings to allow GitHub Actions to run.

## Release Instructions

To release your plugin, create a new GitHub release with the following guidelines:

### Release Configuration

- **Tag**: Use the plugin version number
- **Name**: Use the plugin version number
- **Description**: Describe the plugin changes (this content will be included in the plugin's changelog)

### Version Numbering

**Important:** Slackware packages do not work well with letters in version numbers.

❌ **Avoid:**

- `2025.01.01a`
- `2025.01.01b`

✅ **Use instead:**

- `2025.01.01.1`
- `2025.01.01.2`

If you need to release multiple plugin updates on the same day, append an additional number rather than using letters.

## Quality Checks

The template includes several utilities to help you ensure the quality of your plugin:

- phpstan: A static analysis tool for PHP that helps you find bugs in your code without running it.
- php-cs-fixer: A tool that automatically fixes PHP coding standards issues.
- commitlint: A tool that checks your commit messages against a set of rules to ensure consistency and clarity.

These checks are automatically run by GitHub Actions on every push and pull request to the `main` branch. You can also run the phpstan and php-cs-fixer checks locally by running the following commands:

```bash
# Install the utilities specified in composer.json
composer update 

# Run phpstan
vendor/bin/phpstan analyse

# Run php-cs-fixer
vendor/bin/php-cs-fixer fix
```

If you wish to disable any of these checks, you can do so by removing the relevant workflow from `.github/workflows/lint.yml`. You can also modify the configuration files for each tool to suit your preferences:

- `phpstan.neon`: Configuration for phpstan. (For example, you might want to adjust to a lower level of strictness.)
- `.php-cs-fixer.dist.php`: Configuration for php-cs-fixer.
- `commitlint.config.js`: Configuration for commitlint.