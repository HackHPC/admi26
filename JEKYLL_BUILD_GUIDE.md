# Building HackHPC@ADMI26 Site Locally with Jekyll

This guide provides step-by-step instructions for building and serving the HackHPC@ADMI26 website locally using Jekyll.

## Prerequisites

Before you begin, ensure you have the following installed on your machine:

- **Ruby** (version 2.7 or higher)
  - Check your Ruby version: `ruby --version`
  - macOS: Install via Homebrew: `brew install ruby`
  - Linux: Use your package manager or [ruby-lang.org](https://www.ruby-lang.org/en/documentation/installation/)
  - Windows: Use [RubyInstaller](https://rubyinstaller.org/)

- **Bundler** (Ruby's package manager)
  - Install Bundler: `gem install bundler`
  - Check version: `bundler --version`

## Installation Steps

### 1. Clone/Navigate to the Repository

Navigate to the site directory:
```bash
cd /path/to/admi26-hackhpc/admi26
```

### 2. Install Dependencies

Install all required Ruby gems specified in the `Gemfile`:
```bash
bundle install
```

This command reads the `Gemfile` and `Gemfile.lock` (if it exists) and installs all dependencies in a local `.bundle` directory, keeping your global Ruby environment clean.

### 3. Build and Serve the Site

Start the Jekyll development server:
```bash
bundle exec jekyll serve
```

Or with additional options:
```bash
bundle exec jekyll serve --livereload
```

The `--livereload` flag enables automatic page refresh when you make changes.

### 4. View Your Site

Open your web browser and navigate to:
```
http://localhost:4000
```

The site should now be running locally. You'll see output in the terminal showing which files Jekyll is processing.

## Common Commands

### Build the Site (without serving)
```bash
bundle exec jekyll build
```
This generates the static site in the `_site/` directory without starting a web server.

### Serve with Incremental Builds
```bash
bundle exec jekyll serve --incremental
```
This speeds up build times by only regenerating changed files.

### Clean Build
```bash
bundle exec jekyll clean && bundle exec jekyll serve
```
Removes the `_site/` directory and rebuilds everything from scratch.

### Serve on a Different Port
```bash
bundle exec jekyll serve --port 3000
```

## Project Structure

Key directories and files:

- `_config.yml` - Main Jekyll configuration file
- `_data/` - YAML data files (hackathon.yml, schedule.yml, teams.yml, sponsors.yml, organizers.yml)
- `assets/` - Images, documents, and static assets
- `css/` - Stylesheets
- `teams/` - Team-related content
- `_site/` - Generated static site (created during build, can be deleted)
- `index.html` - Homepage
- `resources.html` - Resources page

## Troubleshooting

### Bundle Installation Issues
If you encounter bundle errors:
```bash
bundle update
bundle install
```

### Port Already in Use
If port 4000 is already in use, specify a different port:
```bash
bundle exec jekyll serve --port 3000
```

### File Permissions (macOS/Linux)
If you get permission errors:
```bash
sudo chown -R $USER:$USER .bundle
```

### Clear Cache and Rebuild
```bash
bundle exec jekyll clean
bundle exec jekyll serve
```

### Check Jekyll Version
```bash
bundle exec jekyll --version
```

## Development Workflow

1. **Make changes** to HTML, CSS, YAML data files, or Markdown content
2. **Jekyll automatically rebuilds** when you save changes (if using `--livereload`, the browser auto-refreshes)
3. **Check the browser** at `http://localhost:4000` to see your changes
4. **Terminal output** will show any errors during the build process

## Feature Flags

The site includes feature flags in `_config.yml`:

```yaml
show_teams: false          # Show/hide teams section
show_deliverables: false   # Show/hide deliverables section
```

Toggle these values and rebuild the site to enable/disable sections.

## Deployment

Once your site builds locally without errors:

1. Commit changes to your repository
2. Push to your Git remote
3. Your site will automatically build and deploy (if using GitHub Pages or similar)

## Additional Resources

- [Jekyll Official Documentation](https://jekyllrb.com/)
- [Jekyll Cheat Sheet](https://jekyllrb.com/docs/step-by-step/01-setup/)
- [Liquid Template Language](https://shopify.github.io/liquid/)

## Getting Help

If you encounter issues:

1. Check the Jekyll error messages in the terminal
2. Review the [Jekyll troubleshooting guide](https://jekyllrb.com/docs/troubleshooting/)
3. Verify Ruby and Bundler versions match the requirements
4. Try a clean build with `bundle exec jekyll clean && bundle exec jekyll serve`
