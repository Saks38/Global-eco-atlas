# Global Eco Footprint Atlas - Complete Source Code (Presentation Version)

## Overview
Environmental tracking web application with authentic data for 190+ countries, built with TypeScript, React, and Node.js.

---

## Frontend Components

### Main App Structure (`client/src/App.tsx`)
```typescript
import { Switch, Route } from "wouter";
import { QueryClientProvider } from "@tanstack/react-query";
import { Preloader } from "@/components/preloader";
import { useState, useEffect } from "react";

// Main application component with theme provider and routing setup
function App() {
  const [isLoading, setIsLoading] = useState(true);

  const handleLoadingComplete = () => {
    setIsLoading(false);
  };

  return (
    <ThemeProvider defaultTheme="dark" storageKey="eco-atlas-theme">
      <QueryClientProvider client={queryClient}>
        <Toaster />
        {/* Show preloader during app initialization, then main app */}
        {isLoading ? (
          <Preloader onComplete={handleLoadingComplete} />
        ) : (
          <Router />
        )}
      </QueryClientProvider>
    </ThemeProvider>
  );
}

// Router component defining all application pages
function Router() {
  return (
    <div>
      <Navigation />
      <Switch>
        <Route path="/" component={Home} />
        <Route path="/calculator" component={Calculator} />
        <Route path="/world-map" component={WorldMap} />
        <Route path="/stories" component={Stories} />
        <Route component={NotFound} />
      </Switch>
    </div>
  );
}
```

### Animated Preloader (`client/src/components/preloader.tsx`)
```typescript
import { useEffect, useState } from "react";
import { Globe, Leaf, Recycle } from "lucide-react";

interface PreloaderProps {
  onComplete: () => void;
}

export function Preloader({ onComplete }: PreloaderProps) {
  const [loadingProgress, setLoadingProgress] = useState(0);

  useEffect(() => {
    // Simulate realistic loading progress with random increments
    const interval = setInterval(() => {
      setLoadingProgress((prev) => {
        if (prev >= 100) {
          clearInterval(interval);
          setTimeout(() => onComplete(), 500);
          return 100;
        }
        return prev + Math.random() * 12; // Random progress increments
      });
    }, 100);

    return () => clearInterval(interval);
  }, [onComplete]);

  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center bg-gradient-to-br from-green-50 to-blue-50 dark:from-green-950 dark:to-blue-950">
      <div className="text-center space-y-8">
        {/* Three animated environmental icons with staggered bounce animation */}
        <div className="flex items-center justify-center space-x-6">
          <div className="animate-bounce delay-0">
            <Globe className="h-12 w-12 text-blue-600" />
          </div>
          <div className="animate-bounce delay-150">
            <Leaf className="h-12 w-12 text-green-600" />
          </div>
          <div className="animate-bounce delay-300">
            <Recycle className="h-12 w-12 text-purple-600" />
          </div>
        </div>

        {/* Dynamic title and subtitle */}
        <div className="space-y-2">
          <h1 className="text-4xl font-bold text-gray-800 dark:text-gray-200">
            Global Eco Footprint Atlas
          </h1>
          <p className="text-lg text-gray-600 dark:text-gray-400">
            Loading environmental data from 190+ countries worldwide
          </p>
        </div>

        {/* Animated progress bar with real-time percentage */}
        <div className="w-80 mx-auto space-y-2">
          <div className="w-full bg-gray-200 dark:bg-gray-700 rounded-full h-2">
            <div 
              className="bg-gradient-to-r from-green-500 to-blue-500 h-2 rounded-full transition-all duration-300 ease-out"
              style={{ width: `${loadingProgress}%` }}
            />
          </div>
          <p className="text-sm text-gray-500 dark:text-gray-400">
            {Math.round(loadingProgress)}% Complete
          </p>
        </div>

        {/* Contextual loading messages that change based on progress */}
        <div className="space-y-1">
          <p className="text-sm text-gray-600 dark:text-gray-400 animate-pulse">
            {loadingProgress < 30 && "Initializing environmental database..."}
            {loadingProgress >= 30 && loadingProgress < 60 && "Loading CO₂ emissions data..."}
            {loadingProgress >= 60 && loadingProgress < 90 && "Preparing renewable energy statistics..."}
            {loadingProgress >= 90 && "Almost ready!"}
          </p>
        </div>
      </div>
    </div>
  );
}
```

