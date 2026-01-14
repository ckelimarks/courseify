# Courseify

Transform any Git repository into an interactive learning course powered by AI.

## Concept

**The Problem**: Codebases are hard to learn from. Even with good documentation, understanding how technologies, patterns, and decisions fit together requires deep exploration.

**The Solution**: Courseify analyzes a git repository and generates a structured, beginner-friendly interactive course that teaches you the technologies, patterns, and engineering decisions by exploring real production code.

## How It Works

1. **Input**: User provides a git repository URL
2. **Analysis**: AI agent explores the codebase structure, technologies, patterns, and architecture
3. **Generation**: Creates progressive learning modules with:
   - Concept explanations (beginner-friendly)
   - Real code walkthroughs (actual files + line numbers)
   - Hands-on exercises (with complete setup instructions)
   - Interactive exploration challenges
4. **Output**: Beautiful course interface with sidebar navigation, markdown rendering, and progress tracking

## Current Status

### ✅ Completed (Proof of Concept)
- [x] Course generation prompt framework (`prompts/codebase-course-prompt.md`)
- [x] LoveNotes course specification (`prompts/generate-lovenotes-course.md`)
- [x] First 3 modules generated for LoveNotes codebase
  - Module 0: Getting Started (45 min)
  - Module 1: Project Overview (60 min)
  - Module 2: React Fundamentals (75 min)
- [x] Interactive course viewer UI (`prototypes/courseify-lovenotes.html`)
  - 3-screen flow (landing → generating → course)
  - Collapsible module navigation
  - Progress tracking
  - Markdown rendering with syntax highlighting
  - Responsive design

### 🚧 Next Steps
- [ ] Generate modules 3-5 for LoveNotes
  - Module 3: Understanding Supabase Backend
  - Module 4: The SMS Flow - Twilio Integration
  - Module 5: Edge Functions - Serverless API
- [ ] Connect UI to actual markdown files (currently mocked)
- [ ] Build backend to handle git repo cloning + analysis
- [ ] Real AI generation pipeline (Claude API integration)
- [ ] Exercise validation/testing
- [ ] Save user progress (localStorage or backend)

### 💡 Future Ideas
- Code playgrounds for exercises (embedded CodeSandbox)
- Interactive quizzes and checkpoints
- Community-contributed courses
- Multi-language support
- Video walkthroughs for complex concepts
- Export to PDF/ebook formats

## Project Structure

```
Projects/courseify/
├── README.md                           # This file
├── prompts/
│   ├── codebase-course-prompt.md      # Core framework for generating courses
│   └── generate-lovenotes-course.md   # LoveNotes-specific generation prompt
├── prototypes/
│   ├── courseify-wireframe.html       # Initial wireframe design
│   └── courseify-lovenotes.html       # Working prototype with LoveNotes content
└── courses/
    └── lovenotes/
        ├── lovenotes-course-module-0.md  # Module 0: Getting Started
        ├── lovenotes-course-module-1.md  # Module 1: Project Overview
        └── lovenotes-course-module-2.md  # Module 2: React Fundamentals
```

## Tech Stack

### Current (Prototype)
- **Frontend**: Vanilla HTML/CSS/JavaScript
- **Markdown Rendering**: marked.js
- **Course Generation**: Claude (AI agent with codebase access)

### Planned (Production)
- **Frontend**: React + TypeScript + Tailwind
- **Backend**: Node.js + Express (or Deno/Bun)
- **Database**: Supabase (courses, progress tracking)
- **AI**: Claude API for course generation
- **Git Operations**: simple-git or nodegit
- **Deployment**: Vercel or Cloudflare Pages

## Design Principles

1. **Beginner-First**: Assume little to no coding experience. Define every technical term.
2. **Real Code Only**: All examples come from the actual codebase, not toy projects.
3. **Progressive Disclosure**: Build concepts incrementally. Don't overwhelm.
4. **Hands-On Learning**: Every module includes exercises with complete setup instructions.
5. **Safe Environment**: Learners use git branches so they can't break anything.
6. **Context Matters**: Explain WHY decisions were made, not just WHAT they are.

## Example Course: LoveNotes

**Codebase**: [github.com/ckelimarks/ease-empathy-flow](https://github.com/ckelimarks/ease-empathy-flow)

**What you learn**:
- Modern React patterns (hooks, context, TypeScript)
- Supabase backend (database, auth, edge functions)
- SMS integration (Twilio webhooks)
- Payment processing (Stripe)
- State machines for workflow management
- Production considerations (error handling, security)

**Target audience**: Beginner to intermediate developers

**Estimated completion**: 6-8 hours across 5-8 modules

## Running the Prototype

1. Open `prototypes/courseify-lovenotes.html` in a browser
2. Click "Generate Interactive Course" to see the loading animation
3. Explore the course interface with:
   - Sidebar navigation (collapsible modules)
   - Lesson content with syntax-highlighted code
   - Previous/Next navigation
   - Progress tracking

**Note**: Content is currently embedded in the HTML. Production version would load from actual markdown files.

## Course Generation Workflow

1. **Read the framework**: `prompts/codebase-course-prompt.md`
2. **Customize for repo**: Create a generation prompt (like `generate-lovenotes-course.md`)
3. **Run AI agent**: Use Claude with file access to explore codebase and generate modules
4. **Review and edit**: Modules are markdown files, easy to refine
5. **Load into UI**: Courseify viewer renders the course

## Vision

Imagine a world where every open-source project could be learned interactively. Instead of:
- Reading dry documentation
- Guessing where to start
- Getting lost in unfamiliar codebases

You could:
- Follow a structured learning path
- See concepts explained in context
- Practice with real code
- Build understanding progressively

**Courseify makes codebases teachable.**

## Contributing

Currently a personal prototype. If this becomes public, contributions would be welcome for:
- New course modules for existing repos
- UI/UX improvements
- Backend implementation
- Additional codebase analysis features

## License

TBD (currently private project)

---

**Created**: January 13, 2026
**Status**: Proof of concept / Vibe-code prototype
**Next Session**: Generate remaining LoveNotes modules, connect UI to real markdown files
