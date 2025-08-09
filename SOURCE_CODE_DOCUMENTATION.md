# Global Eco Footprint Atlas - Source Code Documentation

## Project Overview

The Global Eco Footprint Atlas is a comprehensive environmental impact tracking application that allows users to calculate their carbon footprint, explore global environmental data, and read inspiring environmental stories from around the world.

## Technology Stack

### Frontend
- **React 18** with TypeScript for type safety and modern React features
- **Vite** for fast development and optimized production builds
- **Wouter** for lightweight client-side routing
- **TanStack Query (React Query)** for server state management and caching
- **shadcn/ui** components built on Radix UI primitives for accessibility
- **Tailwind CSS** with CSS variables for theming and dark mode support
- **React Hook Form** with Hookform resolvers for form validation
- **Chart.js** for data visualization capabilities

### Backend
- **Node.js** with Express.js framework
- **PostgreSQL** with Neon serverless provider (configured but using in-memory storage for demo)
- **Drizzle ORM** for type-safe database queries and schema management
- **Session-based authentication** with connect-pg-simple for PostgreSQL session storage
- **Zod** schemas for validation between frontend and backend

### Build & Development
- **TypeScript** strict configuration across client, server, and shared code
- **Vite HMR** for frontend hot reload, tsx for backend development
- **Path mapping** with @ aliases (@/, @shared/, @assets/)
- **ESBuild** for backend production builds

## Project Structure

```
/
├── client/                 # Frontend React application
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   │   ├── ui/         # shadcn/ui components
│   │   │   ├── navigation.tsx
│   │   │   └── theme-provider.tsx
│   │   ├── pages/          # Application pages
│   │   │   ├── home.tsx    # Landing page with analytics
│   │   │   ├── calculator.tsx  # Carbon footprint calculator
│   │   │   ├── world-map.tsx   # Global environmental data
│   │   │   ├── stories.tsx     # Environmental stories
│   │   │   └── not-found.tsx   # 404 page
│   │   ├── hooks/          # Custom React hooks
│   │   │   ├── use-analytics.ts
│   │   │   └── use-toast.ts
│   │   ├── lib/            # Utility libraries
│   │   │   └── queryClient.ts
│   │   ├── utils/          # Helper utilities
│   │   │   └── carbon-tips.ts
│   │   └── main.tsx        # React app entry point
│   ├── public/             # Static assets
│   │   ├── favicon.svg
│   │   └── _redirects      # Netlify routing configuration
│   └── index.html          # HTML template
├── server/                 # Backend Express application
│   ├── index.ts            # Main server file
│   ├── routes.ts           # API route definitions
│   ├── storage.ts          # Data storage interface
│   └── vite.ts             # Vite server integration
├── shared/                 # Shared types and schemas
│   └── schema.ts           # Database schema and Zod validators
├── dist/                   # Build output directory
│   ├── index.js            # Built server bundle
│   └── public/             # Built frontend assets (for Netlify)
├── package.json            # Dependencies and npm scripts
├── vite.config.ts          # Vite build configuration
├── tailwind.config.ts      # Tailwind CSS configuration
├── netlify.toml            # Netlify deployment configuration
└── tsconfig.json           # TypeScript configuration
```

## Key Features

### 1. Carbon Footprint Calculator
- **Location**: `client/src/pages/calculator.tsx`
- **Features**:
  - Multi-step form with validation
  - Transportation, energy, food, and consumption categories
  - Personalized reduction tips based on user inputs
  - Real-time calculation with local storage tracking
  - Results with detailed breakdown by category

### 2. Global Environmental Data Explorer
- **Location**: `client/src/pages/world-map.tsx`
- **Features**:
  - Search functionality across 30+ countries
  - Advanced filtering with sliders for population, CO₂, and renewable energy
  - Regional filtering (Asia, Europe, Africa, etc.)
  - Interactive country selection with detailed statistics
  - Multiple metrics: CO₂ emissions, renewable energy percentage, population

### 3. Environmental Stories
- **Location**: `client/src/pages/stories.tsx`
- **Features**:
  - Curated environmental success stories from around the world
  - Category filtering (Renewable Energy, Ocean Conservation, etc.)
  - Country-based filtering
  - Custom SVG illustrations for each story
  - Reading time estimates and engagement metrics

### 4. Real-time Analytics Dashboard
- **Location**: `client/src/pages/home.tsx`
- **Features**:
  - Live user activity tracking via localStorage
  - Updates every 10 seconds with simulated real-time data
  - Total users, active users, daily visitors, calculations completed
  - CO₂ savings tracking from user actions