### Home Page (`client/src/pages/home.tsx`)
```typescript
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card";
import { BarChart3, Globe, Calculator, BookOpen } from "lucide-react";
import { Link } from "wouter";

export default function Home() {
  return (
    <div className="min-h-screen bg-gradient-to-br from-green-50 to-blue-50 dark:from-green-950 dark:to-blue-950">
      {/* Hero section with main call-to-action */}
      <section className="container mx-auto px-4 py-16 text-center">
        <div className="max-w-4xl mx-auto space-y-8">
          <h1 className="text-5xl md:text-6xl font-bold bg-gradient-to-r from-green-600 to-blue-600 bg-clip-text text-transparent">
            Global Eco Footprint Atlas
          </h1>
          <p className="text-xl text-gray-600 dark:text-gray-300 max-w-2xl mx-auto">
            Track your environmental impact, explore global climate data from 190+ countries, 
            and discover actionable insights for a sustainable future.
          </p>
          <div className="flex flex-col sm:flex-row gap-4 justify-center">
            <Link href="/calculator">
              <Button size="lg" className="bg-green-600 hover:bg-green-700">
                <Calculator className="mr-2 h-5 w-5" />
                Calculate My Footprint
              </Button>
            </Link>
            <Link href="/world-map">
              <Button size="lg" variant="outline">
                <Globe className="mr-2 h-5 w-5" />
                Explore World Data
              </Button>
            </Link>
          </div>
        </div>
      </section>

      {/* Feature cards showcasing main application capabilities */}
      <section className="container mx-auto px-4 py-16">
        <h2 className="text-3xl font-bold text-center mb-12 text-gray-800 dark:text-gray-200">
          Comprehensive Environmental Tracking
        </h2>
        <div className="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
          {/* Feature card with authentic data statistics */}
          <Card className="hover:shadow-lg transition-shadow">
            <CardHeader>
              <Globe className="h-12 w-12 text-blue-600 mb-4" />
              <CardTitle>Global Data</CardTitle>
              <CardDescription>
                Explore authentic environmental data from 190+ countries with real CO₂ emissions and renewable energy statistics
              </CardDescription>
            </CardHeader>
          </Card>
          
          {/* Additional feature cards... */}
        </div>
      </section>
    </div>
  );
}
```

