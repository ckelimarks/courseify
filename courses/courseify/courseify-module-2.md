# Module 2: Interactive Delivery

**Estimated time:** 45 minutes
**Prerequisites:** Module 0 (Getting Started), Module 1 (The Prompt Framework)
**Learning objectives:**
- Understand how HTML prototypes work
- Load generated course modules into the UI
- Customize styling and navigation
- Deploy your own course viewer

---

## Why Interactive Delivery Matters

Markdown files are great for content creation, but HTML provides:
- **Navigation:** Jump between modules easily
- **Progress tracking:** See what you've completed
- **Better readability:** Formatted text, code highlighting, structured layout
- **Portability:** Share a single HTML file that works anywhere

---

## The HTML Prototype Architecture

Courseify uses **pure client-side HTML** - no server, no build step, no npm dependencies.

### File Structure

```
prototypes/
├── courseify-wireframe.html    # Basic UI framework
└── courseify-demo.html          # Example with Courseify course loaded
```

**Key design principle:** Everything in one file. The HTML contains:
- Structure (HTML)
- Styling (CSS in `<style>` tag)
- Logic (JavaScript in `<script>` tag)
- Content (course modules as JSON data)

**Why single-file?**
- Easy to share (just email the .html file)
- Works offline (no external dependencies)
- No hosting required (open in browser)
- Simple to customize (edit one file)

---

## How the Prototype Works

Let's walk through `courseify-wireframe.html`:

### 1. HTML Structure (Lines 1-100)

```html
<div class="container">
  <!-- Sidebar: Module navigation -->
  <nav class="sidebar">
    <h1>Course Title</h1>
    <ul id="moduleList">
      <!-- Modules populated by JavaScript -->
    </ul>
  </nav>

  <!-- Main content area -->
  <main class="content">
    <div id="moduleContent">
      <!-- Selected module rendered here -->
    </div>
  </main>
</div>
```

**Key elements:**
- **`.sidebar`:** Shows list of modules
- **`.content`:** Displays the selected module
- **`#moduleList`:** JavaScript will fill this with module titles
- **`#moduleContent`:** JavaScript will render markdown as HTML here

### 2. CSS Styling (Lines 10-80)

The prototype uses a **two-column layout**:

```css
.container {
  display: grid;
  grid-template-columns: 300px 1fr;  /* Sidebar | Content */
  height: 100vh;
}
```

**Why grid?**
- Simple responsive layout
- Sidebar stays fixed width
- Content area fills remaining space

**Key design choices:**
- **Monospace font for code:** Makes code blocks stand out
- **Max-width on content:** Improves readability (60-80 characters per line)
- **Progress indicators:** Green checkmarks for completed modules

### 3. JavaScript Logic (Lines 100-200)

The magic happens in the JavaScript:

```javascript
// 1. Define course modules as data
const courseModules = [
  { id: 0, title: "Module 0: Getting Started", markdown: "..." },
  { id: 1, title: "Module 1: Prompt Framework", markdown: "..." },
  { id: 2, title: "Module 2: Interactive Delivery", markdown: "..." }
];

// 2. Render module list in sidebar
function renderModuleList() {
  const list = document.getElementById('moduleList');
  courseModules.forEach(module => {
    const li = document.createElement('li');
    li.textContent = module.title;
    li.onclick = () => loadModule(module.id);
    list.appendChild(li);
  });
}

// 3. Load and display selected module
function loadModule(moduleId) {
  const module = courseModules[moduleId];
  const content = document.getElementById('moduleContent');

  // Convert markdown to HTML (using marked.js or similar)
  content.innerHTML = convertMarkdownToHTML(module.markdown);

  // Mark module as completed
  markModuleComplete(moduleId);
}
```

**Key insight:** Course data is just a JavaScript array. To add your generated modules:
1. Copy the markdown content
2. Paste it into the `courseModules` array
3. That's it - no build step required

---

## Loading Your Generated Modules

Let's walk through adding your own course to the prototype.

### Step 1: Prepare Your Module Content

You've generated `courses/my-project/module-0.md`. Copy the entire markdown content.

### Step 2: Open the Prototype

Open `prototypes/courseify-wireframe.html` in your text editor.

### Step 3: Find the courseModules Array

Search for `const courseModules = [` (around line 120).

