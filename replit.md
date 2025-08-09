# Global Eco Footprint Atlas - Environmental Impact Tracking Application

## Overview

This is a comprehensive environmental impact tracking application built with React, Express, and PostgreSQL. The application allows users to explore global environmental data, calculate their personal carbon footprint, read environmental stories from around the world, and track their progress through a personal dashboard. The app integrates real environmental data concepts and provides an interactive user experience for environmental awareness and action.

## User Preferences

Preferred communication style: Simple, everyday language.

## Recent Changes (Latest Updates)

**August 6, 2025 - Source Code Documentation and Enhanced Features**
- ✅ Created comprehensive SOURCE_CODE_BY_PAGES.md with complete code organization
- ✅ Updated favicon from earth globe to clean leaf design for focused environmental branding
- ✅ Added story submission feature allowing users to submit environmental stories
- ✅ Implemented moderation system with "pending review" status and security check messaging
- ✅ Enhanced Stories page with professional submission form and validation
- ✅ Users receive confirmation: "Story submitted successfully, will be published after security check"
- ✅ Complete backend API support for story submission with proper error handling

**August 5, 2025 - Production Ready with Presentation Documentation**
- ✅ Created PRESENTATION_SOURCE_CODE.md with strategic code explanations for presentations
- ✅ Added one-line explanations for key code sections someone might ask about
- ✅ Included technical decision rationale and implementation details
- ✅ Added animated preloader with environmental themes (Globe, Leaf, Recycle icons)
- ✅ Integrated progressive loading states with contextual messages
- ✅ Created NETLIFY_DEPLOYMENT_STEPS.md with complete deployment guide
- ✅ Built production-ready dist/public folder with all updates included
- ✅ Comprehensive environmental data for 190+ countries worldwide
- ✅ Real CO₂ emissions per capita data from Our World in Data (2023)
- ✅ Real renewable energy percentages from IRENA 2024 statistics
- ✅ Updated all website references from "over 200 countries" to "190+ countries" for accuracy

**August 4, 2025 - Deployment Health Check Issue Analysis and Fix**
- ✅ Enhanced health check endpoints with comprehensive diagnostic information (uptime, port, environment)
- ✅ Added simple ping endpoints (`/ping`, `/api/ping`) for basic connectivity testing
- ✅ Identified root cause of deployment health check failures: multiple port configurations in .replit file
- ✅ Created comprehensive DEPLOYMENT_FIX.md guide with step-by-step solutions
- ✅ Verified all health check endpoints return proper 200 status codes in both development and production
- ✅ Confirmed server configuration is correct (0.0.0.0 binding, PORT variable usage)
- 🔧 **Action Required**: Remove second port configuration (5001/3000) from .replit file via Replit interface
- 🔧 **Action Required**: Fix deployment run command to use "npm start" instead of "npm run build"

**August 4, 2025 - Production Deployment Fixes**
- ✅ Added dedicated health check endpoints (`/health` and `/api/health`) that return 200 status codes
- ✅ Fixed production server startup by ensuring proper build configuration 
- ✅ Server correctly listens on port 5000 with host 0.0.0.0 for deployment compatibility
- ✅ Build process generates optimized production bundle with static file serving
- ✅ Health check endpoints provide JSON responses with status, message, timestamp, and environment info
- ✅ Production build tested successfully - root endpoint serves React app, health checks respond with 200 status
- ✅ All deployment requirements satisfied for Replit production deployment

**August 4, 2025 - Real Environmental Stories Integration**
- ✅ Replaced fictional stories with authentic environmental success stories based on 2024 research
- ✅ Added real data from Kenya's KOSAP solar project (₹5.8 billion, 75% rural electrification)
- ✅ Included Gotham Greens' urban farming success (₹2.7 billion revenue, 100M lettuce heads annually)
- ✅ Featured Manila Bay restoration (280,000 tons waste removed, 74,075 volunteers)
- ✅ Added Copenhagen's green roof mandate (72.6% CO2 reduction, 200,000 sq meters vegetation)
- ✅ Created professional SVG illustrations that match the real story content and environmental themes
- ✅ Fixed image display issues with properly formatted URL-encoded SVG data
- ✅ All environmental stories now feature authentic data with measurable impact metrics

**January 31, 2025 - Complete Feature Enhancement and Localization**
- ✅ Changed currency from $ to ₹ (rupees) and distance units from miles to kilometers
- ✅ Fixed world map "More Filters" button with advanced filtering dialog (population, CO₂, renewable energy ranges)
- ✅ Expanded country data to 190+ countries with authentic 2023-2024 environmental data
- ✅ Set dark theme as default instead of system theme
- ✅ Added validation warnings for empty calculator inputs with user-friendly alerts
- ✅ Created comprehensive SOURCE_CODE_DOCUMENTATION.md file for developers
- ✅ All features fully functional with enhanced user experience

**January 30, 2025 - Production Ready Netlify Deployment**
- ✅ Removed sample data, implemented real user analytics tracking via localStorage
- ✅ Removed dashboard page completely from navigation and routes  
- ✅ Added smooth navigation transitions with hover scale effects
- ✅ Enhanced calculator with personalized carbon reduction tips
- ✅ Implemented real-time analytics that update every 10 seconds
- ✅ Added comprehensive dark/light mode toggle with system preference detection
- ✅ Created production-ready build configuration for Netlify deployment
- ✅ All files organized for zero-configuration deployment

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript for type safety and modern React features
- **Build Tool**: Vite for fast development and optimized production builds
- **Routing**: Wouter for lightweight client-side routing (configured but not yet implemented)
- **State Management**: TanStack Query (React Query) for server state management and caching
- **UI Framework**: shadcn/ui components built on Radix UI primitives for accessibility
- **Styling**: Tailwind CSS with CSS variables for theming and dark mode support
- **Form Handling**: React Hook Form with Hookform resolvers for validation
- **Charts**: Chart.js for data visualization capabilities

