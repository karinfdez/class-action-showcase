# Class Action: Employment Litigation Management

[![Built with Next.js](https://img.shields.io/badge/Built%20with-Next.js-000000?style=flat-square&logo=next.js&logoColor=white)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-4.9-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Supabase](https://img.shields.io/badge/Supabase-Auth%20%26%20DB-38BDF8?style=flat-square&logo=supabase&logoColor=white)](https://supabase.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-3.3-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)

## Note  
This repository is a public showcase of a private project. The actual source code is private, but this outlines the architecture, technologies used, and demo links.


## DEMO

[Watch the full demo here](https://www.youtube.com/watch?v=nSMyOyMHcmA)

# Class Action: Employment Litigation Management

[![Built with Next.js](https://img.shields.io/badge/Built%20with-Next.js-000000?style=flat-square&logo=next.js&logoColor=white)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-4.9-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Supabase](https://img.shields.io/badge/Supabase-Auth%20%26%20DB-38BDF8?style=flat-square&logo=supabase&logoColor=white)](https://supabase.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-3.3-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![TanStack Query](https://img.shields.io/badge/TanStack%20Query-5.0-FF4154?style=flat-square&logo=react-query&logoColor=white)](https://tanstack.com/query)

**Note:**  
The application is privately hosted and not open for public access. For privacy and security reasons, I am providing a video demo below to showcase some of the platform's features and user experience. If you would like a private walkthrough, please contact me directly.

[Watch the full demo here](https://www.youtube.com/watch?v=nSMyOyMHcmA)


## Project Overview

Class Action is a multi-tenant web platform designed to identify, contact, and recruit potential clients for employment class action lawsuits. The system enables law firms to dynamically load and manage profiles of individuals based on their past job experience with specific companies, filter and search through these profiles, and reach out to them directly via email. This platform connects individuals affected by workplace violations with law firms handling relevant class action litigation, streamlining the process of finding and engaging qualified participants.

---

### Business Problem Solved

Law firms struggle to efficiently identify and engage potential clients who may qualify for employment class action lawsuits, especially those who worked for a specific company during a relevant time period. This platform bridges the gap between affected individuals and legal representation by:

- **Dynamic Profile Loading**: Fetches additional profiles on-demand from external APIs and seamlessly integrates them into the database
- **Real-time Data Management**: Uses React Query for efficient caching and automatic refetching without page reloads
- **Advanced Filtering & Search**: Server-side filtering and sorting via API endpoints for optimal performance
- **Profile Discovery**: Organizes profiles of people who have previously worked for the analyzed (target) company
- **Flexible Sorting**: Sort profiles alphabetically or by creation date
- **Targeted Outreach**: Connects affected individuals with appropriate legal representation through customized email communication
- **Automated Communication**: AI-powered email templates via Cloudflare Workers to inform potential clients of their legal options


## Screenshots

![Main Dashboard](./screenshots/dashboard.png)
![Profile Search](./screenshots/profile-search.png)
![Email Service](./screenshots/email-service.png)

---

## 🛠️ Technology Stack

### Frontend
- **Framework**: Next.js 14 (React 18) with App Router
- **Language**: TypeScript
- **Styling**: Tailwind CSS with custom components
- **State Management**: React Hooks and Jotai for global state
- **Data Fetching**: TanStack Query (React Query) for server state management
- **UI Components**: Radix UI primitives
- **Tables**: TanStack React Table

### Backend & Infrastructure
- **Authentication**: Supabase Auth with Google OAuth
- **Database**: Supabase PostgreSQL with indexed queries
- **API Routes**: Next.js API routes for server-side data fetching
- **Email Service**: Custom email dispatcher via Cloudflare Workers
- **External APIs**: Integration with profile data providers
- **Deployment**: Netlify with CI/CD pipeline


## Data Flow Architecture

### Profile Management System

The application uses a hybrid approach for optimal performance:

**Server-Side (Initial Load)**
1. Next.js server fetches all profiles for a company from Supabase
2. Passes initial data to client as `initialData` for React Query
3. Provides instant page load with pre-rendered content

**Client-Side (Dynamic Updates)**
1. **React Query** manages profile data with automatic caching
2. **Load More**: Fetches additional profiles from external API → saves to Supabase → invalidates cache → refetches all profiles
3. **Filtering & Sorting**: Server-side processing via API with query parameters (name, email, location, sort order)
4. **Cache Management**: 5-minute stale time with manual invalidation on mutations

**API Routes**
- `GET /api/companies/[slug]/profiles` - Fetches and filters profiles by company
- Accepts query parameters for search and sort
- Uses Supabase indexes for optimized queries (`company_id`, `full_name`, `email`, `location`)
- Currently returns up to 50 profiles (pagination in progress)

### Key Features

- **No Page Reloads**: React Query handles all data fetching and updates
- **Server-Side Filtering**: Efficient filtering using database indexes
- **Smart Caching**: Reduces API calls while keeping data fresh
- **Real-time Notifications**: Success/error feedback after mutations

## Application Structure

```
app/
├── (auth)/              # Authentication routes and components
├── (main)/              # Main application pages
│   ├── cases/           # Case management and company views
│   │   └── [name]/      # Dynamic company profile pages
│   └── teams/           # Team collaboration features
├── api/                 # Next.js API routes
│   └── companies/       # Company and profile endpoints
├── components/          # Reusable UI components
│   ├── ui/              # Base UI components (Radix UI)
│   ├── CompanyProfiles/ # Profile table and management
│   └── LoadMoreProfiles.tsx # Dynamic profile loading
├── lib/                 # Client-side utilities
│   └── fetchCompaniesProfiles.ts # React Query fetcher
├── utils/supabase/      # Supabase utilities and data layer
│   └── data/            # Database query functions
├── helpers/             # Business logic and filters
└── types/               # TypeScript type definitions
```

## Getting Started

```bash
# Install dependencies
npm install

# Run development server
npm run dev

# Open in browser
open http://localhost:3000
```

## Key Libraries & Tools

- **Data Fetching**: TanStack Query (React Query) for server state management and caching
- **Data Tables**: TanStack React Table for advanced table features
- **UI Components**: Radix UI (Dialog, Dropdown, Tabs, Checkbox, etc.)
- **Form Handling**: React Hook Form with Zod validation
- **Date Handling**: date-fns
- **Animations**: Framer Motion
- **Database Indexes**: Optimized Supabase queries with custom indexes on `company_id`, `full_name`, `email`, and `location`

## 🔗 Design Resources

View the application wireframes and design system on [Figma](https://www.figma.com/board/0n73dQHwWePl8IaZ6UFjF3/LexQuery?node-id=0-1&t=yp5DYCHHaFFJGuM6-1)

## Roadmap

### Current Features ✅
- Dynamic profile loading with "Load More" functionality
- React Query integration with 5-minute cache for efficient data management
- Automatic cache revalidation on mutations using `revalidatePath`
- Client-side search and sorting (no date filtering)
- Secure API routes with Supabase Auth (httpOnly cookies)
- Email outreach system via Cloudflare Workers
- Page transition animations with Framer Motion

### In Progress 🚧
- Server-side filtering and sorting API endpoints
- Fetch limited profiles initially (50) for faster page loads
- Advanced pagination with offset/cursor support