### Step 4: Add Your Module

```javascript
const courseModules = [
  {
    id: 0,
    title: "Module 0: Getting Started",
    markdown: `
# Module 0: Getting Started

[PASTE YOUR MARKDOWN CONTENT HERE]
    `
  },
  {
    id: 1,
    title: "Module 1: [Your Next Module]",
    markdown: `
[PASTE MODULE 1 CONTENT]
    `
  }
];
```

**Important:** Use template literals (backticks) so you can paste multi-line markdown.

### Step 5: Save and Open in Browser

Save the file, then open it in your browser. You should see:
- Sidebar with your module titles
- Clickable navigation
- Formatted markdown content

---

## Markdown Rendering

The prototype needs to convert markdown to HTML. Two approaches:

### Approach 1: Use marked.js (Recommended)

Add this script tag before your JavaScript:

```html
<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
```

Then use it in your code:

```javascript
function convertMarkdownToHTML(markdown) {
  return marked.parse(markdown);
}
```

**Pros:** Full markdown support (tables, code blocks, lists)
**Cons:** Requires internet (CDN dependency)

### Approach 2: Embed marked.js

For offline use, copy the entire marked.js library into your HTML:

```html
<script>
// [entire marked.js source code here - ~50KB]
</script>
```

**Pros:** Works offline, single file
**Cons:** Larger file size

### Approach 3: Simplified Markdown Parser

For basic markdown, write your own simple parser:

```javascript
function convertMarkdownToHTML(markdown) {
  return markdown
    .replace(/^### (.*$)/gim, '<h3>$1</h3>')      // ### Headings
    .replace(/^## (.*$)/gim, '<h2>$1</h2>')       // ## Headings
    .replace(/^# (.*$)/gim, '<h1>$1</h1>')        // # Headings
    .replace(/\*\*(.*)\*\*/gim, '<strong>$1</strong>')  // **bold**
    .replace(/\*(.*)\*/gim, '<em>$1</em>')        // *italic*
    .replace(/```(.*?)```/gims, '<pre><code>$1</code></pre>'); // ```code blocks```
}
```

**Pros:** No dependencies, lightweight
**Cons:** Limited markdown support

---

## Customizing the UI

Want to make the course viewer your own? Here's what to customize:

### 1. Colors and Branding

Find the CSS variables (around line 20):

```css
:root {
  --primary-color: #2563eb;      /* Change to your brand color */
  --bg-dark: #1e293b;
  --bg-light: #f8fafc;
  --text-dark: #0f172a;
}
```

### 2. Typography

Change fonts:

```css
body {
  font-family: 'Inter', -apple-system, sans-serif;  /* Your preferred font */
}

code {
  font-family: 'Fira Code', monospace;  /* Code font */
}
```

### 3. Layout

Adjust sidebar width:

```css
.container {
  grid-template-columns: 250px 1fr;  /* Narrower sidebar */
}
```

Or make it responsive:

```css
@media (max-width: 768px) {
  .container {
    grid-template-columns: 1fr;  /* Stack on mobile */
  }
}
```

### 4. Code Highlighting

Add syntax highlighting with Prism.js:

```html
<link href="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/themes/prism-tomorrow.css" rel="stylesheet" />
<script src="https://cdn.jsdelivr.net/npm/prismjs@1.29.0/prism.js"></script>
```

Then in your JavaScript:

```javascript
function loadModule(moduleId) {
  // ... existing code ...

  // Highlight code blocks after rendering
  Prism.highlightAll();
}
```

---

## Progress Tracking

The prototype includes simple progress tracking:

```javascript
// Store completed modules in localStorage
function markModuleComplete(moduleId) {
  const completed = JSON.parse(localStorage.getItem('completed') || '[]');
  if (!completed.includes(moduleId)) {
    completed.push(moduleId);
    localStorage.setItem('completed', JSON.stringify(completed));
  }
  updateProgressUI();
}

// Show checkmarks for completed modules
function updateProgressUI() {
  const completed = JSON.parse(localStorage.getItem('completed') || '[]');
  completed.forEach(id => {
    const moduleItem = document.querySelector(`[data-module-id="${id}"]`);
    moduleItem.classList.add('completed');  // Adds checkmark via CSS
  });
}
```

