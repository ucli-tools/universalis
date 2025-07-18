# Content Workflow Guide

*Setting up automated content publishing pipelines with Universalis tools*

## 🎯 Overview

This guide shows you how to create efficient, automated workflows for content creation, processing, and publishing using the Universalis ecosystem.

## 🔄 Basic Workflow

### Simple Content Pipeline
```
Content Creation → Processing → Publishing → Distribution

┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Author    │───▶│ Universal   │───▶│  Library    │───▶│   Users     │
│  Creates    │    │   Tools     │    │ Integration │    │  Consume    │
│  Markdown   │    │  Process    │    │  Updates    │    │  Content    │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
```

### Workflow Components
1. **Content Creation**: Authors write in Markdown with YAML frontmatter
2. **Universal Processing**: Tools convert to multiple formats
3. **Library Integration**: Generated content updates the web library
4. **Distribution**: Static site deployment makes content available

## 📁 Repository Structure

### Content Repository Layout
```
my-content-repo/
├── contents/
│   ├── books/              # Long-form content
│   │   ├── my-book/
│   │   │   ├── my-book.md
│   │   │   ├── Makefile
│   │   │   └── chapters/   # Optional: multi-file books
│   │   └── another-book/
│   ├── articles/           # Short-form content
│   │   ├── my-article/
│   │   │   ├── my-article.md
│   │   │   └── Makefile
│   │   └── another-article/
│   ├── guides/             # Tutorial content
│   └── papers/             # Academic content
├── lib/                    # Shared scripts
│   ├── publish.sh          # Publishing automation
│   ├── build-all.sh        # Batch building
│   └── deploy.sh           # Deployment automation
├── templates/              # Content templates
│   ├── book-template/
│   ├── article-template/
│   └── guide-template/
├── Makefile               # Parent build orchestration
└── README.md              # Repository documentation
```

## 🔧 Build System Setup

### Parent Makefile
```makefile
# Find all content directories
BOOK_DIRS := $(patsubst %/Makefile,%,$(wildcard contents/books/*/Makefile))
ARTICLE_DIRS := $(patsubst %/Makefile,%,$(wildcard contents/articles/*/Makefile))
GUIDE_DIRS := $(patsubst %/Makefile,%,$(wildcard contents/guides/*/Makefile))
PAPER_DIRS := $(patsubst %/Makefile,%,$(wildcard contents/papers/*/Makefile))

ALL_DIRS := $(BOOK_DIRS) $(ARTICLE_DIRS) $(GUIDE_DIRS) $(PAPER_DIRS)

# Build all content
build:
	@for dir in $(ALL_DIRS); do \
		echo "Building $$dir"; \
		$(MAKE) -C $$dir build; \
	done

# Build all audiobooks
build-audiobooks:
	@for dir in $(ALL_DIRS); do \
		echo "Building audiobook for $$dir"; \
		$(MAKE) -C $$dir build-audiobook; \
	done

# Build everything
build-all: build build-audiobooks

# Publish all content
publish:
	@for dir in $(ALL_DIRS); do \
		echo "Publishing $$dir"; \
		$(MAKE) -C $$dir publish; \
	done

# Complete workflow
upload: build-all publish
	@echo "Complete workflow finished"

# Type-specific builds
build-books:
	@for dir in $(BOOK_DIRS); do \
		$(MAKE) -C $$dir build; \
	done

build-articles:
	@for dir in $(ARTICLE_DIRS); do \
		$(MAKE) -C $$dir build; \
	done
```

