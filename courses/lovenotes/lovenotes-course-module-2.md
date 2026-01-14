# Module 2: React Fundamentals in Practice

**Estimated time**: 75 minutes
**Prerequisites**: Module 0 (Setup), Module 1 (Project Overview)
**What you'll build/learn**: Understand React components, props, JSX, and TypeScript by modifying real LoveNotes code

## Overview

You've seen the big picture. Now let's dive into how React actually works. Instead of abstract examples, we'll learn by reading and modifying actual components from the LoveNotes codebase.

By the end of this module, you'll:
- Understand what a component is and how they compose together
- Read JSX (JavaScript + HTML) confidently
- Pass data between components using props
- Add console logs to trace component rendering
- Make meaningful code changes with immediate visual feedback

**No theory-only learning here** - every concept comes with hands-on practice in the real codebase.

## Concepts

### 1. Components: The Building Blocks

In React, everything is a **component** - a reusable piece of UI. Think of components like LEGO blocks: small, focused pieces that snap together to build complex interfaces.

**Example from LoveNotes**: The home page (`Index.tsx`) is composed of many smaller components:

```tsx
// File: /app/src/pages/Index.tsx (simplified)
const Index = () => {
  return (
    <div>
      <StickyNav />       {/* Navigation bar */}
      <NewHero />         {/* Hero section with headline */}
      <HowItWorks />      {/* 3-step explanation */}
      <SignupForm />      {/* Email capture form */}
      <Footer />          {/* Footer links */}
    </div>
  );
};
```

Each component is self-contained. `NewHero` doesn't know or care about `Footer`. They just do their job.

**Two types of components**:

1. **Page components** (`src/pages/`) - Full page views like `Index`, `Dashboard`, `Auth`
2. **Reusable components** (`src/components/`) - Smaller pieces like `Button`, `HowItWorks`, `NewHero`

### 2. JSX: JavaScript + HTML

JSX looks like HTML but it's actually JavaScript. When you write:

```tsx
<h1 className="text-5xl font-bold">Hello World</h1>
```

React converts it to:

```javascript
React.createElement('h1', { className: 'text-5xl font-bold' }, 'Hello World')
```

**Key differences from HTML**:
- `className` instead of `class` (because `class` is a reserved word in JS)
- Self-closing tags require `/`: `<img />` not `<img>`
- Use `{}` to embed JavaScript expressions: `<p>Today is {new Date().getFullYear()}</p>`

**Example from NewHero component** (`/app/src/components/NewHero.tsx`, line 29-33):

```tsx
<h1 className="scroll-animate font-sans text-5xl font-extrabold tracking-tight text-foreground sm:text-6xl lg:text-7xl mb-6">
  Strengthen your <span className="text-primary relative inline-block">
    relationship
  </span>,<br /> one text at a time.
</h1>
```

This is JSX. The `className` applies CSS styles. The `<span>` and `<br />` are HTML elements embedded in the JS.

### 3. Props: Passing Data to Components

**Props** (short for "properties") are how you pass data from a parent component to a child component. Think of props like function arguments.

**Example**: The `Button` component can look different based on props.

```tsx
// Using the Button component with different props
<Button size="lg" variant="default">
  Get Early Access
</Button>

<Button size="sm" variant="outline">
  Learn More
</Button>
```

**The Button component definition** (`/app/src/components/ui/button.tsx`, line 39-44):

```tsx
const Button = React.forwardRef<HTMLButtonElement, ButtonProps>(
  ({ className, variant, size, asChild = false, ...props }, ref) => {
    const Comp = asChild ? Slot : "button";
    return <Comp className={cn(buttonVariants({ variant, size, className }))} ref={ref} {...props} />;
  },
);
```

**What this means**:
- The function receives props: `variant`, `size`, `className`, etc.
- It uses those props to determine how the button looks
- Different props → different styles/behavior

**Props flow one way**: Parent → Child (never the other way). If a child needs to communicate back to a parent, it does so via **callback functions** passed as props.

### 4. TypeScript: Types Make Code Safer

TypeScript adds **type annotations** to JavaScript, helping catch bugs before runtime.

**Example from Dashboard** (`/app/src/pages/Dashboard.tsx`, line 12-20):