**How it works:**
1. When user finishes a module, call `markModuleComplete(id)`
2. Module ID saved to browser's localStorage
3. Checkmark appears in sidebar
4. Persists across browser sessions

---

## Deploying Your Course

### Option 1: GitHub Pages (Free Hosting)

1. Create a GitHub repo for your course
2. Add your customized HTML file as `index.html`
3. Enable GitHub Pages in repo settings
4. Your course is live at `https://yourusername.github.io/your-repo`

### Option 2: Netlify Drop (Easiest)

1. Go to https://app.netlify.com/drop
2. Drag your HTML file
3. Get instant public URL
4. No account required!

### Option 3: Share the File Directly

Since it's a single HTML file:
- Email it
- Put it on Dropbox/Google Drive
- Share via USB drive
- Works anywhere with a browser

---

## Practice Exercise

**Goal:** Create your own custom course viewer

**Instructions:**

1. **Copy the wireframe:**
   ```bash
   cp prototypes/courseify-wireframe.html my-course.html
   ```

2. **Add your course data:**
   - Open `my-course.html`
   - Find the `courseModules` array
   - Paste in your generated module content

3. **Customize the branding:**
   - Change the `:root` CSS variables to your colors
   - Update the `<title>` tag
   - Add your name/logo in the sidebar

4. **Test it:**
   - Open `my-course.html` in your browser
   - Navigate between modules
   - Complete a module and check for the checkmark

5. **Deploy it:**
   - Upload to GitHub Pages or Netlify
   - Share the link!

**Expected outcome:**
You have a working, branded course viewer with your content loaded and hosted online.

---

## Advanced: Adding Features

Want to extend the prototype? Here are ideas:

### Search Functionality

```javascript
function searchModules(query) {
  const results = courseModules.filter(module =>
    module.title.toLowerCase().includes(query.toLowerCase()) ||
    module.markdown.toLowerCase().includes(query.toLowerCase())
  );
  renderSearchResults(results);
}
```

### Bookmarks

```javascript
function bookmarkSection(moduleId, sectionId) {
  const bookmarks = JSON.parse(localStorage.getItem('bookmarks') || '{}');
  bookmarks[moduleId] = sectionId;
  localStorage.setItem('bookmarks', JSON.stringify(bookmarks));
}
```

### Estimated Time

```javascript
const courseModules = [
  {
    id: 0,
    title: "Getting Started",
    estimatedMinutes: 30,  // Add time estimate
    markdown: "..."
  }
];
```

Display total course time in the sidebar.

### Notes

Let users add personal notes to each module:

```javascript
function saveNote(moduleId, noteText) {
  const notes = JSON.parse(localStorage.getItem('notes') || '{}');
  notes[moduleId] = noteText;
  localStorage.setItem('notes', JSON.stringify(notes));
}
```

---

## Course Complete!

Congratulations! You now understand:
- ✅ How to generate courses from codebases using the Courseify prompt
- ✅ How the prompt framework is structured and why it works
- ✅ How to build interactive course viewers with HTML
- ✅ How to customize, deploy, and share your courses

### What You've Built

By following this course, you've:
1. Learned the Courseify workflow
2. Understood prompt engineering for course generation
3. Built a working course viewer
4. Deployed it publicly (if you did the exercises)

### Next Steps

**Apply what you learned:**
- Pick a codebase you want to teach (your own project, open source, etc.)
- Use the Courseify prompt to generate 3-5 modules
- Build a custom course viewer
- Share it with your community!

**Improve Courseify:**
- Contribute back to the project (https://github.com/ckelimarks/courseify)
- Share courses you've generated
- Suggest new features or prompt improvements

---

## Final Exercise

**Goal:** Generate and publish your first complete course

**Instructions:**

1. Choose a codebase (start small - under 20 files)
2. Use the Courseify prompt to generate 3 modules
3. Create a custom HTML viewer with your modules
4. Deploy to GitHub Pages or Netlify
5. Share the link!

**Reflection:**
- What worked well in your generated course?
- What did you customize in the prompt?
- How would you improve the HTML viewer?
- What's the next codebase you want to teach?

---

**Course complete! Thanks for learning with Courseify.**

Want to stay updated? Star the repo: https://github.com/ckelimarks/courseify