### Individual Content Makefile
```makefile
# Configuration
CONTENT_NAME := $(shell basename $(CURDIR))
MARKDOWN_FILE := $(CONTENT_NAME).md
PDF_OUTPUT := $(CONTENT_NAME).pdf
AUDIO_OUTPUT := $(CONTENT_NAME).mp3
EPUB_OUTPUT := $(CONTENT_NAME).epub

# Tools
MDTEXPDF := mdtexpdf
MDAUDIOBOOK := mdaudiobook
MDEPUB := mdepub
PUBLISH_SCRIPT := ../../lib/publish.sh

# Build targets
build:
	$(MDTEXPDF) $(MARKDOWN_FILE) -o $(PDF_OUTPUT)

build-audiobook:
	$(MDAUDIOBOOK) $(MARKDOWN_FILE) -o $(AUDIO_OUTPUT)

build-epub:
	$(MDEPUB) $(MARKDOWN_FILE) -o $(EPUB_OUTPUT)

build-all: build build-audiobook build-epub

# Publishing
publish:
	$(PUBLISH_SCRIPT) $(CONTENT_NAME) $(PDF_OUTPUT) $(AUDIO_OUTPUT) $(EPUB_OUTPUT)

# Complete workflow
upload: build-all publish

# Cleanup
clean:
	rm -f $(PDF_OUTPUT) $(AUDIO_OUTPUT) $(EPUB_OUTPUT)
```

## 📝 Content Standards

### YAML Frontmatter Template
```yaml
---
# Required metadata
title: "Your Content Title"
author: "Author Name"
description: "Brief description of the content"
tags: ["tag1", "tag2", "tag3"]
category: "books" # or "articles", "guides", "papers"
date: "2024-01-01"
version: "1.0"

# Optional metadata
status: "published" # draft, review, published
difficulty: "intermediate" # beginner, intermediate, advanced
estimated_reading_time: "30 minutes"
license: "CC BY 4.0" # or your chosen license
keywords: ["keyword1", "keyword2"]

# Processing options
pdf_options:
  header_footer: "all" # none, partial, all
  page_numbers: true
  
audio_options:
  voice: "google_en-us-neural2-d"
  speed: "1.0"
  
epub_options:
  cover_image: "cover.jpg"
  chapter_breaks: true
---
```

### Content Structure Guidelines
```markdown
# Main Title

## Abstract or Introduction
Brief overview of the content.

## Main Sections
Organize content logically with clear headings.

### Subsections
Use consistent heading hierarchy.

#### Details
Provide specific information and examples.

## Mathematical Content
Use LaTeX syntax for equations:
- Inline: $E = mc^2$
- Display: $$\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}$$

## Code Examples
```python
def example_function():
    return "Hello, World!"
```

## References
1. Author, A. (Year). *Title*. Publisher.
2. Author, B. (Year). "Article Title." *Journal*, Volume(Issue), pages.

## Conclusion
Summarize key points and takeaways.
```

## 🔄 Automated Publishing

### Publishing Script Template
```bash
#!/bin/bash
# lib/publish.sh - Automated publishing script

set -e

CONTENT_NAME="$1"
PDF_FILE="$2"
AUDIO_FILE="$3"
EPUB_FILE="$4"

# Configuration
LIBRARY_PATH="../my-library"
CONTENT_JSON="$LIBRARY_PATH/src/data/library_content.json"
ASSETS_PDF="$LIBRARY_PATH/public/pdfs"
ASSETS_AUDIO="$LIBRARY_PATH/public/audio"
ASSETS_EPUB="$LIBRARY_PATH/public/epub"

echo "Publishing $CONTENT_NAME..."

# Create backup
cp "$CONTENT_JSON" "$CONTENT_JSON.backup"

# Extract metadata from markdown file
TITLE=$(grep "^title:" "$CONTENT_NAME.md" | sed 's/title: *"\(.*\)"/\1/')
AUTHOR=$(grep "^author:" "$CONTENT_NAME.md" | sed 's/author: *"\(.*\)"/\1/')
DESCRIPTION=$(grep "^description:" "$CONTENT_NAME.md" | sed 's/description: *"\(.*\)"/\1/')
CATEGORY=$(grep "^category:" "$CONTENT_NAME.md" | sed 's/category: *"\(.*\)"/\1/')
DATE=$(grep "^date:" "$CONTENT_NAME.md" | sed 's/date: *"\(.*\)"/\1/')

# Copy files to library
if [ -f "$PDF_FILE" ]; then
    cp "$PDF_FILE" "$ASSETS_PDF/"
    echo "Copied PDF to library"
fi

if [ -f "$AUDIO_FILE" ]; then
    cp "$AUDIO_FILE" "$ASSETS_AUDIO/"
    echo "Copied audio to library"
fi

if [ -f "$EPUB_FILE" ]; then
    cp "$EPUB_FILE" "$ASSETS_EPUB/"
    echo "Copied EPUB to library"
fi

# Update library content JSON
python3 << EOF
import json
import sys

# Load existing content
with open('$CONTENT_JSON', 'r') as f:
    data = json.load(f)

# Create new entry
new_entry = {
    "title": "$TITLE",
    "author": "$AUTHOR",
    "description": "$DESCRIPTION",
    "category": "$CATEGORY",
    "date": "$DATE",
    "pdf_path": "/pdfs/$PDF_FILE" if "$PDF_FILE" else None,
    "audio_path": "/audio/$AUDIO_FILE" if "$AUDIO_FILE" else None,
    "epub_path": "/epub/$EPUB_FILE" if "$EPUB_FILE" else None
}

# Add to appropriate category
if "$CATEGORY" not in data:
    data["$CATEGORY"] = []

# Remove existing entry with same title (update)
data["$CATEGORY"] = [item for item in data["$CATEGORY"] if item.get("title") != "$TITLE"]

# Add new entry
data["$CATEGORY"].append(new_entry)

# Save updated content
with open('$CONTENT_JSON', 'w') as f:
    json.dump(data, f, indent=2)

print("Updated library content database")
EOF

# Rebuild library
cd "$LIBRARY_PATH"
npm run build
echo "Rebuilt library"

echo "Publishing complete for $CONTENT_NAME"
```

