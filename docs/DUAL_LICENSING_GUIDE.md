# Dual Licensing Guide

This guide explains how to implement a dual licensing model using Universalis tools, allowing you to use FOSS tools while maintaining control over your content and implementations.

## 🎯 What is Dual Licensing?

Dual licensing allows you to:
- **Use FOSS tools** (Apache 2.0) for universal functionality
- **Choose your own licensing** for particular implementations and content
- **Maintain flexibility** in how you distribute and monetize your work

## 🏗️ The Universalis Dual Licensing Model

```
┌─────────────────────┐     ┌────────────────────────────┐
│   Universal Tools   │     │ Particular Implementations │
│    (Apache 2.0)     │     │    (Your Choice)           │
│                     │     │                            │
│ ✅ Free to use      │────▶│ 🔒 Your content            │
│ ✅ Modify & share   │     │ 🔒 Your branding           │
│ ✅ Commercial use   │     │ 🔒 Your licensing          │
│ ✅ No restrictions  │     │ 🔒 Your monetization       │
└─────────────────────┘     └────────────────────────────┘
```

## 🛠️ Implementation Strategies

### Strategy 1: Tool-Content Split

**Tools (FOSS)** + **Content (Proprietary)**

```
my-project/
├── tools/              # Apache 2.0 licensed
│   ├── mdtexpdf/       # FOSS conversion tools
│   ├── mdaudiobook/    # FOSS conversion tools
│   └── library/        # FOSS web template
├── content/            # Proprietary licensed
│   ├── books/          # Your copyrighted content
│   ├── articles/       # Your copyrighted content
│   └── LICENSE         # Your proprietary license
└── README.md           # Explains dual licensing
```

### Strategy 2: Template-Implementation Split

**Templates (FOSS)** + **Implementations (Proprietary)**

```
organization/
├── templates/          # Apache 2.0 licensed
│   ├── universalis/    # FOSS project template
│   ├── works-template/ # FOSS content template
│   └── library-template/ # FOSS library template
├── implementations/    # Proprietary licensed
│   ├── our-library/    # Customized implementation
│   ├── our-content/    # Our specific content
│   └── our-branding/   # Our specific branding
└── LICENSE             # Dual licensing explanation
```

### Strategy 3: Core-Extensions Split

**Core (FOSS)** + **Extensions (Proprietary)**

```
my-system/
├── core/               # Apache 2.0 licensed
│   ├── basic-tools/    # Standard FOSS tools
│   └── basic-templates/ # Standard FOSS templates
├── extensions/         # Proprietary licensed
│   ├── premium-features/ # Advanced proprietary features
│   ├── custom-integrations/ # Proprietary integrations
│   └── enterprise-tools/ # Commercial extensions
└── LICENSE             # Dual licensing model
```

## 📄 Licensing Documentation

### Repository Structure
Each repository should clearly indicate its licensing:

```
my-dual-licensed-project/
├── LICENSE-APACHE      # Apache 2.0 for FOSS components
├── LICENSE-PROPRIETARY # Proprietary license for content
├── README.md           # Explains dual licensing model
└── LICENSING.md        # Detailed licensing guide
```

### README.md Template
```markdown
# My Knowledge Library

## License

This project uses a **dual licensing model**:

### 🌐 FOSS Components (Apache 2.0)
- Universal tools and templates
- Core conversion functionality
- Base library template

### 🔒 Proprietary Components
- Specific content and implementations
- Custom branding and styling
- Proprietary integrations

See [LICENSING.md](LICENSING.md) for detailed information.
```

### LICENSING.md Template
```markdown
# Licensing Information

## Dual Licensing Model

This project demonstrates a dual licensing approach that combines:
1. **Free and Open Source Software (FOSS)** components
2. **Proprietary** content and implementations

## FOSS Components (Apache 2.0)

The following components are licensed under Apache 2.0:
- `/tools/` - Universal conversion tools
- `/templates/` - Base templates and examples
- `/scripts/` - Build and deployment scripts

You are free to:
- ✅ Use for any purpose
- ✅ Modify and distribute
- ✅ Use commercially
- ✅ Create proprietary derivatives

## Proprietary Components

The following components are proprietary:
- `/content/` - All content and materials
- `/branding/` - Custom branding and styling
- `/config/` - Specific configurations

These components are:
- 🔒 Copyrighted by [Your Organization]
- 🔒 Not freely distributable
- 🔒 Require permission for use

## Using This Model

You can use this dual licensing approach by:
1. Using our FOSS tools for your own projects
2. Creating your own proprietary content
3. Choosing your own licensing for your implementations
```

