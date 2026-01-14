# Module 1: The Prompt Framework

**Estimated time:** 45 minutes
**Prerequisites:** Module 0 (Getting Started)
**Learning objectives:**
- Understand how the Courseify prompt is structured
- Learn why specific instructions produce better courses
- Customize the framework for your own needs

---

## Understanding the Prompt Framework

The heart of Courseify is `prompts/codebase-course-prompt.md` - a carefully crafted system prompt that tells AI how to analyze code and generate beginner-friendly courses.

### Why Prompts Matter

**Bad prompt:**
> "Explain this code to beginners"

**Result:** Generic explanations, assumes too much knowledge, no structure

**Good prompt (Courseify):**
> "You are a technical educator creating an interactive course from a codebase. Your goal is to help learners with **little to no coding experience**..."

**Result:** Structured modules, plain language, progressive learning path

---

## The Courseify Prompt Structure

Let's break down how the prompt is organized:

### Section 1: Role and Goal (Lines 1-8)

```markdown
You are a technical educator creating an interactive course from a codebase.
Your goal is to help learners with **little to no coding experience** understand
the technologies, patterns, and engineering decisions by exploring real working code.
```

**Why this works:**
- **"You are..."** - Sets the AI's identity (educator, not just code explainer)
- **"little to no coding experience"** - Explicit audience definition
- **"understand... by exploring"** - Focus on comprehension, not just facts

**Customization tip:** If your audience is more advanced, change this to "intermediate developers" or "experienced engineers learning [new tech]".

---

### Section 2: Codebase Analysis (Lines 14-20)

The prompt tells the AI what to look for:

```markdown
- **Tech stack**: Languages, frameworks, libraries, services
- **Architecture**: How components connect, data flows, state management
- **Key patterns**: Design patterns, architectural decisions, interesting techniques
- **Project structure**: Organization, separation of concerns
- **External integrations**: APIs, third-party services, webhooks
```

**Why this works:**
- Systematic analysis framework
- Covers technical AND architectural concerns
- Focuses on "why" not just "what"

**Example output for Courseify:**
- **Tech stack:** Markdown (content), HTML/CSS/JS (delivery)
- **Architecture:** File-based, no build step, static HTML
- **Key patterns:** Prompt engineering for course generation
- **Project structure:** `prompts/`, `courses/`, `prototypes/` separation
- **External integrations:** None (pure client-side)

---

### Section 3: Learning Path Design (Lines 22-26)

```markdown
Create a progressive course outline:
- **Beginner modules**: Setup, core concepts, basic patterns
- **Intermediate modules**: Component architecture, state management, API design
- **Advanced modules**: Complex integrations, edge cases, production concerns
```

**Why this works:**
- Explicit progression (beginner → advanced)
- Module themes are concrete (not vague "intro to X")
- Matches how real learning happens

**Customization tip:** For specialized courses, adjust the themes:
- **Data science:** "Data loading → Analysis → Visualization"
- **DevOps:** "Local setup → CI/CD → Production deployment"

---

### Section 4: Module Structure (Lines 28-80)

This is the most detailed section - it defines the exact format of each module.

#### 4.1 Concept Overview

```markdown
- What is this technology/pattern?
- Why was it chosen for this project?
- What problem does it solve?
- **Beginner context**: Explain like they've never seen it before
```

**Why "What/Why/Problem" works:**
- **What:** Concrete definition
- **Why:** Decision-making context
- **Problem:** Real-world relevance

**Example from this module:**
- **What:** The Courseify prompt is a structured instruction set
- **Why:** Generic "explain this code" prompts produce poor results
- **Problem:** Beginners need progressive, plain-language explanations

#### 4.2 Code Walkthrough

```markdown
- Point to specific files/functions (with line numbers)
- Explain how they work together
- Highlight interesting techniques or gotchas
- Use plain language, define jargon
```

**Key insight:** Line numbers and file paths make it concrete. "The prompt is in `prompts/codebase-course-prompt.md:1-8`" is better than "the prompt file."

#### 4.3 Real Examples

```markdown
- Extract 2-3 code snippets that demonstrate the concept
- Explain what **each line** does (for beginners)
- Show how it fits into the larger system
- Annotate code with inline comments
```