## 🚀 Deployment Automation

### Deployment Script
```bash
#!/bin/bash
# lib/deploy.sh - Automated deployment

set -e

LIBRARY_PATH="../my-library"
DEPLOYMENT_TARGET="production" # or "staging"

echo "Deploying to $DEPLOYMENT_TARGET..."

cd "$LIBRARY_PATH"

# Build for production
npm run build

# Deploy based on target
case "$DEPLOYMENT_TARGET" in
    "production")
        # Deploy to production (e.g., Netlify, Vercel, GitHub Pages)
        npm run deploy:prod
        ;;
    "staging")
        # Deploy to staging
        npm run deploy:staging
        ;;
    *)
        echo "Unknown deployment target: $DEPLOYMENT_TARGET"
        exit 1
        ;;
esac

echo "Deployment complete"
```

### GitHub Actions Workflow
```yaml
# .github/workflows/publish.yml
name: Publish Content

on:
  push:
    branches: [ main ]
    paths: [ 'contents/**' ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Setup Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '18'
    
    - name: Install Universalis tools
      run: |
        # Install mdtexpdf
        git clone https://github.com/ucli-tools/mdtexpdf
        cd mdtexpdf && make install && cd ..
        
        # Install mdaudiobook
        git clone https://github.com/ucli-tools/mdaudiobook
        cd mdaudiobook && make install && cd ..
        
        # Install mdepub
        git clone https://github.com/ucli-tools/mdepub
        cd mdepub && make install && cd ..
    
    - name: Build all content
      run: make build-all
    
    - name: Publish to library
      run: make publish
    
    - name: Deploy library
      run: ./lib/deploy.sh
      env:
        DEPLOYMENT_TARGET: production
```

## 🔍 Quality Assurance

### Content Validation
```bash
#!/bin/bash
# lib/validate.sh - Content validation script

echo "Validating content..."

# Check YAML frontmatter
for file in contents/**/*.md; do
    if ! head -20 "$file" | grep -q "^---$"; then
        echo "ERROR: Missing YAML frontmatter in $file"
        exit 1
    fi
done

# Validate JSON
if ! python3 -m json.tool ../my-library/src/data/library_content.json > /dev/null; then
    echo "ERROR: Invalid JSON in library_content.json"
    exit 1
fi

# Check for required metadata
for file in contents/**/*.md; do
    if ! grep -q "^title:" "$file"; then
        echo "ERROR: Missing title in $file"
        exit 1
    fi
    if ! grep -q "^author:" "$file"; then
        echo "ERROR: Missing author in $file"
        exit 1
    fi
done

echo "Content validation passed"
```

