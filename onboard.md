# /onboard - Interactive Developer Onboarding Site Generator

# Input
Additional instructions: $ARGUMENTS

## Command Purpose
Generate a comprehensive onboarding website that helps new developers quickly understand and start contributing to the codebase.

## Output Structure
Creates an `onboard/` directory containing:
```
onboard/
├── index.html          # Main landing page
├── architecture.html   # System architecture & diagrams
├── setup.html         # Development environment setup
├── codebase.html      # Code organization & patterns
├── workflows.html     # Development workflows
├── technologies.html  # Tech stack deep dive
├── resources.html     # Learning resources & docs
├── assets/
│   ├── style.css     # Unified styling
│   ├── script.js     # Interactive features
│   └── diagrams/     # Generated diagram files
└── data/
    └── codebase.json # Analyzed codebase metadata
```

## Analysis Phase

### 1. Project Discovery
- Detect primary language(s) and frameworks
- Identify build tools and package managers
- Analyze directory structure
- Find configuration files
- Detect testing frameworks
- Identify deployment configurations

### 2. Architecture Analysis
- Map high-level components
- Identify service boundaries
- Trace data flow patterns
- Document API endpoints
- Map database schemas
- Identify external integrations

### 3. Code Pattern Recognition
- Common design patterns used
- Naming conventions
- File organization patterns
- State management approach
- Error handling patterns
- Authentication/authorization flow

### 4. Development Workflow
- Git workflow (branching strategy)
- CI/CD pipeline steps
- Testing requirements
- Code review process indicators
- Deployment process clues

## Content Generation

### index.html - Welcome & Overview
```html
<!-- Dynamic content including: -->
- Project elevator pitch
- Key features and capabilities
- Quick start checklist
- Navigation to all sections
- Search functionality
- Recently updated indicators
```

### architecture.html - System Design
```html
<!-- Interactive diagrams showing: -->
- High-level architecture (Mermaid)
- Component relationships
- Data flow diagrams
- API architecture
- Database schema visualization
- Service dependencies
- Deployment architecture
```

Example diagrams to generate:
- **System Overview**: Component boxes showing frontend, backend, databases, external services
- **Request Flow**: Sequence diagram of typical user interaction
- **Data Model**: ER diagram of core entities
- **Service Map**: Microservices or module dependencies

### setup.html - Environment Setup
```html
<!-- Step-by-step guides for: -->
- Prerequisites checklist
- Repository cloning
- Dependency installation
- Environment variables
- Database setup
- Running locally
- Common setup issues
- Verification steps
```

### codebase.html - Code Organization
```html
<!-- Interactive file tree and explanations: -->
- Directory structure with purposes
- Key files and their roles
- Code style guide summary
- Common patterns examples
- Where to find what
- Adding new features guide
```

### workflows.html - Development Process
```html
<!-- Practical guides for: -->
- Creating a new feature
- Fixing a bug
- Writing tests
- Submitting PR/MR
- Running test suite
- Debugging tips
- Performance profiling
- Common tasks automation
```

### technologies.html - Tech Stack Deep Dive
```html
<!-- For each technology: -->
- Why we use it
- Version information
- Key concepts for this project
- Common gotchas
- Useful commands
- Links to documentation
- Links to learning resources
- Internal usage examples
```

### resources.html - Learning Hub
```html
<!-- Curated resources including: -->
- Official documentation links
- Recommended tutorials
- Video courses
- Internal wikis/docs
- Team conventions
- Slack/Discord channels
- Key contacts
- Glossary of terms
```

## Visual Design Elements

### Diagrams (using Mermaid.js)
- Architecture overviews
- Sequence diagrams for flows
- State diagrams for processes
- Entity relationship diagrams
- Gantt charts for project timelines
- Flowcharts for decision trees

### Interactive Features
- Collapsible sections
- Code syntax highlighting
- Copy-to-clipboard buttons
- Progress tracking checklist
- Search functionality
- Dark/light mode toggle
- Responsive design

### Styling Approach
- Clean, modern design
- Consistent color coding
- Clear typography hierarchy
- Accessible contrast ratios
- Mobile-responsive layout
- Print-friendly styles

## Technology Detection & Resources

### For each detected technology, provide:
1. **Overview**: What it does in this project
2. **Version**: Currently used version
3. **Configuration**: Where to find config files
4. **Common Tasks**: Project-specific usage
5. **Learning Path**:
   - Beginner resources
   - Advanced topics relevant to project
   - Official documentation
   - Community resources

### Example Technology Sections:
- **React**: Component patterns, state management approach, routing
- **Node.js**: API structure, middleware usage, async patterns
- **PostgreSQL**: Schema design, migration approach, query patterns
- **Docker**: Container setup, compose files, local development
- **Jest**: Test structure, mocking approach, coverage goals

## Implementation Details

### Analysis Output Format
The command should output progress indicators:
```
🔍 Analyzing project structure...
📊 Mapping architecture...
🎨 Generating diagrams...
📝 Creating documentation...
🎯 Building onboarding site...
✅ Onboarding site created at: ./onboard/index.html
```

### Smart Defaults
- Detect README files and incorporate content
- Find and link to existing documentation
- Identify and highlight recent changes
- Auto-generate glossary from code comments
- Extract TODO/FIXME items as known issues

### Customization Hooks
Allow developers to enhance generated content by:
- Including `.onboard.json` configuration
- Custom diagram definitions
- Additional resource links
- Team-specific information
- Project-specific guides

## Success Metrics
The generated site should enable a new developer to:
1. Understand what the project does in 5 minutes
2. Set up their environment in 30 minutes
3. Find any piece of code within 2 minutes
4. Make their first contribution in 1 day
5. Feel confident about the architecture in 1 week

## Example Usage
```
Human: /onboard