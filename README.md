# NextStep AI — Your AI-Powered Career Coach

NextStep AI is a full-stack web application that uses Google's Gemini AI to help job seekers accelerate their career growth. It provides personalized resume building, AI-generated cover letters, mock interview practice, and live industry insights — all tailored to the user's specific industry and skill set.

---

## Features

- **AI-Powered Career Dashboard** — Get real-time industry insights including salary ranges, demand levels, market outlook, growth rates, top skills, and key trends. Insights are automatically refreshed weekly via a background job.
- **Smart Resume Builder** — Build a Markdown-based resume with an in-browser editor. Get an ATS compatibility score and AI-generated feedback to improve your chances of passing automated screening.
- **AI Cover Letter Generator** — Generate tailored cover letters for specific companies and job titles. Manage multiple drafts and export them as PDFs.
- **Mock Interview Practice** — Take role-specific, AI-generated quizzes (10 multiple-choice questions per session). Receive an immediate score, per-question explanations, and an AI-generated improvement tip based on your wrong answers.
- **Performance Tracking** — View your quiz history in an interactive chart to monitor skill progression over time.
- **Onboarding Flow** — Set your industry, years of experience, bio, and skills on first sign-in to unlock personalised AI outputs across the entire app.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 15 (App Router, Turbopack) |
| UI | Tailwind CSS, shadcn/ui, Radix UI |
| Auth | Clerk |
| Database | PostgreSQL (Neon DB) via Prisma ORM |
| AI | Google Gemini 1.5 Flash (`@google/generative-ai`) |
| Background Jobs | Inngest (weekly cron for industry insight refresh) |
| Forms | React Hook Form + Zod |
| Charts | Recharts |
| PDF Export | html2pdf.js |
| Markdown Editor | @uiw/react-md-editor |

---

## Project Structure

```
├── app/
│   └── (auth)/             # Clerk sign-in / sign-up pages
├── (main)/                 # Protected app routes
│   ├── dashboard/          # Industry insights dashboard
│   ├── resume/             # Resume builder
│   ├── ai-cover-letter/    # Cover letter generator & list
│   ├── interview/          # Mock interview quizzes & stats
│   └── onboarding/         # First-time user setup
├── actions/                # Next.js Server Actions
│   ├── user.js             # Profile & onboarding
│   ├── dashboard.js        # AI insight generation
│   ├── interview.js        # Quiz generation & results
│   ├── resume.js           # Resume CRUD & ATS scoring
│   └── cover-letter.js     # Cover letter CRUD
├── components/             # Shared UI components
├── data/                   # Static data (features, FAQs, industries, testimonials)
├── lib/
│   ├── prisma.js           # Prisma client singleton
│   ├── inngest/            # Background job client & functions
│   └── schema.js           # Zod validation schemas
├── prisma/
│   ├── schema.prisma       # Database models
│   └── migrations/         # Migration history
└── middleware.js           # Clerk auth middleware (route protection)
```

---

## Getting Started

### Prerequisites

