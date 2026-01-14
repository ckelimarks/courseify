# Courseify

Transform any codebase into an interactive learning course powered by AI.

## Concept

**The Problem**: Codebases are hard to learn from. Even with good documentation, understanding how technologies, patterns, and decisions fit together requires deep exploration.

**The Solution**: Courseify analyzes a codebase and generates a structured, beginner-friendly interactive course that teaches you the technologies, patterns, and engineering decisions by exploring real code.

## How It Works

1. **Input**: Provide a codebase (GitHub URL, local repo, or code files)
2. **Analysis**: Use the Courseify prompt framework with an AI (Claude, GPT-4, etc.) to explore the codebase structure, technologies, patterns, and architecture
3. **Generation**: AI creates progressive learning modules with:
   - Concept explanations (beginner-friendly)
   - Real code walkthroughs (actual files + line numbers)
   - Hands-on exercises (with complete setup instructions)
   - Interactive exploration challenges
4. **Output**: Load generated modules into the HTML course viewer for interactive learning

## Project Structure

```
courseify/
├── README.md                     # This file
├── prompts/
│   └── codebase-course-prompt.md # AI framework for generating courses
├── prototypes/
│   ├── courseify-wireframe.html  # Course viewer UI template
│   └── courseify-demo.html       # Example with Courseify course loaded
└── courses/
    └── courseify/                # Example: Course about Courseify itself
        ├── courseify-module-0.md # Getting Started (30 min)
        ├── courseify-module-1.md # The Prompt Framework (45 min)
        └── courseify-module-2.md # Interactive Delivery (45 min)
```

## Quick Start

### 1. Review the Prompt Framework

Open `prompts/codebase-course-prompt.md` to see how the AI is instructed to analyze codebases and generate courses.

### 2. Generate Your First Module

Use the prompt with Claude, GPT-4, or similar AI:

```
Using the Courseify framework in prompts/codebase-course-prompt.md,
generate Module 0: Getting Started for [Your Project].

Repository: [GitHub URL or codebase description]
Target audience: Beginners learning [technology]
```

### 3. Load Into Course Viewer

1. Open `prototypes/courseify-wireframe.html` in a text editor
2. Find the `courseModules` array
3. Paste your generated markdown content
4. Open in browser to view

## Example Course: Courseify Teaching Itself

This repo includes a meta example - **Courseify generating a course about Courseify**!

**What you learn:**
- How the prompt framework works
- Why certain instructions produce better courses
- How to customize the viewer
- How to deploy your own course

**Location:** `courses/courseify/`

**Try it:** Open `prototypes/courseify-demo.html` in your browser

## Design Principles

1. **Beginner-First**: Assume little to no coding experience. Define every technical term.
2. **Real Code Only**: All examples come from the actual codebase, not toy projects.
3. **Progressive Disclosure**: Build concepts incrementally. Don't overwhelm.
4. **Hands-On Learning**: Every module includes exercises with complete setup instructions.
5. **Context Matters**: Explain WHY decisions were made, not just WHAT they are.
6. **No Build Step**: Pure HTML/CSS/JS - works anywhere

## Tech Stack

**Current (Prototype)**
- **Frontend**: Vanilla HTML/CSS/JavaScript (single-file viewer)
- **Markdown Rendering**: marked.js (via CDN)
- **Course Generation**: Claude/GPT-4 with the Courseify prompt
- **Content**: Markdown files

**Why single-file HTML?**
- Easy to share (just send the .html file)
- Works offline (no dependencies)
- No hosting required (open in browser)
- Simple to customize (edit one file)

## Running the Prototype

1. Open `prototypes/courseify-demo.html` in a browser
2. Navigate through the Courseify course using the sidebar
3. See how generated modules are rendered
4. Click Previous/Next to move through content

## Creating Your Own Course

### Step 1: Generate Modules

Use an AI (Claude recommended) with the Courseify prompt to generate 3-5 modules for your codebase.

**Prompt template:**
```
Using the framework in courseify/prompts/codebase-course-prompt.md:

Codebase: [GitHub URL or description]
Target audience: [Beginners/Intermediate/Advanced]
Technologies: [React, Python, etc.]

Generate Module 0: Getting Started

Include:
- What this project does
- Why these technologies were chosen
- How to set up locally
- First steps for learners
```

### Step 2: Customize the Viewer

1. Copy `prototypes/courseify-wireframe.html` to `my-course.html`
2. Edit the `courseModules` array with your content
3. Customize colors, fonts, and branding in the CSS
4. Add your course title and description

### Step 3: Deploy

**Option 1: GitHub Pages**
- Push to GitHub
- Enable Pages in settings
- Your course is live!

**Option 2: Netlify Drop**
- Go to app.netlify.com/drop
- Drag your HTML file
- Instant public URL

**Option 3: Share Directly**
- Email the HTML file
- Works offline anywhere

## Vision

Imagine a world where every codebase could be learned interactively. Instead of:
- Reading dry documentation
- Guessing where to start
- Getting lost in unfamiliar code

You could:
- Follow a structured learning path
- See concepts explained in context
- Practice with real code
- Build understanding progressively

**Courseify makes codebases teachable.**

## Use Cases

- **Open source maintainers**: Help contributors understand your codebase
- **Teachers/Bootcamps**: Turn real projects into courses
- **Documentation**: Interactive alternative to static docs
- **Onboarding**: Help new team members learn the system
- **Personal learning**: Study any codebase systematically

## Contributing

Ideas welcome! This is an early prototype exploring:
- AI-assisted technical education
- Codebase analysis and documentation
- Interactive learning experiences

Potential contributions:
- New course examples for different tech stacks
- UI/UX improvements to the viewer
- Prompt framework enhancements
- Additional features (search, bookmarks, notes)

## License

MIT - Free to use and modify

---

**Created**: January 13, 2026 during Prototype Hour
**Status**: Working prototype with self-referential example course
**Repository**: https://github.com/ckelimarks/courseify

*Built with Claude Code*
