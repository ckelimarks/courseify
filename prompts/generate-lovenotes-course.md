# Generate Interactive Course: LoveNotes Codebase

Using the course generation framework in `codebase-course-prompt.md`, create an interactive learning course from the LoveNotes codebase.

## Target Codebase
- **Project**: LoveNotes (SMS-based relationship micro-ritual app)
- **Location**: `/Users/christopherk.marks/Downloads/personal-os-main/Projects/lovenotes/app/`
- **Repository**: github.com/ckelimarks/ease-empathy-flow
- **Tech Stack**: React 18 + TypeScript + Vite + Supabase + Twilio + Stripe

## Target Audience
Developers with little to no experience who want to understand:
- Modern React patterns (hooks, context, TypeScript)
- Supabase backend architecture (auth, database, edge functions)
- Third-party integrations (Twilio SMS, Stripe payments)
- Real-world production app patterns
- State machines and workflow orchestration

## Learning Objectives
By the end of this course, learners will understand:
1. How to build a full-stack React + Supabase application
2. SMS integration patterns with Twilio
3. Subscription payment flows with Stripe
4. Edge functions and serverless architecture
5. Database design for relationship data
6. State machine patterns for workflow management
7. Production considerations (error handling, webhooks, security)

## Course Scope
Generate **Modules 0-5** covering:

### Module 0: Getting Started with LoveNotes
- Environment setup (Node, Git, VS Code, Supabase CLI)
- Clone and run the project locally
- Understanding the project structure
- Using browser DevTools and React DevTools
- Your first code exploration

### Module 1: Project Overview - What is LoveNotes?
- User journey walkthrough (from signup to receiving prompts)
- System architecture at a high level
- Key files and their roles
- How data flows from user → SMS → database → AI → response
- Following one complete feature (e.g., sending a daily prompt)

### Module 2: React Fundamentals in Practice
- Component structure (using actual LoveNotes components)
- Props and component composition
- Reading JSX and TypeScript
- Finding components and tracing renders
- **Exercise**: Modify the home page button text
- **Exercise**: Add a console.log to track navigation

### Module 3: Understanding Supabase Backend
- What is Supabase? (Backend-as-a-Service explained)
- Database tables and relationships (couples, profiles, phone_subscriptions)
- Supabase client setup in React
- Row Level Security (RLS) policies
- **Exercise**: Query the database from browser console
- **Exercise**: Trace how user data loads on login

### Module 4: The SMS Flow - Twilio Integration
- How SMS prompts are sent (edge function walkthrough)
- Twilio webhook for receiving responses
- Message routing and response matching
- The state machine (idle → prime_sent → main_sent)
- **Exercise**: Follow a prompt from cron trigger to SMS delivery
- **Exercise**: Trace how a user's SMS response gets stored

### Module 5: Edge Functions - Serverless API Endpoints
- What are edge functions? (Deno runtime explained)
- Key functions: daily-prompts, send-sms, twilio-webhook
- Environment variables and secrets
- Testing functions locally
- **Exercise**: Add logging to see when daily-prompts runs
- **Exercise**: Trigger send-sms manually with a test couple

## Requirements for Each Module

Follow the template in `codebase-course-prompt.md`:

✅ **Complete setup instructions** for every hands-on exercise
✅ **Actual code references** with file paths and line numbers
✅ **Beginner-friendly explanations** (define all jargon)
✅ **Progressive difficulty** (each builds on previous)
✅ **Safe practice environment** (use branches, don't modify original)
✅ **Clear success criteria** ("You'll know it works when...")
✅ **Troubleshooting sections** for common issues
✅ **Key takeaways** summarizing what was learned

## Special Considerations

### For Module 0 (Setup):
- LoveNotes repo is at `Projects/lovenotes/app/` (not root)
- Need Supabase CLI for local development
- Environment variables required (.env.local setup)
- May need to use mock data to avoid requiring full Twilio/Stripe setup

### For Module 1 (Overview):
- Include the state machine diagram from technical.md
- Show the ER diagram for database schema
- Walk through one complete user flow with mermaid sequence diagram

### For Module 3 (Supabase):
- Explain Row Level Security (RLS) - critical for multi-tenant data
- Show how to use Supabase Studio (local dashboard)
- Demonstrate real-time subscriptions (if used in codebase)

### For Module 4 (SMS/Twilio):
- Explain webhook security (signature verification)
- Show how phone number normalization works
- Trace the "smart pairing" algorithm for matching responses to prompts

### For Module 5 (Edge Functions):
- Explain Deno vs Node.js
- Show how to test functions locally with `supabase functions serve`
- Demonstrate viewing logs with `supabase functions logs`

## Output Format

For each module, generate:

```markdown
# Module [N]: [Title]

**Estimated time**: [X] minutes
**Prerequisites**: [List previous modules]
**What you'll build/learn**: [Concrete outcome]

## Overview
[What this module covers and why it matters]

## Concepts
[2-3 key concepts explained simply]

## Code Walkthrough
[Actual code from LoveNotes with annotations]

## Try It Yourself
[Complete hands-on exercise with setup instructions]

## Key Takeaways
[Bullet points of what was learned]

## What's Next
[Preview of next module]

## Further Exploration
[Optional deeper dives into related code]
```

## Context Files to Reference

- `Projects/lovenotes/.claude/technical.md` - Architecture, tech stack, database schema
- `Projects/lovenotes/app/src/` - React frontend code
- `Projects/lovenotes/app/supabase/functions/` - Edge functions
- `Projects/lovenotes/app/supabase/migrations/` - Database schema

## Begin Generation

Create Modules 0-5 following the framework. Make them practical, beginner-friendly, and grounded in real LoveNotes code.