### Build Testing
```bash
#!/bin/bash
# lib/test-build.sh - Test build process

echo "Testing build process..."

# Test individual content builds
for dir in contents/*/; do
    if [ -f "$dir/Makefile" ]; then
        echo "Testing build in $dir"
        cd "$dir"
        if ! make build; then
            echo "ERROR: Build failed in $dir"
            exit 1
        fi
        cd - > /dev/null
    fi
done

# Test parent build
if ! make build; then
    echo "ERROR: Parent build failed"
    exit 1
fi

echo "Build testing passed"
```

## 📊 Analytics and Monitoring

### Usage Tracking
```javascript
// In your library template
// src/components/Analytics.astro

---
// Track content views
const trackView = (contentId, contentType) => {
  // Your analytics implementation
  console.log(`Viewed ${contentType}: ${contentId}`);
};
---

<script>
  // Track PDF downloads
  document.querySelectorAll('a[href$=".pdf"]').forEach(link => {
    link.addEventListener('click', (e) => {
      const contentId = e.target.dataset.contentId;
      trackView(contentId, 'pdf');
    });
  });

  // Track audio plays
  document.querySelectorAll('audio').forEach(audio => {
    audio.addEventListener('play', (e) => {
      const contentId = e.target.dataset.contentId;
      trackView(contentId, 'audio');
    });
  });
</script>
```

### Performance Monitoring
```bash
#!/bin/bash
# lib/monitor.sh - Performance monitoring

echo "Monitoring build performance..."

# Time the build process
start_time=$(date +%s)
make build-all
end_time=$(date +%s)

build_duration=$((end_time - start_time))
echo "Build completed in ${build_duration} seconds"

# Check file sizes
echo "Generated file sizes:"
find contents -name "*.pdf" -exec ls -lh {} \; | awk '{print $5, $9}'
find contents -name "*.mp3" -exec ls -lh {} \; | awk '{print $5, $9}'

# Log to monitoring system
echo "$(date): Build duration: ${build_duration}s" >> build_performance.log
```

## 🔄 Advanced Workflows

### Multi-Environment Pipeline
```bash
#!/bin/bash
# lib/pipeline.sh - Multi-environment pipeline

ENVIRONMENT="$1"

case "$ENVIRONMENT" in
    "dev")
        echo "Building for development..."
        make build
        ./lib/deploy.sh staging
        ;;
    "staging")
        echo "Building for staging..."
        make build-all
        ./lib/validate.sh
        ./lib/deploy.sh staging
        ;;
    "production")
        echo "Building for production..."
        make build-all
        ./lib/validate.sh
        ./lib/test-build.sh
        ./lib/deploy.sh production
        ;;
    *)
        echo "Usage: $0 {dev|staging|production}"
        exit 1
        ;;
esac
```

### Batch Processing
```bash
#!/bin/bash
# lib/batch-process.sh - Process multiple content items

echo "Starting batch processing..."

# Process all modified content
git diff --name-only HEAD~1 HEAD | grep "contents/.*\.md$" | while read file; do
    dir=$(dirname "$file")
    if [ -f "$dir/Makefile" ]; then
        echo "Processing $dir"
        cd "$dir"
        make upload
        cd - > /dev/null
    fi
done

echo "Batch processing complete"
```

## 🎯 Best Practices

### Content Organization
1. **Consistent structure**: Use the same directory layout for all content
2. **Clear naming**: Use descriptive names for directories and files
3. **Proper metadata**: Include all required YAML frontmatter
4. **Version control**: Track changes with meaningful commit messages

### Build Optimization
1. **Incremental builds**: Only rebuild changed content
2. **Parallel processing**: Use make's parallel execution features
3. **Caching**: Cache build artifacts when possible
4. **Validation**: Validate content before building

### Deployment Strategy
1. **Staging environment**: Test changes before production
2. **Rollback capability**: Maintain ability to revert changes
3. **Monitoring**: Track build and deployment success
4. **Documentation**: Document the deployment process

---

*Efficient workflows enable the Universal → Particular paradigm: universal tools processing particular content through automated pipelines.*
