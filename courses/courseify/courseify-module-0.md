# Module 0: Getting Started with Courseify

**Estimated time:** 30 minutes
**Prerequisites:** Basic familiarity with AI prompts and course creation
**Learning objectives:**
- Understand what Courseify does and why it exists
- Learn the three-step workflow for generating courses
- Set up your environment to use Courseify

---

## What is Courseify?

Courseify is an **AI-powered course generator** that turns any codebase into structured, beginner-friendly learning materials. Instead of manually documenting your code, you use AI to analyze the repository and generate interactive modules.

### The Problem It Solves

**Traditional approach:**
- Manually write documentation
- Try to anticipate what beginners need to know
- Struggle to keep docs in sync with code changes
- Hard to create progressive learning paths

**Courseify approach:**
- AI analyzes the actual codebase
- Generates structured modules with code examples
- Includes exercises and explanations
- Can be regenerated as code evolves

---

## How It Works: The Three-Step Workflow

### Step 1: Analyze the Codebase

Courseify uses a specialized AI prompt (stored in `prompts/codebase-course-prompt.md`) that:
- Reads through the repository structure
- Identifies key technologies, patterns, and decisions
- Maps out the architecture and data flow

**Example:** For this Courseify repo, it would identify:
- Markdown files for course content
- HTML prototypes for interactive delivery
- Prompt templates for AI generation

### Step 2: Generate Modules

The AI creates progressive learning modules:
- **Module 0:** Getting Started (what you're reading now!)
- **Module 1:** Deep dive into core concepts
- **Module 2:** Advanced techniques and patterns

Each module includes:
- **Learning objectives:** What you'll know by the end
- **Concept explanations:** Plain language, no jargon
- **Code walkthroughs:** Line-by-line explanations
- **Practice exercises:** Hands-on application

### Step 3: Deliver Interactively

The generated modules can be:
- Read as markdown files
- Loaded into an HTML prototype for interactive navigation
- Customized with your own styling and branding

---

## Project Structure

```
courseify/
├── README.md                     # Project overview and instructions
├── prompts/
│   └── codebase-course-prompt.md # AI framework for course generation
├── prototypes/
│   ├── courseify-wireframe.html  # Basic HTML prototype
│   └── courseify-demo.html       # Example with Courseify course loaded
└── courses/
    └── courseify/                # Example: Course about Courseify itself
        ├── courseify-module-0.md # Getting Started (this file)
        ├── courseify-module-1.md # The Prompt Framework
        └── courseify-module-2.md # Interactive Delivery
```

**Key design principle:** Everything is files. No databases, no complex build steps. Just markdown for content and HTML for delivery.

---

## Setting Up Your Environment

### Prerequisites
- A codebase you want to teach (GitHub repo, local project, etc.)
- Access to Claude, GPT-4, or similar AI with good code understanding
- Text editor (VS Code, Sublime, etc.)
- Web browser (for viewing HTML prototypes)

### Step 1: Clone or Download Courseify
```bash
git clone https://github.com/ckelimarks/courseify.git
cd courseify
```

### Step 2: Review the Prompt Framework
Open `prompts/codebase-course-prompt.md` and read through it. This is the "system prompt" that tells the AI how to analyze codebases and generate courses.

**Key sections to notice:**
- **Codebase Analysis:** What the AI looks for
- **Learning Path Design:** How it structures modules
- **Module Structure:** The format of each module
- **Beginner Focus:** How it explains concepts

### Step 3: Prepare Your Codebase
The AI needs access to your code. You can:
- Provide a GitHub URL
- Share a zip file of the repository
- Copy/paste key files into the prompt

**Pro tip:** Start with a small, focused repo (< 20 files) for your first course. Larger codebases can overwhelm the AI.

### Step 4: Generate Your First Module
1. Copy the prompt from `codebase-course-prompt.md`
2. Add context about your codebase (URL, description, target audience)
3. Ask the AI: "Generate Module 0: Getting Started"
4. Save the output as `courses/[your-project]/module-0.md`

**Example prompt:**
```
Using the Courseify framework, generate Module 0 for [Your Project].

Repository: https://github.com/yourname/your-project
Target audience: Beginners learning React
Project description: A simple to-do app with local storage

Generate Getting Started module following the Courseify structure.
```

---

## What You'll Learn in This Course

By the end of the Courseify course, you'll understand:

**Module 0 (this module):**
- ✅ What Courseify is and why it exists
- ✅ The three-step workflow for generating courses
- ✅ How to set up your environment

**Module 1: The Prompt Framework**
- How the AI prompt is structured
- Why certain instructions produce better courses
- How to customize the prompt for your needs

**Module 2: Interactive Delivery**
- How the HTML prototypes work
- Loading generated modules into the UI
- Customizing styling and navigation

---

## Practice Exercise

**Goal:** Get familiar with the Courseify structure

**Instructions:**
1. Clone the Courseify repository (if you haven't already)
2. Open `README.md` in your text editor
3. Browse the `prompts/` folder and read `codebase-course-prompt.md`
4. Open `prototypes/courseify-wireframe.html` in your browser
5. Explore the course navigation and module structure

**Reflection questions:**
- What makes the prompt framework effective for generating courses?
- What kind of codebase would you want to teach with Courseify?
- What would you customize about the HTML prototype?

---

## Next Steps

Ready to dive deeper? Move on to:
- **Module 1:** The Prompt Framework - Learn how the AI generates great courses
- **Module 2:** Interactive Delivery - Build your own course viewer

**Estimated time to complete all modules:** 2-3 hours