## 🎨 Use Case Examples

### Academic Institution
```
university-library/
├── tools/              # Apache 2.0 - Universal tools
├── course-materials/   # Proprietary - Course content
├── research-papers/    # Mixed - Depends on publication
└── public-resources/   # Apache 2.0 - Open educational resources
```

### Publishing Company
```
publisher-system/
├── conversion-tools/   # Apache 2.0 - Processing tools
├── book-catalog/       # Proprietary - Published books
├── author-tools/       # Apache 2.0 - Tools for authors
└── distribution/       # Proprietary - Sales and distribution
```

### Open Source Project
```
oss-documentation/
├── doc-tools/          # Apache 2.0 - Documentation tools
├── project-docs/       # Apache 2.0 - Project documentation
├── community-content/  # Apache 2.0 - Community contributions
└── examples/           # Apache 2.0 - Usage examples
```

## 🔧 Implementation Steps

### Step 1: Identify Components
Categorize your project components:
- **Universal tools**: Should be FOSS
- **Particular content**: Can be proprietary
- **Templates**: Usually FOSS
- **Implementations**: Your choice

### Step 2: Structure Your Repository
```bash
# Create dual-licensed structure
mkdir my-project
cd my-project

# FOSS components
mkdir -p foss/{tools,templates,scripts}
cp /path/to/apache-license foss/LICENSE

# Proprietary components
mkdir -p proprietary/{content,branding,config}
cat > proprietary/LICENSE << 'EOF'
© 2024 Your Organization. All rights reserved.
EOF

# Root documentation
cat > README.md << 'EOF'
# My Project

This project uses a dual licensing model...
EOF
```

### Step 3: Set Up Build System
Create `Makefile`:
```makefile
# Build using FOSS tools
build:
	@echo "Building with FOSS tools..."
	# Use Apache 2.0 licensed tools
	foss/tools/mdtexpdf proprietary/content/book.md
	foss/tools/mdaudiobook proprietary/content/book.md

# Deploy with your licensing
deploy:
	@echo "Deploying with proprietary licensing..."
	# Deploy your proprietary content
	# Using FOSS tools for processing
```

### Step 4: Document Your Approach
Create clear documentation explaining:
- Which components are FOSS
- Which components are proprietary
- How others can use your FOSS components
- How to implement their own dual licensing

## 💰 Monetization Strategies

### FOSS Tools + Proprietary Content
- **Tools**: Free to use and modify
- **Content**: Paid subscriptions, purchases, or licensing
- **Support**: Paid support for tool implementation

### FOSS Core + Proprietary Extensions
- **Core**: Free basic functionality
- **Extensions**: Paid premium features
- **Enterprise**: Paid enterprise support and features

### FOSS Templates + Proprietary Implementations
- **Templates**: Free starting points
- **Implementations**: Paid custom implementations
- **Consulting**: Paid implementation services

## ⚖️ Legal Considerations

### License Compatibility
- **Apache 2.0**: Compatible with most licenses
- **Proprietary**: Your choice of restrictions
- **Mixed projects**: Clearly separate components

### Attribution Requirements
- **Apache 2.0**: Requires attribution and license inclusion
- **Proprietary**: Your attribution requirements
- **Documentation**: Clear attribution in README

### Distribution Rights
- **FOSS components**: Can be freely distributed
- **Proprietary components**: Controlled distribution
- **Combined works**: Follow most restrictive license

## 🚀 Getting Started

### 1. Choose Your Model
Pick the dual licensing strategy that fits your needs:
- Tool-Content Split
- Template-Implementation Split
- Core-Extensions Split

### 2. Set Up Your Structure
Use our templates or create your own structure that clearly separates FOSS and proprietary components.

### 3. Document Everything
Create clear documentation explaining your licensing approach and how others can use your FOSS components.

### 4. Implement and Iterate
Start with a simple implementation and refine your approach based on feedback and needs.

## 📚 Resources

- [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0)
- [Implementation Examples](EXAMPLES.md)
- [Legal Resources](https://choosealicense.com/)
- [FOSS Best Practices](https://opensource.guide/)

## 🤝 Community

- Share your dual licensing implementations
- Contribute to the FOSS tools
- Help others implement dual licensing
- Join discussions about licensing strategies

---

*Dual licensing: The best of both worlds - FOSS flexibility with proprietary control*
