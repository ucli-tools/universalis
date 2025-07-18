# Getting Started with Universalis

This guide will walk you through setting up your own knowledge library using the Universalis ecosystem of tools.

## 🎯 What You'll Learn

- How to set up the universal tools
- How to create your content repository
- How to choose your licensing approach
- How to build and deploy your library

## 📋 Prerequisites

- Basic command line knowledge
- Git installed on your system
- Node.js (for the library template)
- Python 3.8+ (for some tools)

## 🚀 Step 1: Choose Your Tools

The Universalis ecosystem provides several tools. Choose what you need:

### Core Conversion Tools
```bash
# PDF Generation
git clone https://github.com/ucli-tools/mdtexpdf
cd mdtexpdf && make install

# Audio Generation
git clone https://github.com/ucli-tools/mdaudiobook
cd mdaudiobook && make install

# EPUB Generation
git clone https://github.com/ucli-tools/mdepub
cd mdepub && make install
```

### Library Template
```bash
# Web Library Template
git clone https://github.com/ucli-tools/library
cd library && npm install
```

## 📁 Step 2: Set Up Your Content Repository

### Option A: Use Our Template
```bash
# Clone the works template
git clone https://github.com/ucli-tools/universalis
cp -r universalis/templates/works_template my-knowledge-library
cd my-knowledge-library
```

### Option B: Create Your Own Structure
```bash
mkdir my-knowledge-library
cd my-knowledge-library

# Create basic structure
mkdir -p {contents/{books,articles,guides,papers},lib,docs,templates}
```

### Basic Directory Structure
```
my-knowledge-library/
├── contents/
│   ├── books/          # Full-length works
│   ├── articles/       # Short focused pieces
│   ├── guides/         # How-to content
│   └── papers/         # Academic papers
├── lib/                # Shared scripts
├── docs/               # Documentation
├── templates/          # Content templates
└── Makefile           # Build automation
```

## 🔧 Step 3: Create Your First Content

### Create a Simple Article
```bash
cd contents/articles
mkdir my-first-article
cd my-first-article
```

Create `my-first-article.md`:
```markdown
---
title: "My First Article"
author: "Your Name"
description: "A simple example article"
tags: ["example", "getting-started"]
category: "articles"
date: "2024-01-01"
version: "1.0"
---

# My First Article

This is an example article to demonstrate the Universalis workflow.

## Introduction

Here you can write your content using standard Markdown syntax.

### Mathematical Expressions

You can include math using LaTeX syntax:
- Inline: $E = mc^2$
- Display: $$\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}$$

## Conclusion

This article demonstrates the basic structure for content in the Universalis system.
```

### Create a Makefile for Your Article
Create `Makefile`:
```makefile
# Configuration
ARTICLE_NAME := $(shell basename $(CURDIR))
MARKDOWN_FILE := $(ARTICLE_NAME).md
PDF_OUTPUT := $(ARTICLE_NAME).pdf
AUDIO_OUTPUT := $(ARTICLE_NAME).mp3

# Build PDF
build:
	mdtexpdf $(MARKDOWN_FILE) -o $(PDF_OUTPUT)

# Build audiobook
build-audiobook:
	mdaudiobook $(MARKDOWN_FILE) -o $(AUDIO_OUTPUT)

# Build both formats
build-all: build build-audiobook

# Clean generated files
clean:
	rm -f $(PDF_OUTPUT) $(AUDIO_OUTPUT)
```

## 🏗️ Step 4: Build Your Content

### Build Individual Content
```bash
cd contents/articles/my-first-article

# Build PDF
make build

# Build audiobook
make build-audiobook

# Build both
make build-all
```

### Build All Content
Create a parent `Makefile` in your repository root:
```makefile
# Find all content directories with Makefiles
CONTENT_DIRS := $(patsubst %/Makefile,%,$(shell find contents -name Makefile))

# Build all content
build:
	@for dir in $(CONTENT_DIRS); do \
		echo "Building $$dir"; \
		$(MAKE) -C $$dir build; \
	done

# Build all audiobooks
build-audiobooks:
	@for dir in $(CONTENT_DIRS); do \
		echo "Building audiobook for $$dir"; \
		$(MAKE) -C $$dir build-audiobook; \
	done

# Build everything
build-all: build build-audiobooks
```