```tsx
interface PhoneSubscription {
  id: string;
  primary_phone: string;
  secondary_phone: string | null;  // Can be string OR null
  timezone: string;
  preferred_send_time: string;
  plan_type: string;
  is_active: boolean;              // Must be true or false
}
```

This **interface** defines the shape of a `PhoneSubscription` object. If you try to use a field that doesn't exist (like `subscription.email`), TypeScript will show an error **before you even run the code**.

**Benefits**:
- Autocomplete: Your editor knows what fields exist
- Error prevention: Typos and wrong types are caught immediately
- Documentation: The type tells you what data looks like

## Code Walkthrough

Let's trace how a component renders, starting with the home page.

### Entry Point: main.tsx

**File**: `/app/src/main.tsx`

```tsx
// Line 1-5
import { createRoot } from "react-dom/client";
import App from "./App.tsx";
import "./index.css";

createRoot(document.getElementById("root")!).render(<App />);
```

**What happens**:
1. React finds the HTML element with id="root" (in `/app/index.html`)
2. Creates a React root at that element
3. Renders the `<App />` component inside it

This is the **entry point** - where your React app starts.

### App Component: Routing

**File**: `/app/src/App.tsx`

```tsx
// Line 19-41 (simplified)
const App = () => (
  <QueryClientProvider client={queryClient}>
    <TooltipProvider>
      <BrowserRouter>
        <Routes>
          <Route path="/" element={<Index />} />
          <Route path="/auth" element={<Auth />} />
          <Route path="/app" element={<Dashboard />} />
          <Route path="/admin" element={<Admin />} />
          <Route path="*" element={<NotFound />} />
        </Routes>
      </BrowserRouter>
    </TooltipProvider>
  </QueryClientProvider>
);
```

**What this does**:
- `BrowserRouter`: Enables navigation (changing pages without full reload)
- `Routes`: Defines which component to show for each URL
- `path="/"` → shows `<Index />` component
- `path="/app"` → shows `<Dashboard />` component
- `path="*"` → catch-all for 404 pages

**Providers**: `QueryClientProvider` and `TooltipProvider` wrap the entire app, providing shared functionality to all components below them. Think of them as app-wide settings.

### Index Page: Component Composition

**File**: `/app/src/pages/Index.tsx`

```tsx
// Line 37-52
return (
  <div className="min-h-screen">
    <StickyNav />
    <main className="pt-20">
      <NewHero />
      <NewPainPoints />
      <HowItWorks />
      <Features />
      <ScienceBacked />
      <CreatorQuote />
      <NewTestimonials />
      <SignupForm />
    </main>
    <Footer />
  </div>
);
```

This is **component composition** - the Index page is built by stacking other components. Each component is responsible for one section of the page.

**Visual mapping**:
- `StickyNav` → Navigation bar at top
- `NewHero` → Big headline + phone mockup
- `HowItWorks` → 3-step explanation
- `SignupForm` → Email capture
- `Footer` → Bottom links

### NewHero Component: Props and Event Handlers

**File**: `/app/src/components/NewHero.tsx`

```tsx
// Line 4-8
const scrollToSignup = () => {
  document.getElementById("signup")?.scrollIntoView({
    behavior: "smooth"
  });
};

// Line 44-46
<Button onClick={scrollToSignup} size="lg" className="...">
  Get Early Access
</Button>
```

**Breaking this down**:

1. **Function definition**: `scrollToSignup` is a function that finds an element and scrolls to it
2. **Event handler**: `onClick={scrollToSignup}` means "when button is clicked, call this function"
3. **Props**: `size="lg"` and `className="..."` customize the button's appearance

**Note**: We pass `scrollToSignup` (the function itself), not `scrollToSignup()` (the result of calling it). If we used `onClick={scrollToSignup()}`, the function would run immediately when rendering, not on click.

### HowItWorks Component: useEffect Hook

**File**: `/app/src/components/HowItWorks.tsx`