### Carbon Footprint Calculator (`client/src/pages/calculator.tsx`)
```typescript
import { zodResolver } from "@hookform/resolvers/zod";
import { useForm } from "react-hook-form";
import { z } from "zod";
import { useState } from "react";

// Validation schema for calculator inputs
const calculatorSchema = z.object({
  electricity: z.number().min(0, "Must be a positive number"),
  gas: z.number().min(0, "Must be a positive number"),
  transportation: z.number().min(0, "Must be a positive number"),
  diet: z.string().min(1, "Please select a diet type"),
  flights: z.number().min(0, "Must be a positive number"),
});

type CalculatorData = z.infer<typeof calculatorSchema>;

export default function Calculator() {
  const [result, setResult] = useState<number | null>(null);
  const [tips, setTips] = useState<string[]>([]);

  // React Hook Form setup with Zod validation
  const form = useForm<CalculatorData>({
    resolver: zodResolver(calculatorSchema),
    defaultValues: {
      electricity: 0,
      gas: 0,
      transportation: 0,
      diet: "",
      flights: 0,
    },
  });

  // Carbon footprint calculation with realistic emission factors
  const onSubmit = (data: CalculatorData) => {
    // Emission factors based on real environmental data
    const electricityFactor = 0.4; // kg CO2 per kWh
    const gasFactor = 2.3; // kg CO2 per cubic meter
    const transportFactor = 0.12; // kg CO2 per km
    const dietFactors = {
      meat: 2.5,
      vegetarian: 1.7,
      vegan: 1.5,
    };
    const flightFactor = 0.25; // kg CO2 per km

    // Calculate total annual emissions
    const totalEmissions = 
      (data.electricity * 12 * electricityFactor) +
      (data.gas * 12 * gasFactor) +
      (data.transportation * 365 * transportFactor) +
      (dietFactors[data.diet as keyof typeof dietFactors] * 365) +
      (data.flights * flightFactor);

    const annualTons = totalEmissions / 1000; // Convert to tons
    setResult(annualTons);

    // Generate personalized reduction tips based on user input
    generatePersonalizedTips(data, annualTons);
    
    // Store calculation in localStorage for analytics
    storeCalculationData(data, annualTons);
  };

  // Dynamic tip generation based on user's highest emission sources
  const generatePersonalizedTips = (data: CalculatorData, total: number) => {
    const newTips: string[] = [];
    
    if (data.electricity > 300) {
      newTips.push("💡 Switch to LED bulbs to reduce electricity consumption by up to 80%");
    }
    if (data.transportation > 50) {
      newTips.push("🚗 Consider carpooling or public transport to cut transport emissions by 45%");
    }
    // Additional tip logic...
    
    setTips(newTips);
  };

  return (
    <div className="container mx-auto px-4 py-8">
      {/* Calculator form with real-time validation */}
      <Form {...form}>
        <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-6">
          {/* Form fields with proper validation and error handling */}
        </form>
      </Form>

      {/* Results display with actionable insights */}
      {result && (
        <Card className="mt-8">
          <CardHeader>
            <CardTitle className="flex items-center">
              <Leaf className="mr-2 h-6 w-6 text-green-600" />
              Your Carbon Footprint: {result.toFixed(2)} tons CO₂/year
            </CardTitle>
          </CardHeader>
          <CardContent>
            {/* Personalized reduction tips */}
            <div className="space-y-2">
              {tips.map((tip, index) => (
                <p key={index} className="text-sm text-gray-600 dark:text-gray-400">
                  {tip}
                </p>
              ))}
            </div>
          </CardContent>
        </Card>
      )}
    </div>
  );
}
```

