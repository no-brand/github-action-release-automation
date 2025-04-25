# Ontology Release Automation

This repository demonstrates automated versioning and release management for ontology projects using GitHub Actions.

## 📋 Project Overview
- Each top-level directory represents a separate ontology sub-project
- Ontology files are stored in `.ttl` (Turtle) and `.dlog` (Datalog) formats
- GitHub Actions automatically creates versioned releases when changes are merged into main

## 🚀 How It Works
1. Merge a PR into the main branch
2. GitHub Actions identifies changed sub-projects
3. For each sub-project, a versioned tag is created: `v{SUB_PROJECT}-{YYYYMMDD}-{REVISION}`
4. A release is created with ontology files packaged as a zip file
5. Release notes include a table showing file details and changes

## 🧪 Sample Data Structure
The repository contains sample ontology projects:
- `A/` - Example ontology for domain A
- `B/` - Example ontology for domain B

## 🔧 Development
1. Clone the repository
2. Make changes to ontology files
3. Create a PR to main
4. Merge the PR to trigger the release workflow

## 📚 Documentation
For detailed requirements and specifications, see [.doc/requirements.md](.doc/requirements.md) 