### Backend Architecture
- **Runtime**: Node.js with Express.js framework
- **Database**: PostgreSQL with Neon serverless provider
- **ORM**: Drizzle ORM for type-safe database queries and schema management
- **Authentication**: Session-based with connect-pg-simple for PostgreSQL session storage
- **API Design**: RESTful API endpoints with /api prefix
- **Validation**: Shared Zod schemas between frontend and backend

### Development Setup
- **Package Manager**: npm with ES modules
- **TypeScript**: Strict configuration across client, server, and shared code
- **Hot Reload**: Vite HMR for frontend, tsx for backend development
- **Path Mapping**: Clean imports using @ aliases (@/, @shared/, @assets/)
- **Build Process**: Vite for frontend bundling, esbuild for backend production builds

## Key Components

### Database Schema (shared/schema.ts)
Comprehensive environmental tracking system:
- **Users**: User profiles with gamification (levels, experience points)
- **Footprint Calculations**: Detailed carbon footprint data with breakdown by category
- **Stories**: Environmental stories from different countries with engagement metrics
- **Achievements**: User achievement system for motivation and engagement
- **Environmental Data**: Real-world environmental statistics by country and year
- **Global Stats**: Aggregated environmental data for dashboard insights
- **Newsletter Subscriptions**: Email subscription management

The schema uses Drizzle ORM with PostgreSQL dialect and supports complex environmental data tracking.

### Storage Interface (server/storage.ts)
- **Abstraction Layer**: IStorage interface defines CRUD operations
- **In-Memory Implementation**: MemStorage class for development/testing
- **Database Ready**: Structured to easily swap to Drizzle database implementation

### Frontend Structure
- **Pages**: Complete application with Home, Calculator, World Map, Stories, and Dashboard
- **Navigation**: Responsive navigation with mobile sheet menu and active state indicators
- **Component Library**: Complete shadcn/ui component set with Radix UI primitives
- **Routing**: Wouter implementation with full client-side routing
- **Global State**: React Query client configured with custom fetch utilities
- **Theming**: CSS variables system supporting light/dark modes
- **Charts**: Interactive data visualization using Chart.js for environmental metrics

### API Layer
- **Request Utilities**: Custom fetch wrapper with error handling and credentials
- **Query Functions**: Reusable query functions with unauthorized behavior options
- **Logging**: Request/response logging middleware for API endpoints

## Data Flow

### Frontend to Backend
1. Frontend makes API requests using custom fetch utilities
2. Requests include credentials for session management
3. TanStack Query handles caching and state management
4. Responses are validated and typed using shared schemas

### Database Operations
1. Drizzle ORM provides type-safe database queries
2. Migrations managed through drizzle-kit
3. Schema changes tracked in ./migrations directory
4. Connection pooling handled by Neon serverless

### Authentication Flow
1. Session-based authentication using PostgreSQL session store
2. Middleware handles session validation
3. Protected routes check authentication status
4. User context maintained across requests

## External Dependencies

### Database Provider
- **Neon**: Serverless PostgreSQL hosting
- **Connection**: DATABASE_URL environment variable required
- **Features**: Automatic scaling, built-in connection pooling

### UI Components
- **Radix UI**: Accessible component primitives
- **Lucide React**: Icon library for consistent iconography
- **Class Variance Authority**: Component variant management

### Development Tools
- **Replit Integration**: Cartographer plugin for development environment
- **Runtime Error Modal**: Development error overlay
- **PostCSS**: CSS processing with Tailwind and Autoprefixer

## Deployment Strategy

### Build Process
1. **Frontend Build**: Vite builds optimized production bundle to dist/public
2. **Backend Build**: esbuild bundles server code to dist/index.js
3. **Database**: Drizzle migrations applied via `db:push` command
4. **Assets**: Static files served from dist/public

### Environment Configuration
- **Development**: NODE_ENV=development with hot reload
- **Production**: NODE_ENV=production with optimized builds
- **Database**: DATABASE_URL must be provided for both environments

### Scripts
- **dev**: Development server with hot reload (NODE_ENV=development tsx server/index.ts)
- **build**: Production build for both frontend and backend (vite build && esbuild server/index.ts)
- **start**: Production server startup (NODE_ENV=production node dist/index.js)
- **check**: TypeScript type checking
- **db:push**: Apply database schema changes

### Health Check Endpoints
- **GET /health**: Main health check endpoint returning 200 status with application status
- **GET /api/health**: API-specific health check endpoint for monitoring API functionality
- Both endpoints return JSON with status, message, timestamp, and environment information

### Production Deployment
The application is fully configured for production deployment:
- Server binds to 0.0.0.0:5000 (configurable via PORT environment variable)
- Static files served from dist/public directory
- Health check endpoints respond with proper 200 status codes
- Build process creates optimized bundles for both frontend and backend
- Compatible with cloud platforms including Replit Deployments

The application requires minimal configuration and can be deployed to any cloud platform supporting Node.js applications.