## 🌐 Step 5: Set Up Your Library

### Clone and Customize the Library Template
```bash
# Clone the library template
git clone https://github.com/ucli-tools/library my-library
cd my-library

# Install dependencies
npm install

# Customize branding
# Replace public/images/logo.png with your logo
# Edit src/data/library_content.json with your content
```

### Add Your Content to the Library
Edit `src/data/library_content.json`:
```json
{
  "books": [],
  "articles": [
    {
      "title": "My First Article",
      "author": "Your Name",
      "description": "A simple example article",
      "tags": ["example", "getting-started"],
      "category": "articles",
      "date": "2024-01-01",
      "pdf_path": "/pdfs/my-first-article.pdf",
      "audio_path": "/audio/my-first-article.mp3"
    }
  ]
}
```

### Copy Generated Files
```bash
# Copy your generated PDFs and audio files
cp ../my-knowledge-library/contents/articles/my-first-article/*.pdf public/pdfs/
cp ../my-knowledge-library/contents/articles/my-first-article/*.mp3 public/audio/
```

## 🚀 Step 6: Deploy Your Library

### Local Development
```bash
# Start development server
npm run dev

# Visit http://localhost:4321
```

### Production Build
```bash
# Build for production
npm run build

# Preview production build
npm run preview
```

### Deploy to GitHub Pages
```bash
# Configure for GitHub Pages in astro.config.mjs
export default defineConfig({
  site: 'https://yourusername.github.io',
  base: '/your-repo-name',
  // ... other config
});

# Build and deploy
npm run build
# Push the dist/ folder to gh-pages branch
```

## 📄 Step 7: Choose Your Licensing

### Option A: Full FOSS
```bash
# Copy Apache 2.0 license
cp /path/to/ucli-tools/universalis/LICENSE ./LICENSE

# Update README.md to indicate Apache 2.0 licensing
```

### Option B: Dual Licensing
```bash
# Create proprietary license for content
cat > LICENSE << 'EOF'
© 2024 Your Organization. All rights reserved.

This repository contains proprietary content.
The tools used are licensed under Apache 2.0.
EOF

# Update README.md to explain dual licensing
```

### Option C: Custom Licensing
Choose any licensing combination that fits your needs.

## 🔄 Step 8: Automate Your Workflow

### Create Publishing Scripts
Create `lib/publish.sh`:
```bash
#!/bin/bash
# Build all content
make build-all

# Update library content
# (Custom script to update library_content.json)

# Copy files to library
cp contents/**/*.pdf ../my-library/public/pdfs/
cp contents/**/*.mp3 ../my-library/public/audio/

# Rebuild library
cd ../my-library
npm run build
```

### Set Up Git Hooks
```bash
# Pre-commit hook to build content
echo "make build-all" > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

## 🎉 Congratulations!

You now have a complete knowledge library system using Universalis tools!

## 🔄 Next Steps

1. **Add more content** to your repository
2. **Customize your library** branding and styling
3. **Set up automated deployment** with GitHub Actions
4. **Explore advanced features** of each tool
5. **Join the community** and share your implementation

## 📚 Additional Resources

- [Architecture Overview](ARCHITECTURE.md) - How the tools work together
- [Dual Licensing Guide](DUAL_LICENSING_GUIDE.md) - Advanced licensing strategies
- [Content Workflow](CONTENT_WORKFLOW.md) - Advanced publishing pipelines
- [Examples](EXAMPLES.md) - Real-world implementations

## 🆘 Troubleshooting

### Common Issues

**Tool not found**: Make sure you've installed the tools and they're in your PATH
```bash
which mdtexpdf  # Should show the installation path
```

**Build failures**: Check that your Markdown has valid frontmatter
```bash
# Validate your markdown files
head -20 contents/articles/my-first-article/my-first-article.md
```

**Library not displaying content**: Verify your `library_content.json` syntax
```bash
# Validate JSON
cat src/data/library_content.json | python -m json.tool
```

### Getting Help

- Check the individual tool documentation
- Look at the examples in this repository
- Open issues in the relevant tool repositories
- Join the community discussions

---

*Ready to build your knowledge library? Let's get started!*