- Node.js 18+
- A PostgreSQL database (e.g. [Neon](https://neon.tech))
- A [Clerk](https://clerk.com) account
- A [Google AI Studio](https://aistudio.google.com) API key (Gemini)
- An [Inngest](https://inngest.com) account (for background jobs, optional in dev)

### 1. Clone the repository

```bash
git clone https://github.com/your-username/nextstep-ai.git
cd nextstep-ai
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a `.env` file in the project root with the following variables:

```env
# Database
DATABASE_URL=

# Clerk Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=

# Clerk redirect URLs
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/onboarding
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/onboarding

# Google Gemini AI
GEMINI_API_KEY=
```

### 4. Set up the database

Run Prisma migrations to create all the necessary tables:

```bash
npx prisma migrate deploy
```

To explore your database visually:

```bash
npx prisma studio
```

### 5. Start the development server

```bash
npm run dev
```

The app will be available at [http://localhost:3000](http://localhost:3000).

---

## Background Jobs (Inngest)

Industry insights are automatically regenerated every Sunday at midnight using an Inngest cron function. To run Inngest locally, start the Inngest dev server alongside the Next.js app:

```bash
npx inngest-cli@latest dev
```

The Inngest route is served at `/api/inngest`.

---

## Database Schema

The app uses five Prisma models:

- **User** — Stores profile info (industry, bio, skills, experience) linked to a Clerk user ID.
- **Assessment** — Records each quiz attempt with per-question results, a score, and an AI improvement tip.
- **Resume** — One resume per user, stored as Markdown with an ATS score and AI feedback.
- **CoverLetter** — Multiple cover letters per user, each linked to a specific company and job title.
- **IndustryInsight** — Cached AI-generated market data per industry (salary ranges, growth rate, top skills, key trends), refreshed weekly.

---

## Available Scripts

```bash
npm run dev        # Start development server with Turbopack
npm run build      # Create a production build
npm run start      # Start the production server
npm run lint       # Run ESLint
```

---

## Screenshot
<img width="1894" height="707" alt="Screenshot 2025-12-09 161305" src="https://github.com/user-attachments/assets/40147554-607e-4a2c-83c5-21a8f4ab319e" />
<img width="1891" height="833" alt="Screenshot 2025-12-09 161327" src="https://github.com/user-attachments/assets/93d2222b-f87a-4ee6-93bc-85cada77fc0a" />
<img width="1891" height="814" alt="Screenshot 2025-12-09 161511" src="https://github.com/user-attachments/assets/1d22ee6d-bb51-425a-bee3-ab23eac442b4" />
<img width="1887" height="815" alt="Screenshot 2025-12-09 161932" src="https://github.com/user-attachments/assets/3aef5e72-a89e-4ddf-8b4a-61673993d803" />
<img width="1892" height="828" alt="Screenshot 2025-12-09 162032" src="https://github.com/user-attachments/assets/b427da45-dd79-4c2c-ab6d-92762f48ff40" />
<img width="1891" height="822" alt="Screenshot 2025-12-09 162116" src="https://github.com/user-attachments/assets/d47ed3af-52bb-41b4-a7e4-c3e525b9564c" />
<img width="1318" height="813" alt="Screenshot 2025-12-09 163038" src="https://github.com/user-attachments/assets/a8303cef-fbb9-4e1a-909e-31b84067fa8e" />
<img width="1888" height="827" alt="Screenshot 2026-05-14 143157" src="https://github.com/user-attachments/assets/90488a74-6a39-4376-a61a-84b693210df1" />
<img width="1884" height="831" alt="Screenshot 2025-12-13 152404" src="https://github.com/user-attachments/assets/36a67198-5b3a-4b4a-8e1f-6f7e2df4c6de" />
<img width="1883" height="818" alt="Screenshot 2025-12-13 152420" src="https://github.com/user-attachments/assets/6891bd20-a025-4837-bc46-6435db0d4b07" />
<img width="846" height="699" alt="Screenshot 2026-05-14 142908" src="https://github.com/user-attachments/assets/43845b47-81d7-48b8-b9c2-f2e582da285c" />
<img width="1882" height="827" alt="Screenshot 2026-05-14 142956" src="https://github.com/user-attachments/assets/84137ab4-5231-4e9a-9db9-b9861559c5d3" />
<img width="1245" height="745" alt="Screenshot 2026-05-14 143031" src="https://github.com/user-attachments/assets/7843ba80-f8c1-497a-8654-f3e2db025925" />
<img width="1881" height="793" alt="Screenshot 2026-05-14 143102" src="https://github.com/user-attachments/assets/1e0f54d3-bd5b-4357-9e84-d07df3e23224" />

---

## Deployment

This app can be deployed to [Vercel](https://vercel.com) with zero configuration. Make sure to add all environment variables from your `.env` file to your Vercel project settings before deploying.

For the database, [Neon](https://neon.tech) is recommended as it provides a serverless PostgreSQL database with a generous free tier that pairs well with Vercel's edge network.
