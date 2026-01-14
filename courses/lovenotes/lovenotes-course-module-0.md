# Module 0: Getting Started with LoveNotes

**Estimated time**: 45 minutes
**Prerequisites**: None - complete beginner friendly
**What you'll build/learn**: Set up your local development environment, run the LoveNotes app, and explore the codebase

## Overview

Welcome to the LoveNotes interactive course! In this module, you'll set up everything you need to explore a real-world production application. By the end, you'll have the LoveNotes app running on your computer and understand how to navigate the codebase.

**What is LoveNotes?** An SMS-based relationship app that sends daily appreciation prompts to couples via text message. Partners respond, and their answers are compiled into weekly "LoveLetters." Think of it as a low-friction way for couples to stay connected through small, consistent rituals.

**Why learn from this codebase?** LoveNotes is a production app serving real users, built with modern tools (React, TypeScript, Supabase), and includes real-world complexity like SMS integration, payments, and user authentication. It's a perfect learning environment.

## Concepts

Before we dive in, let's define a few terms you'll encounter:

### 1. Development Environment
Your development environment is the set of tools you use to write and test code on your own computer before deploying it to users. Think of it as your workshop where you can safely experiment.

**Key tools we'll use:**
- **Node.js**: A runtime that lets you run JavaScript outside of a browser
- **npm**: Node Package Manager - installs code libraries (like importing ingredients for a recipe)
- **Git**: Version control system - tracks changes to your code over time
- **VS Code**: A text editor for writing code (you can use any editor you prefer)

### 2. Frontend vs Backend
- **Frontend**: The part users see and interact with (the website/UI). In LoveNotes, this is the React app that runs in your browser.
- **Backend**: The server-side logic that handles data storage, authentication, and business logic. In LoveNotes, this is Supabase (database + edge functions).

### 3. Local Development
Running the app on your own computer (localhost) instead of on the internet. This lets you make changes and see results instantly without affecting real users.

## Code Walkthrough

Let's explore the LoveNotes project structure. After you clone the repository, you'll see this organization:

```
/Projects/lovenotes/app/
├── src/                    # Frontend React code
│   ├── components/        # Reusable UI pieces (buttons, forms, etc.)
│   ├── pages/            # Full page views (home, dashboard, etc.)
│   ├── integrations/     # Connections to external services (Supabase)
│   └── lib/              # Utility functions and helpers
├── supabase/
│   ├── functions/        # Backend API endpoints (edge functions)
│   └── migrations/       # Database schema definitions
├── public/               # Static files (images, icons)
└── package.json          # Project dependencies and scripts
```

**Key file to know**: `/Projects/lovenotes/app/package.json`

This file lists all the code libraries (dependencies) the project needs. When you run `npm install`, it reads this file and downloads everything listed. Here's a snippet:

```json
{
  "dependencies": {
    "react": "^18.3.1",           // UI framework
    "@supabase/supabase-js": "^2.81.0",  // Database client
    "react-router-dom": "^6.30.1"  // Page navigation
  }
}
```

## Try It Yourself

### Setup Instructions

**Step 1: Install Required Tools**

First, check if you have Node.js installed:

```bash
node --version
```