### Interactive World Map (`client/src/pages/world-map.tsx`)
```typescript
import { useState, useMemo } from "react";
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogDescription } from "@/components/ui/dialog";

// Authentic environmental data for 190+ countries
const countriesData = [
  {
    name: "Qatar",
    region: "Middle East",
    co2PerCapita: 38.84, // Highest globally - Our World in Data 2023
    renewableEnergy: 2.1, // IRENA 2024
    population: 2.9,
    flagEmoji: "🇶🇦"
  },
  {
    name: "Kuwait",
    region: "Middle East", 
    co2PerCapita: 28.85,
    renewableEnergy: 1.8,
    population: 4.3,
    flagEmoji: "🇰🇼"
  },
  // ... 188+ more countries with real data
];

export default function WorldMap() {
  const [searchTerm, setSearchTerm] = useState("");
  const [selectedRegion, setSelectedRegion] = useState("all");
  const [selectedMetric, setSelectedMetric] = useState("co2");
  const [showAdvancedFilters, setShowAdvancedFilters] = useState(false);
  
  // Advanced filtering ranges for precise data exploration
  const [populationRange, setPopulationRange] = useState([0, 1500]);
  const [co2Range, setCo2Range] = useState([0, 40]); // Updated to include Qatar's 38.84
  const [renewableRange, setRenewableRange] = useState([0, 100]);

  // Intelligent filtering system combining multiple criteria
  const filteredCountries = useMemo(() => {
    return countriesData.filter(country => {
      const matchesSearch = country.name.toLowerCase().includes(searchTerm.toLowerCase());
      const matchesRegion = selectedRegion === "all" || country.region === selectedRegion;
      const matchesPopulation = country.population >= populationRange[0] && country.population <= populationRange[1];
      const matchesCo2 = country.co2PerCapita >= co2Range[0] && country.co2PerCapita <= co2Range[1];
      const matchesRenewable = country.renewableEnergy >= renewableRange[0] && country.renewableEnergy <= renewableRange[1];
      
      return matchesSearch && matchesRegion && matchesPopulation && matchesCo2 && matchesRenewable;
    });
  }, [searchTerm, selectedRegion, populationRange, co2Range, renewableRange]);

  // Dynamic sorting based on selected environmental metric
  const sortedCountries = useMemo(() => {
    return [...filteredCountries].sort((a, b) => {
      switch (selectedMetric) {
        case "co2":
          return b.co2PerCapita - a.co2PerCapita; // Highest emissions first
        case "renewable":
          return b.renewableEnergy - a.renewableEnergy; // Highest renewable first
        case "population":
          return b.population - a.population; // Largest population first
        default:
          return 0;
      }
    });
  }, [filteredCountries, selectedMetric]);

  return (
    <div className="container mx-auto px-4 py-8">
      {/* Page header with accurate country count */}
      <div className="text-center mb-8">
        <h1 className="text-4xl font-bold mb-4 text-gray-800 dark:text-gray-200">
          Global Environmental Data
        </h1>
        <p className="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
          Explore authentic environmental data from 190+ countries worldwide. 
          Filter by CO₂ emissions, renewable energy usage, and population metrics.
        </p>
      </div>

      {/* Search and filter interface */}
      <div className="grid md:grid-cols-4 gap-4 mb-8">
        <Input
          placeholder="Search countries..."
          value={searchTerm}
          onChange={(e) => setSearchTerm(e.target.value)}
          className="md:col-span-2"
        />
        
        {/* Region filter dropdown */}
        <Select value={selectedRegion} onValueChange={setSelectedRegion}>
          <SelectTrigger>
            <SelectValue placeholder="Select region" />
          </SelectTrigger>
          <SelectContent>
            <SelectItem value="all">All Regions</SelectItem>
            {regions.map(region => (
              <SelectItem key={region} value={region}>{region}</SelectItem>
            ))}
          </SelectContent>
        </Select>

        {/* Advanced filters dialog with accessibility features */}
        <Dialog open={showAdvancedFilters} onOpenChange={setShowAdvancedFilters}>
          <DialogTrigger asChild>
            <Button variant="outline" className="w-full">
              <Filter className="mr-2 h-4 w-4" />
              More Filters
            </Button>
          </DialogTrigger>
          <DialogContent className="sm:max-w-md" aria-describedby="filter-description">
            <DialogHeader>
              <DialogTitle>Advanced Filters</DialogTitle>
              <DialogDescription id="filter-description">
                Fine-tune your search with additional filters
              </DialogDescription>
            </DialogHeader>
            {/* Range sliders for precise filtering */}
            <div className="space-y-6">
              <div>
                <label className="text-sm font-medium mb-2 block">
                  CO₂ Emissions Range (tons/person): {co2Range[0]} - {co2Range[1]}
                </label>
                <Slider
                  value={co2Range}
                  onValueChange={setCo2Range}
                  min={0}
                  max={40} // Updated to accommodate Qatar's 38.84 tons/person
                  step={0.5}
                  className="w-full"
                />
              </div>
              {/* Additional range controls... */}
            </div>
          </DialogContent>
        </Dialog>
      </div>

      {/* Country data grid with real environmental statistics */}
      <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        {sortedCountries.map((country) => (
          <Card key={country.name} className="hover:shadow-lg transition-shadow">
            <CardHeader>
              <CardTitle className="flex items-center justify-between">
                <span className="flex items-center">
                  <span className="text-2xl mr-2">{country.flagEmoji}</span>
                  {country.name}
                </span>
                <Badge variant="secondary">{country.region}</Badge>
              </CardTitle>
            </CardHeader>
            <CardContent>
              {/* Real environmental data display */}
              <div className="space-y-3">
                <div className="flex justify-between">
                  <span className="text-sm text-gray-600 dark:text-gray-400">CO₂ Emissions:</span>
                  <span className="font-medium">{country.co2PerCapita} tons/person</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-sm text-gray-600 dark:text-gray-400">Renewable Energy:</span>
                  <span className="font-medium">{country.renewableEnergy}%</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-sm text-gray-600 dark:text-gray-400">Population:</span>
                  <span className="font-medium">{country.population}M</span>
                </div>
              </div>
            </CardContent>
          </Card>
        ))}
      </div>

      {/* Results summary */}
      <div className="mt-8 text-center">
        <p className="text-gray-600 dark:text-gray-400">
          Showing {sortedCountries.length} of 190+ countries
        </p>
      </div>
    </div>
  );
}
```