### 5. Dark/Light Theme System
- **Location**: `client/src/components/theme-provider.tsx`
- **Features**:
  - System preference detection
  - Default dark theme (as requested)
  - Persistent theme storage
  - CSS variables for consistent theming

## API Endpoints

The application uses a storage interface pattern that can work with both in-memory storage (current demo) and database storage:

### Storage Interface (`server/storage.ts`)
```typescript
interface IStorage {
  // User management
  createUser(user: InsertUser): Promise<User>;
  getUserByEmail(email: string): Promise<User | null>;
  
  // Footprint calculations
  createFootprintCalculation(calc: InsertFootprintCalculation): Promise<FootprintCalculation>;
  getFootprintCalculationsByUserId(userId: number): Promise<FootprintCalculation[]>;
  
  // Stories management
  getStories(): Promise<Story[]>;
  getStoriesByCountry(country: string): Promise<Story[]>;
  createStory(story: InsertStory): Promise<Story>;
}
```

### API Routes (`server/routes.ts`)
- `GET /api/users` - Get all users
- `POST /api/users` - Create new user
- `GET /api/footprint-calculations` - Get calculations for authenticated user
- `POST /api/footprint-calculations` - Create new calculation
- `GET /api/stories` - Get all stories with optional country filter

## Database Schema

### Core Tables (`shared/schema.ts`)
```typescript
// Users table with gamification
users: {
  id: serial().primaryKey(),
  email: varchar().notNull().unique(),
  username: varchar().notNull(),
  hashedPassword: varchar().notNull(),
  level: integer().default(1),
  experiencePoints: integer().default(0),
  createdAt: timestamp().defaultNow()
}

// Carbon footprint calculations
footprintCalculations: {
  id: serial().primaryKey(),
  userId: integer().references(() => users.id),
  transportationScore: numeric(),
  energyScore: numeric(),
  foodScore: numeric(),
  consumptionScore: numeric(),
  totalScore: numeric().notNull(),
  calculatedAt: timestamp().defaultNow()
}

// Environmental stories
stories: {
  id: serial().primaryKey(),
  title: varchar().notNull(),
  content: text().notNull(),
  country: varchar().notNull(),
  category: varchar().notNull(),
  imageUrl: varchar(),
  readTime: integer(),
  likes: integer().default(0),
  createdAt: timestamp().defaultNow()
}
```

## Build and Deployment

### Development
```bash
npm run dev        # Start development server
npm run check      # TypeScript type checking
```

### Production Build
```bash
npm run build      # Build both frontend and backend
```
- Frontend builds to `dist/public/` (ready for Netlify)
- Backend builds to `dist/index.js`

### Netlify Deployment
The application is configured for easy Netlify deployment:
- Upload contents of `dist/public/` folder
- Includes `_redirects` file for SPA routing
- `netlify.toml` provides build configuration

## Configuration Files

### Key Configuration
- **vite.config.ts**: Build configuration with path aliases and plugins
- **tailwind.config.ts**: CSS framework configuration with dark mode
- **netlify.toml**: Deployment configuration with redirects and headers
- **tsconfig.json**: TypeScript strict mode configuration

## Recent Updates (Latest Changes)

### January 31, 2025 - Major Improvements
1. **Currency & Units**: Changed from $ to ₹ and miles to kilometers
2. **World Map Enhancement**: Fixed "More Filters" with advanced filtering dialog
3. **Country Data**: Expanded from 10 to 30+ countries for better search functionality
4. **Story Images**: Added custom SVG illustrations for all environmental stories
5. **Theme**: Set dark mode as default theme
6. **Validation**: Added input validation warnings in calculator
7. **Documentation**: Created comprehensive source code documentation

## Development Guidelines

### Code Style
- Use TypeScript strict mode
- Follow React functional component patterns
- Implement proper error handling with try/catch
- Use shadcn/ui components for consistent design
- Maintain responsive design with Tailwind CSS

### State Management
- Use TanStack Query for server state
- Local state with useState for component state
- localStorage for user preferences and analytics
- Session-based authentication for user management

### Performance
- Vite for fast development builds
- Code splitting with dynamic imports
- Optimized images and assets
- Efficient re-rendering with React Query caching

This documentation provides a comprehensive overview of the Global Eco Footprint Atlas codebase, architecture, and implementation details for developers working on the project.