```tsx
// Line 1
import { useEffect } from "react";

// Line 4-38
useEffect(() => {
  const triggers = document.querySelectorAll('.step-trigger');
  const screens = {
    '1': document.getElementById('phone-screen-1'),
    '2': document.getElementById('phone-screen-2'),
    '3': document.getElementById('phone-screen-3')
  };

  const stickyObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const step = entry.target.getAttribute('data-step');
        // ... switch which phone screen is visible
      }
    });
  }, { threshold: 0.5 });

  triggers.forEach(trigger => {
    stickyObserver.observe(trigger);
  });

  return () => {
    triggers.forEach(trigger => stickyObserver.unobserve(trigger));
  };
}, []);
```

**What is useEffect?**

`useEffect` runs code **after** the component renders. It's used for:
- Setting up DOM listeners (like here)
- Fetching data from an API
- Subscribing to external events

**The pattern**:
```tsx
useEffect(() => {
  // Code to run after render

  return () => {
    // Cleanup code (runs when component unmounts)
  };
}, [dependencies]);
```

**In this case**:
- After the component renders, set up an IntersectionObserver (watches when elements become visible)
- When the user scrolls, switch which phone screen is shown
- When the component is removed, clean up the observer (prevent memory leaks)

**The `[]` at the end**: Empty array means "run this effect once after first render, never again."

### Button Component: Reusable with Variants

**File**: `/app/src/components/ui/button.tsx`

```tsx
// Line 7-31
const buttonVariants = cva(
  "inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-md text-sm font-medium ring-offset-background transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 [&_svg]:pointer-events-none [&_svg]:size-4 [&_svg]:shrink-0",
  {
    variants: {
      variant: {
        default: "bg-primary text-primary-foreground hover:bg-primary/90",
        destructive: "bg-destructive text-destructive-foreground hover:bg-destructive/90",
        outline: "border border-input bg-background hover:bg-accent hover:text-accent-foreground",
        secondary: "bg-secondary text-secondary-foreground hover:bg-secondary/80",
        ghost: "hover:bg-accent hover:text-accent-foreground",
        link: "text-primary underline-offset-4 hover:underline",
      },
      size: {
        default: "h-10 px-4 py-2",
        sm: "h-9 rounded-md px-3",
        lg: "h-11 rounded-md px-8",
        icon: "h-10 w-10",
      },
    },
    defaultVariants: {
      variant: "default",
      size: "default",
    },
  },
);
```

**What is cva?**

`cva` (class variance authority) is a helper that generates CSS classes based on props. It's like a style system:

- Base styles (always applied): `"inline-flex items-center ..."`
- Variant styles (conditional): `variant="outline"` adds `"border border-input ..."`
- Size styles: `size="lg"` adds `"h-11 rounded-md px-8"`

**Result**: You get consistent, flexible buttons throughout the app without repeating CSS.

## Try It Yourself

### Exercise 1: Modify the Hero Headline

Let's change the main headline and see the result instantly.

**Step 1**: Make sure the dev server is running (`npm run dev`)

**Step 2**: Open `/app/src/components/NewHero.tsx` in VS Code

**Step 3**: Find the `<h1>` tag around line 29. It currently says:

```tsx
Strengthen your <span className="text-primary relative inline-block">relationship</span>,<br /> one text at a time.
```

**Step 4**: Change it to:

```tsx
Build a stronger <span className="text-primary relative inline-block">connection</span>,<br /> with daily love notes.
```

**Step 5**: Save the file (`Cmd + S` or `Ctrl + S`)

**Step 6**: Look at your browser - the change should appear automatically!

**Success criteria**: The hero headline now says "Build a stronger connection, with daily love notes."

**Bonus challenge**: Change the subheading too (the `<p>` tag around line 35).

### Exercise 2: Add a Console Log to Track Button Clicks

Let's see exactly when a component function runs.

**Step 1**: Still in `/app/src/components/NewHero.tsx`, find the `scrollToSignup` function (line 4-8)

**Step 2**: Add a console log at the start of the function:

```tsx
const scrollToSignup = () => {
  console.log("🚀 Get Early Access button clicked!");
  document.getElementById("signup")?.scrollIntoView({
    behavior: "smooth"
  });
};
```

**Step 3**: Save the file

**Step 4**: Open your browser's DevTools (F12) and go to the **Console** tab

**Step 5**: On the home page, click "Get Early Access"

**Success criteria**: You see "🚀 Get Early Access button clicked!" logged in the console, and the page scrolls to the signup form.