If you see a version number (like `v18.17.0`), you're good! If not, install Node.js:
- Go to [nodejs.org](https://nodejs.org)
- Download the "LTS" (Long Term Support) version
- Run the installer
- Verify installation: `node --version`

**Step 2: Install Git**

Check if Git is installed:

```bash
git --version
```

If not installed:
- Mac: `brew install git` (requires [Homebrew](https://brew.sh))
- Windows: Download from [git-scm.com](https://git-scm.com)
- Verify: `git --version`

**Step 3: Clone the Repository**

Navigate to where you want to store the project:

```bash
# Create a projects folder (if you don't have one)
mkdir -p ~/projects
cd ~/projects

# Clone the LoveNotes repository
git clone https://github.com/ckelimarks/ease-empathy-flow.git
cd ease-empathy-flow/app
```

**What just happened?** You copied the entire LoveNotes codebase from GitHub to your computer. The `app/` folder contains the actual application code.

**Step 4: Install Dependencies**

Now install all the code libraries the project needs:

```bash
npm install
```

**This will take 2-3 minutes.** You'll see lots of output - that's normal! npm is downloading hundreds of small code packages. When it's done, you'll see a message about the number of packages installed.

**Step 5: Start the Development Server**

```bash
npm run dev
```

**You'll know it works when you see:**
```
  VITE v5.4.19  ready in 347 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
```

**Step 6: View the App**

Open your browser and go to: `http://localhost:5173`

You should see the LoveNotes landing page with the hero section!

### Exercise 1: Explore the Running App

With the app running, explore these pages by clicking around:

1. **Home page** (`/`) - The marketing landing page
2. **Sign in** - Click "Sign In" in the navigation
3. **Browser DevTools** - Open them to peek under the hood

**How to open DevTools:**
- Mac: `Cmd + Option + I`
- Windows/Linux: `F12` or `Ctrl + Shift + I`

In DevTools, click the **Console** tab. You might see some messages - this is where developers log information while building.

### Exercise 2: Find Your First Component

Let's find the code that creates the hero section (the big headline at the top).

**Step 1:** Open VS Code in the project folder:

```bash
# From the app/ directory
code .
```

**Step 2:** Navigate to the hero component:
- In VS Code's file explorer (left sidebar)
- Open: `src/components/NewHero.tsx`

**Step 3:** Find line 32 (around there). You'll see:

```tsx
<h1 className="scroll-animate font-sans text-5xl font-extrabold tracking-tight text-foreground sm:text-6xl lg:text-7xl mb-6">
  Strengthen your <span className="text-primary relative inline-block">relationship<svg>...</svg></span>,<br /> one text at a time.
</h1>
```

This is JSX (JavaScript + HTML) that creates the headline. The text "Strengthen your relationship, one text at a time" is right there in the code!

**Step 4:** Make a small change. Change the headline text to:

```tsx
Strengthen your <span className="text-primary relative inline-block">bond<svg>...</svg></span>,<br /> one text at a time.
```

**Step 5:** Save the file (`Cmd + S` or `Ctrl + S`)

**Step 6:** Look at your browser - it should update automatically! This is called "hot module reloading" - your changes appear instantly without refreshing.

**Success criteria**: You see "Strengthen your bond, one text at a time" in the browser.

### Exercise 3: Using Browser DevTools

Let's inspect the page structure to see how the HTML is organized.

**Step 1:** Right-click on the headline in the browser and select **Inspect Element**

**Step 2:** You'll see the HTML structure in the DevTools Elements panel. It looks like this:

```html
<h1 class="scroll-animate font-sans text-5xl...">
  Strengthen your
  <span class="text-primary...">bond</span>
  , one text at a time.
</h1>
```

**Step 3:** Hover over different elements in the DevTools - notice how the corresponding parts of the page highlight. This is how you connect code to visual elements.

**Step 4:** In the **Console** tab, type:

```javascript
console.log("Hello from the console!")
```

Press Enter. You just ran JavaScript code directly in the browser!

## Troubleshooting

### Problem: `npm install` fails with permission errors

**Solution**: You might need to use `sudo` (not recommended) or fix npm permissions:
```bash
# Check npm version
npm --version

# If old version, update npm
npm install -g npm@latest
```

### Problem: `npm run dev` shows "Port 5173 is already in use"

**Solution**: Another process is using that port. Either:
- Close the other app using port 5173, or
- Kill the process: `lsof -ti:5173 | xargs kill -9`

### Problem: Browser shows blank page

**Solution**:
1. Check the terminal for error messages
2. Check the browser console (F12) for errors
3. Try clearing browser cache and reloading
4. Restart the dev server (`Ctrl + C` in terminal, then `npm run dev` again)

### Problem: VS Code won't open with `code .`

**Solution**:
- Open VS Code manually
- Go to View → Command Palette (`Cmd + Shift + P`)
- Type "shell command" and select "Install 'code' command in PATH"
- Restart terminal

## Key Takeaways

✅ **Development environment setup**: You've installed Node.js, Git, and cloned a real project
✅ **Running locally**: You can start a development server and view the app in your browser
✅ **Project structure**: Frontend code lives in `src/`, backend in `supabase/`
✅ **Hot reloading**: Changes to code appear instantly in the browser
✅ **DevTools**: Your debugging companion - use Console for logging, Elements for inspecting HTML
✅ **Components**: UI is built from small, reusable pieces (like `NewHero.tsx`)

## What's Next

In **Module 1**, we'll walk through the entire LoveNotes user journey - from signup to receiving prompts to getting a LoveLetter. You'll learn how data flows through the system and see the big picture of how everything connects.

**Preview**: We'll trace what happens when a user signs up, how daily prompts get sent via SMS, and how AI compiles responses into weekly summaries. You'll follow the code from frontend button click all the way to backend database.

## Further Exploration

Want to dig deeper? Try these challenges:

**Challenge 1: Find the Button Component**

The "Get Early Access" button is a reusable component. Can you find it?

**Hint**: Look in `src/components/ui/button.tsx`

**Challenge 2: Explore Package.json**

Open `package.json` and count how many dependencies are listed. What do you think `react-router-dom` does based on its name?

**Challenge 3: Navigate the File Tree**

Using VS Code's file explorer, find:
1. The main entry point (hint: `main.tsx`)
2. The home page component (hint: `pages/Index.tsx`)
3. The Supabase client setup (hint: `integrations/supabase/client.ts`)

**Challenge 4: Browser Network Tab**

Open DevTools → Network tab, then refresh the page. You'll see all the files being loaded. Can you spot the JavaScript bundle? (Look for files ending in `.js`)

**Challenge 5: Git History**

In the terminal, run:
```bash
git log --oneline -10
```

This shows the last 10 commits to the project. Each line represents a change to the codebase. Read through them to see what recent work was done!

---

**Ready to move on?** Make sure you can run the app locally and have explored the file structure. These foundational skills will be crucial as we dive deeper into the codebase in Module 1.