**Example annotation style:**
```javascript
// Load the course module data
const modules = [
  { id: 0, title: "Getting Started" },  // First module, no prerequisites
  { id: 1, title: "Prompt Framework" }, // Builds on Module 0
];
```

Not just "here's the code" - explain the purpose and context of each line.

#### 4.4 Interactive Exercises

```markdown
Each exercise includes complete setup instructions for beginners.

Format:
**Goal:** [One sentence - what they'll achieve]
**Setup:** [Step-by-step environment prep]
**Instructions:** [Numbered steps, very detailed]
**Expected outcome:** [What success looks like]
**Troubleshooting:** [Common issues + fixes]
```

**Why this structure works:**
- **Goal** - Clear motivation
- **Setup** - Removes "I don't know how to start" barrier
- **Expected outcome** - They know when they're done
- **Troubleshooting** - Anticipates failure modes

---

## Prompt Engineering Principles

What makes the Courseify prompt effective?

### 1. Explicit Audience Definition

✅ **Good:** "learners with **little to no coding experience**"
❌ **Bad:** "beginners" (too vague - beginner at what?)

### 2. Output Format Constraints

✅ **Good:** "Provide: Concept Overview, Code Walkthrough, Real Examples, Interactive Exercises"
❌ **Bad:** "Explain the code" (no structure)

### 3. Progressive Complexity

✅ **Good:** "Beginner modules: Setup, core concepts"
❌ **Bad:** "Create modules" (no guidance on order)

### 4. Real-World Context

✅ **Good:** "Why was it chosen for this project?"
❌ **Bad:** "What is this technology?" (no context)

### 5. Failure Mode Prevention

✅ **Good:** "Use plain language, define jargon"
❌ **Bad:** (no instruction - AI uses technical terms)

---

## Customizing the Prompt

Want to adapt Courseify for your needs? Here's how:

### For More Advanced Audiences

Change line 3:
```markdown
<!-- OLD -->
little to no coding experience

<!-- NEW -->
intermediate developers familiar with [JavaScript/Python/etc]
```

Then adjust module themes:
```markdown
- **Intermediate modules**: Advanced patterns, performance optimization
- **Expert modules**: Architecture decisions, scale considerations
```

### For Specific Technologies

Add a section after "Codebase Analysis":
```markdown
### Special Focus: [Your Tech]
- How [React/Django/etc] is used in this project
- Key patterns specific to [framework]
- Common gotchas when working with [library]
```

### For Non-Code Courses

Courseify can generate courses about things other than code! Adjust the analysis section:
```markdown
### 1. Project Analysis
- **Core concepts**: Main ideas, theories, frameworks
- **Structure**: How information is organized
- **Key insights**: Important discoveries or techniques
- **Practical applications**: Real-world use cases
```

---

## Practice Exercise

**Goal:** Customize the Courseify prompt for a different audience

**Instructions:**
1. Open `prompts/codebase-course-prompt.md` in your editor
2. Save a copy as `prompts/codebase-course-prompt-advanced.md`
3. Modify the audience definition (line 3) to: "experienced developers learning a new technology"
4. Adjust the module themes to focus on:
   - **Module 1:** Migration from familiar tech to this new tech
   - **Module 2:** Advanced patterns and best practices
   - **Module 3:** Production deployment and monitoring
5. Save your customized prompt

**Reflection:**
- How did changing the audience affect the structure?
- What other customizations would be useful for your use case?
- What could you remove from the prompt to make it simpler?

---

## Real-World Example: Generating This Course

This course (Courseify teaching Courseify) was generated using the Courseify prompt! Here's how:

**Step 1:** Input the Courseify repository URL
**Step 2:** Use the prompt: "Generate a 3-module beginner course about Courseify itself"
**Step 3:** AI analyzes the structure and generates:
- Module 0: Getting Started
- Module 1: The Prompt Framework (this one!)
- Module 2: Interactive Delivery

**Key insight:** The prompt framework is self-documenting. By following its own instructions, it produced the course you're reading now.

---

## Next Steps

You now understand how the Courseify prompt works! Ready to see how courses are delivered interactively?

- **Module 2:** Interactive Delivery - Build the HTML prototype and load your generated modules

**Estimated time remaining:** 1 hour