**What you learned**: Console logs are your best friend for debugging. They let you trace code execution and inspect data.

### Exercise 3: Pass Props to a Component

Let's create a custom variation of the Button component.

**Step 1**: Find the "See How It Works" button in `NewHero.tsx` (around line 47):

```tsx
<Button onClick={scrollToHowItWorks} variant="outline" size="lg" className="group w-full sm:w-auto text-lg">
  See How It Works
  <ArrowRight className="transition-transform group-hover:translate-x-1" />
</Button>
```

**Step 2**: Change the variant from `"outline"` to `"secondary"`:

```tsx
<Button onClick={scrollToHowItWorks} variant="secondary" size="lg" className="group w-full sm:w-auto text-lg">
  See How It Works
  <ArrowRight className="transition-transform group-hover:translate-x-1" />
</Button>
```

**Step 3**: Save and observe the button's new style in the browser

**Step 4**: Try other variants: `"default"`, `"ghost"`, `"link"`

**Success criteria**: You understand how changing props changes the component's appearance.

**What's happening behind the scenes**: The Button component receives `variant="secondary"` as a prop, looks up the corresponding CSS classes in `buttonVariants`, and applies them.

### Exercise 4: Trace Component Rendering

Let's see the order in which components render.

**Step 1**: Open `/app/src/pages/Index.tsx`

**Step 2**: At the top of the component function (before the `return`), add:

```tsx
const Index = () => {
  console.log("📄 Index page rendering");

  useEffect(() => {
    // ... existing code
  }, []);

  return (
    // ... existing JSX
  );
};
```

**Step 3**: Open `/app/src/components/NewHero.tsx`

**Step 4**: Add a similar log at the top:

```tsx
const NewHero = () => {
  console.log("🦸 NewHero component rendering");

  const scrollToSignup = () => {
    // ... existing code
  };

  return (
    // ... existing JSX
  );
};
```

**Step 5**: Save both files and refresh your browser

**Step 6**: Check the Console tab in DevTools

**Success criteria**: You see:
```
📄 Index page rendering
🦸 NewHero component rendering
(plus logs from other components)
```

**What you learned**:
- Parent components render before their children
- Every render runs the component function from top to bottom
- Logs help you understand the rendering order

### Exercise 5: Find and Modify a Prop

Let's find where a component is used and change its props.

**Step 1**: Open `/app/src/components/HowItWorks.tsx`

**Step 2**: Around line 44, find the section title:

```tsx
<h2 className="scroll-animate font-sans text-3xl font-bold tracking-tight text-foreground sm:text-4xl">
  From Daily Texts to a Weekly Love Letter
</h2>
```

**Step 3**: Change the text to:

```tsx
<h2 className="scroll-animate font-sans text-3xl font-bold tracking-tight text-foreground sm:text-4xl">
  How LoveNotes Works
</h2>
```

**Step 4**: Save and view the change in the browser

**Step 5**: Now let's change one of the step descriptions. Find line 121 (the first step):

```tsx
<p className="mt-4 text-lg text-muted-foreground pl-[4.75rem]">
  A gentle, science-backed question arrives by text each day. No app to download, no login to remember.
</p>
```

**Step 6**: Change it to emphasize simplicity:

```tsx
<p className="mt-4 text-lg text-muted-foreground pl-[4.75rem]">
  A thoughtful question arrives via SMS each day. No app download required—just text back when you're ready.
</p>
```

**Success criteria**: The "How It Works" section now shows your updated text.

**What you learned**: Components are just functions that return JSX. Text is just data. Change the data, change the output.

## Troubleshooting

### Problem: "My changes aren't showing up"

**Solutions**:
1. Make sure you saved the file (`Cmd + S` or `Ctrl + S`)
2. Check the terminal for error messages (the dev server will show compile errors)
3. Try a hard refresh in the browser (`Cmd + Shift + R` or `Ctrl + Shift + F5`)
4. Restart the dev server (Ctrl + C, then `npm run dev` again)

### Problem: "I see TypeScript errors in VS Code"

**Example**: Red squiggly lines under code

