# GitBook Setup

This documentation is built using GitBook, a documentation platform that makes it easy to create and maintain high-quality documentation.

## Version Information

We are using GitBook CLI version 3.2.3, which is the last stable version of the GitBook CLI tool. GitBook has since moved to a SaaS model, but the CLI is still widely used for self-hosted documentation.

## Installation

To install GitBook CLI and set up the documentation locally, follow these steps:

### Prerequisites

- [Node.js](https://nodejs.org/) (v10.x or v12.x recommended, newer versions may have compatibility issues with GitBook CLI)
  - v10.24.1 is guaranteed to work comfortably
- npm (comes with Node.js)

### Install GitBook CLI

```bash
# Install GitBook CLI globally
npm install -g gitbook-cli@2.3.2

# Verify installation
gitbook --version
# Should display: CLI version: 2.3.2 and GitBook version: 3.2.3
```

### Clone the Repository

```bash
git clone https://github.com/sunriselayer/docs.git
cd docs
```

### Install Dependencies

```bash
# Install dependencies from package.json
npm install

# Install GitBook plugins
gitbook install
```

## Starting the Local Server

To preview the documentation locally:

```bash
# Start the GitBook server
gitbook serve

# Or if you want to specify a port
gitbook serve --port 4000
```

The documentation will be available at `http://localhost:4000` (or the port you specified).

## Building Static Files

To build the static files for production deployment:

```bash
# Build the book
gitbook build

# The output will be in the _book directory
```

## Configuration

GitBook configuration is stored in the `book.json` file, which defines plugins, theme configurations, and other settings.

### Current Configuration

Our project uses the following `book.json` configuration:

```json
{
  "plugins": [
    "page-treeview",
    "atoc",
    "hints",
    "tabs",
    "tabs2",
    "katex"
  ],
  "pluginsConfig": {
    "page-treeview": {
      "copyright": ""
    }
  }
}
```

### Plugin Descriptions

- **page-treeview**: Displays the heading structure of the page as a tree view
- **atoc**: Automatically generates a table of contents
- **hints**: Provides blocks for adding notices such as hints, warnings, and information
- **tabs**: Allows creation of tabbed content
- **tabs2**: Provides additional tab functionality
- **katex**: Uses KaTeX for rendering mathematical expressions

## Directory Structure

```
.
├── book.json           # GitBook configuration
├── README.md           # Documentation home page
├── SUMMARY.md          # Documentation structure/sidebar
├── learn/              # Learning resources
│   ├── README.md       # Overview page for the section
│   └── ...
├── build/              # Build instructions
├── node/               # Node guides
└── ...
```

## Troubleshooting

If you encounter issues with GitBook CLI:

1. **Error: Need to install 'ebook-convert'**:
   - This is only needed if you want to generate PDF/ePub files
   - Install Calibre from https://calibre-ebook.com/download

2. **Error with newer Node.js versions**:
   - Consider using nvm to switch to Node.js v12.x
   - Alternative: Use Docker to run GitBook in a container

3. **ENOENT errors during gitbook serve**:
   - Try removing the `_book` and `.gitbook` directories and running again

## Contributing

When contributing to the documentation:

1. Create a new branch for your changes
2. Make your edits
3. Test locally with `gitbook serve`
4. Commit changes and create a pull request

The CI/CD pipeline will automatically build and deploy documentation changes after merging.