---

## Backend Infrastructure

### Express Server (`server/index.ts`)
```typescript
import express from 'express';
import { fileURLToPath } from 'url';
import path from 'path';

const app = express();
const PORT = process.env.PORT || 5000;

// Middleware for parsing JSON and serving static files
app.use(express.json());

// Serve React app from dist/public in production
if (process.env.NODE_ENV === 'production') {
  const publicPath = path.join(path.dirname(fileURLToPath(import.meta.url)), 'public');
  app.use(express.static(publicPath));
  
  // Handle React routing - serve index.html for all non-API routes
  app.get('*', (req, res) => {
    res.sendFile(path.join(publicPath, 'index.html'));
  });
}

// Health check endpoints for deployment monitoring
app.get('/health', (req, res) => {
  res.status(200).json({
    status: 'healthy',
    message: 'Global Eco Footprint Atlas is running',
    timestamp: new Date().toISOString(),
    environment: process.env.NODE_ENV || 'development'
  });
});

app.get('/api/health', (req, res) => {
  res.status(200).json({
    status: 'healthy',
    message: 'API endpoints are operational',
    timestamp: new Date().toISOString()
  });
});

// Start server with proper host binding for deployment
app.listen(PORT, '0.0.0.0', () => {
  console.log(`[express] serving on port ${PORT}`);
});
```

### Configuration Files

#### Vite Build Configuration (`vite.config.ts`)
```typescript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import path from "path";

export default defineConfig({
  plugins: [react()],
  build: {
    outDir: '../dist/public', // Output for static deployment
    emptyOutDir: true,
    sourcemap: false, // Disable for production
    rollupOptions: {
      output: {
        manualChunks: { // Code splitting for better performance
          vendor: ['react', 'react-dom'],
          ui: ['@radix-ui/react-dialog', '@radix-ui/react-select']
        }
      }
    }
  },
  resolve: {
    alias: { // Clean import paths throughout the app
      "@": path.resolve(__dirname, "./src"),
      "@shared": path.resolve(__dirname, "../shared"),
      "@assets": path.resolve(__dirname, "../attached_assets")
    }
  }
});
```

#### Tailwind Styling (`tailwind.config.ts`)
```typescript
import type { Config } from "tailwindcss";

const config: Config = {
  darkMode: ["class"], // Enable class-based dark mode
  content: [
    "./src/**/*.{js,ts,jsx,tsx,mdx}", // Scan all React files
  ],
  theme: {
    extend: {
      colors: {
        // Custom color palette for environmental theme
        border: "hsl(var(--border))",
        background: "hsl(var(--background))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        // Additional theme colors...
      },
      animation: {
        // Custom animations for preloader and UI elements
        "bounce": "bounce 1s infinite",
      }
    },
  },
  plugins: [require("tailwindcss-animate")], // Enable advanced animations
};

export default config;
```

---

## Key Technical Decisions Explained

### 1. **TypeScript Throughout**
- **Why:** Type safety prevents runtime errors and improves development experience
- **Implementation:** Shared types between frontend/backend, strict configuration

### 2. **React Query for State Management**
- **Why:** Handles server state, caching, and loading states automatically
- **Implementation:** Custom query client with error handling

### 3. **Authentic Environmental Data**
- **Why:** Real data from Our World in Data (2023) and IRENA (2024) ensures accuracy
- **Implementation:** 190+ countries with verified CO₂ emissions and renewable energy statistics

### 4. **Component-Based Architecture**
- **Why:** Reusable UI components with shadcn/ui for consistency and accessibility
- **Implementation:** Modular design with proper prop typing

### 5. **Progressive Loading Experience**
- **Why:** Preloader provides visual feedback during app initialization
- **Implementation:** Animated environmental icons with realistic progress simulation

### 6. **Responsive Design System**
- **Why:** Works seamlessly across all device sizes
- **Implementation:** Tailwind CSS with mobile-first approach

### 7. **Dark Mode Support**
- **Why:** Better user experience and reduced eye strain
- **Implementation:** CSS custom properties with automatic system detection

This codebase demonstrates modern web development practices with emphasis on environmental data accuracy, user experience, and maintainable architecture.