**Solutions**:
1. Hover over the error to read the message
2. Common issue: Typo in a prop name (e.g., `varient` instead of `variant`)
3. Common issue: Passing wrong type (e.g., `size={10}` instead of `size="lg"`)
4. If the error persists but the code works, restart VS Code's TypeScript server:
   - `Cmd + Shift + P` → "TypeScript: Restart TS Server"

### Problem: "I don't understand the className values"

**Example**: `className="inline-flex items-center justify-center gap-2"`

**Explanation**: These are Tailwind CSS utility classes. Each class is a small CSS rule:
- `inline-flex` → `display: inline-flex`
- `items-center` → `align-items: center`
- `gap-2` → `gap: 0.5rem`

You don't need to memorize them. Just know they're styling. Use the [Tailwind docs](https://tailwindcss.com/docs) as reference.

### Problem: "What does `{...props}` mean?"

**Explanation**: It's the **spread operator**. It passes all remaining props to the child component.

**Example**:
```tsx
<Button variant="outline" size="lg" onClick={handleClick} disabled>
  Click me
</Button>
```

Inside the Button component:
```tsx
const Button = ({ variant, size, ...props }) => {
  // variant = "outline"
  // size = "lg"
  // props = { onClick: handleClick, disabled: true }

  return <button {...props}>...</button>;
};
```

`{...props}` expands to `onClick={handleClick} disabled={true}` on the actual `<button>` element.

## Key Takeaways

✅ **Components are functions** that return JSX (JavaScript + HTML)
✅ **Props flow downward** from parent to child components
✅ **JSX looks like HTML** but uses `className`, self-closing tags, and `{}` for expressions
✅ **TypeScript adds types** to catch errors before runtime
✅ **useEffect runs after render** for setup, subscriptions, and side effects
✅ **Console logs are essential** for understanding component behavior
✅ **Component composition** builds complex UIs from simple, focused pieces

## What's Next

In **Module 3**, we'll dive into Supabase - the backend that powers LoveNotes. You'll learn how to query the database, understand Row Level Security (RLS), and trace how user data loads from the database into React components.

**Preview**: We'll query the database from the browser console, trace authentication flow, and see how React Query caches data to improve performance.

## Further Exploration

**Challenge 1: Create a Custom Component**

Create a new file `/app/src/components/CustomBanner.tsx`:

```tsx
const CustomBanner = () => {
  return (
    <div className="bg-primary text-primary-foreground p-4 text-center">
      <p className="font-bold">Custom Banner Component</p>
    </div>
  );
};

export default CustomBanner;
```

Then import and use it in `Index.tsx`:
```tsx
import CustomBanner from "@/components/CustomBanner";

// ... in the return statement:
<CustomBanner />
```

**Challenge 2: Add Props to Your Component**

Modify `CustomBanner` to accept props:

```tsx
interface CustomBannerProps {
  message: string;
  backgroundColor?: string; // Optional prop
}

const CustomBanner = ({ message, backgroundColor = "bg-primary" }: CustomBannerProps) => {
  return (
    <div className={`${backgroundColor} text-primary-foreground p-4 text-center`}>
      <p className="font-bold">{message}</p>
    </div>
  );
};
```

Use it with different props:
```tsx
<CustomBanner message="Welcome!" />
<CustomBanner message="Special Offer" backgroundColor="bg-destructive" />
```

**Challenge 3: Add State to a Component**

Import `useState` and create a counter:

```tsx
import { useState } from "react";

const CustomBanner = ({ message }: CustomBannerProps) => {
  const [count, setCount] = useState(0);

  return (
    <div className="bg-primary text-primary-foreground p-4 text-center">
      <p className="font-bold">{message}</p>
      <p>Clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
```

**Challenge 4: Explore React DevTools**

Install the React DevTools browser extension:
- [Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
- [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)

Open DevTools → Components tab. Click on components in the tree to inspect their props and state.

**Challenge 5: Trace Props Flow**

Pick a component (e.g., `SignupForm`) and:
1. Find where it's imported and used (hint: `Index.tsx`)
2. Check if it receives any props
3. Look inside the component to see how those props are used

**Map the flow**: Parent defines props → passes to child → child uses props to render

---

**Ready for Module 3?** Make sure you're comfortable modifying components, passing props, and using console logs. The next module assumes you can read and understand React code confidently.
