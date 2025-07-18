# Universalis - Universal Knowledge Architecture System

*A comprehensive ecosystem of tools and templates for creating professional knowledge libraries*

## 🌟 Overview

Universalis is a **Free and Open Source** project that provides universal tools and templates for creating professional knowledge libraries. Based on Leibniz's vision of *Characteristica Universalis*, it embodies the **Universal → Particular** paradigm, where universal tools enable infinite particular implementations.

## 🎯 Philosophy

> *"The true method should furnish us with an Ariadne's thread, that is to say, with a certain sensible and palpable medium, which will guide the mind as do the lines drawn in geometry."* - Gottfried Wilhelm Leibniz

Universalis is that thread for the digital age, providing:

- **Universal Tools**: FOSS tools that work with any content
- **Particular Implementations**: Custom libraries and workflows
- **Rational Organization**: Structured knowledge transmission
- **Dual Licensing Model**: Freedom to choose your licensing approach

## 🛠️ Core Tools

### Content Conversion Tools
- **[mdtexpdf](https://github.com/ucli-tools/mdtexpdf)** - Markdown → PDF with LaTeX typesetting
- **[mdaudiobook](https://github.com/ucli-tools/mdaudiobook)** - Markdown → Audio with math narration
- **[mdepub](https://github.com/ucli-tools/mdepub)** - Markdown → EPUB for mobile reading

### Library Template
- **[library](https://github.com/ucli-tools/library)** - Universal web library template (Astro.js)

## 🏗️ Architecture

```
Universal Tools (FOSS) → Particular Implementations (Your Choice)

┌─────────────────────┐     ┌───────────────────────────┐
│   Universal Tools   │     │ Particular Implementations│
│                     │     │                           │
│ • mdtexpdf          │────▶│ • Your Content            │
│ • mdaudiobook       │     │ • Your Branding           │
│ • mdepub            │     │ • Your Licensing          │
│ • library template  │     │ • Your Workflow           │
└─────────────────────┘     └───────────────────────────┘
     Apache 2.0 FOSS           Your Choice
```

## 🚀 Quick Start

### Option 1: Complete FOSS Stack (Recommended)

For the full ecosystem experience, start with Ubuntu 24.04 and ucli:

```bash
# Install ucli (Universal Command Line Interface)
wget https://raw.githubusercontent.com/ucli-tools/ucli/main/ucli.sh
bash ./ucli.sh install
rm ./ucli.sh

# Install prerequisites and login
ucli prereq
ucli login ucli-tools

# Install all publishing tools at once
ucli build mdtexpdf mdaudiobook mdepub library
```

### Option 2: Manual Installation
```bash
# Install mdtexpdf
git clone https://github.com/ucli-tools/mdtexpdf
cd mdtexpdf && make install

# Install library template
git clone https://github.com/ucli-tools/library
cd library && npm install
```

### 2. Set Up Your Content
Create your content repository:
```bash
# Use our template or create your own structure
mkdir my-knowledge-library
cd my-knowledge-library
```

### 3. Choose Your Licensing
Decide on your licensing approach:
- **Full FOSS**: Use Apache 2.0 for everything
- **Dual Licensing**: FOSS tools + proprietary content
- **Custom**: Your own licensing combination

### 4. Build Your Library
Use the universal tools to create your particular implementation:
```bash
# Convert content to multiple formats
mdtexpdf my-content.md
mdaudiobook my-content.md

# Deploy your library
# (using the library template)
```

## 💪 Complete Self-Sufficiency: Knowledge = Power

### From Any Computer to Professional Publishing

Universalis demonstrates the ultimate **Knowledge = Power** principle by providing a complete path from any computer to professional-grade publishing:

```
Any Computer (Windows/macOS/Linux) → Ubuntu Bootstrap → ucli → Publishing Tools → Professional Content
```

**True Independence:**
- 💻 **Start anywhere**: Windows, macOS, or Linux computer
- 🔧 **Build your own OS**: Create Ubuntu 24.04 LTS from scratch
- 🏭 **Install complete ecosystem**: One command gets all publishing tools
- 📚 **Create professional content**: Multi-format publishing pipeline
- 🌐 **Deploy anywhere**: Complete control over hosting and distribution

**No Dependencies. No Subscriptions. No Vendor Control.**

📜 **[See the Complete Journey →](docs/COMPLETE_ECOSYSTEM.md)**

### Why This Matters

- **Complete Independence**: Build everything yourself from any starting point
- **True Ownership**: Own your tools, content, and entire publishing pipeline  
- **Professional Results**: LaTeX-quality PDFs, narrated audio, mobile EPUBs, web libraries
- **Unlimited Scaling**: From personal notes to professional publishing houses
- **Community Power**: Shared FOSS tools that benefit everyone

## 📚 Documentation

- **[Complete Ecosystem Guide](docs/COMPLETE_ECOSYSTEM.md)** - From Ubuntu to full FOSS publishing stack
- **[Getting Started Guide](docs/GETTING_STARTED.md)** - Complete setup walkthrough
- **[Architecture Overview](docs/ARCHITECTURE.md)** - How the tools work together
- **[Philosophy](docs/PHILOSOPHY.md)** - Universal → Particular paradigm

### Implementation Guides
- **[Dual Licensing Guide](docs/DUAL_LICENSING_GUIDE.md)** - How to implement dual licensing
- **[Content Workflow](docs/CONTENT_WORKFLOW.md)** - Setting up your publishing pipeline
- **[Examples](docs/EXAMPLES.md)** - Real-world implementation examples

### Templates
- **[Works Template](templates/works_template/)** - Content repository template
- **[Documentation Template](templates/documentation_template/)** - Project documentation template

## 🌐 Examples

### Basic Setup
See [examples/basic_setup/](examples/basic_setup/) for a minimal implementation using the universal tools.

### Dual Licensing Setup
See [examples/dual_licensing_setup/](examples/dual_licensing_setup/) for a complete dual licensing implementation.

### Content Workflow
See [examples/content_workflow/](examples/content_workflow/) for an automated content publishing pipeline.

## 🎆 Dual Licensing Model

Universalis demonstrates a powerful **dual licensing approach**:

### 🌐 Universal Tools (FOSS)
- **Apache 2.0 Licensed**: Free for everyone
- **No restrictions**: Use commercially, modify, distribute
- **Community driven**: Open source development

### 🔒 Particular Implementations (Your Choice)
- **Your content**: License however you want
- **Your branding**: Proprietary or open
- **Your workflow**: Custom implementations

This model allows:
- **Tool creators** to build sustainable FOSS ecosystems
- **Content creators** to maintain control over their work
- **Organizations** to use FOSS tools in proprietary workflows
- **Community** to benefit from universal tools

## 🎨 Use Cases

### Academic Institutions
- Use FOSS tools for course materials
- Maintain proprietary content licensing
- Share tools while protecting intellectual property

### Publishing Companies
- Leverage universal conversion tools
- Maintain proprietary content and branding
- Reduce development costs with FOSS infrastructure

### Open Source Projects
- Use all tools under Apache 2.0
- Create fully open knowledge libraries
- Contribute back to the ecosystem

### Individual Creators
- Start with FOSS tools
- Choose licensing that fits your goals
- Scale from personal to commercial use

## 🤝 Contributing

We welcome contributions to the universal tools!

### Development Principles
- **Universal Design**: Tools should work for everyone
- **Particular Flexibility**: Enable custom implementations
- **Quality First**: Maintain high standards
- **Community Driven**: Welcome diverse contributions

## 📄 License

**This project is licensed under the Apache 2.0 License** - see the [LICENSE](LICENSE) file for details.

### 🌐 Free and Open Source Software (FOSS)

This template and documentation hub is completely free and open source:

- ✅ Use for any purpose (commercial or non-commercial)
- ✅ Modify and customize for your needs
- ✅ Distribute your modifications
- ✅ Create proprietary implementations using these tools
- ✅ Implement your own dual licensing model

## 🌟 Featured Implementations

*Examples of organizations using Universalis tools:*

- **Academic Libraries**: Using mdtexpdf for course materials
- **Research Institutions**: Using mdaudiobook for accessible content
- **Publishing Houses**: Using the complete toolchain for digital publishing
- **Open Source Projects**: Using all tools for community documentation

*Want to be featured? Open an issue with your implementation!*

## 📞 Support

- **Documentation**: Check the [docs/](docs/) directory
- **Examples**: See [examples/](examples/) for working implementations
- **Issues**: Open issues in the relevant tool repositories
- **Community**: Join discussions in the project repositories

## 🔗 Related Projects

- **Individual Tools**: Each tool can be used independently
- **Template Libraries**: Use our templates or create your own
- **Community Implementations**: See how others are using Universalis

---

*Universalis: Where universal principles meet particular implementations*

**🌐 Universal Tools + 🔒 Particular Implementations = ∞ Possibilities**
