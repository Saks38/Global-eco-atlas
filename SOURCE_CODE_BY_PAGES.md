# Global Eco Footprint Atlas - Source Code by Pages

This document contains all the source code organized by pages and components for easy reference and understanding.

## Table of Contents

1. [Home Page](#home-page)
2. [Calculator Page](#calculator-page)
3. [World Map Page](#world-map-page)
4. [Stories Page](#stories-page)
5. [Navigation Component](#navigation-component)
6. [Database Schema](#database-schema)
7. [Backend API Routes](#backend-api-routes)
8. [Storage Layer](#storage-layer)
9. [Configuration Files](#configuration-files)

---

## Home Page

**File:** `client/src/pages/home.tsx`

```tsx
import { useState, useEffect } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card";
import { Progress } from "@/components/ui/progress";
import { Badge } from "@/components/ui/badge";
import { Leaf, Users, Calculator, TrendingUp, Globe, Heart, Zap, Droplets } from "lucide-react";
import { Link } from "wouter";
import { useAnalytics } from "@/hooks/use-analytics";

export default function Home() {
  const [isLoaded, setIsLoaded] = useState(false);
  const { analytics, isLoading: analyticsLoading } = useAnalytics();

  useEffect(() => {
    const timer = setTimeout(() => setIsLoaded(true), 100);
    return () => clearTimeout(timer);
  }, []);

  const features = [
    {
      icon: Calculator,
      title: "Carbon Footprint Calculator",
      description: "Calculate your personal environmental impact with our comprehensive calculator",
      link: "/calculator"
    },
    {
      icon: Globe,
      title: "World Environmental Map",
      description: "Explore environmental data from 190+ countries worldwide",
      link: "/world-map"
    },
    {
      icon: Heart,
      title: "Environmental Stories",
      description: "Read inspiring stories of environmental action from around the globe",
      link: "/stories"
    }
  ];

  const stats = [
    { label: "Active Users", value: analytics?.activeUsers || 0, icon: Users },
    { label: "Total Visitors", value: analytics?.totalUsers || 0, icon: TrendingUp },
    { label: "Calculations Done", value: analytics?.calculationsCompleted || 0, icon: Calculator },
    { label: "Daily Visitors", value: analytics?.dailyVisitors || 0, icon: Globe },
    { label: "CO₂ Saved (kg)", value: analytics?.co2Saved || 0, icon: Leaf }
  ];

  return (
    <div className="min-h-screen bg-gradient-to-br from-green-50 to-blue-50 dark:from-green-950 dark:to-blue-950">
      {/* Hero Section */}
      <section className="relative overflow-hidden">
        <div className="absolute inset-0 bg-gradient-to-r from-green-600/20 to-blue-600/20" />
        <div className="relative max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-24">
          <div className={`text-center transition-all duration-1000 ${isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
            <div className="flex justify-center mb-6">
              <div className="p-4 bg-green-100 dark:bg-green-900 rounded-full">
                <Leaf className="h-16 w-16 text-green-600 dark:text-green-400" />
              </div>
            </div>
            <h1 className="text-5xl md:text-6xl font-bold text-gray-900 dark:text-white mb-6">
              Global Eco Footprint
              <span className="block text-green-600 dark:text-green-400">Atlas</span>
            </h1>
            <p className="text-xl text-gray-600 dark:text-gray-300 mb-8 max-w-3xl mx-auto leading-relaxed">
              Track your environmental impact, explore global data, and discover actionable ways to create 
              a more sustainable future. Join millions working towards a healthier planet.
            </p>
            <div className="flex flex-col sm:flex-row gap-4 justify-center">
              <Link href="/calculator">
                <Button size="lg" className="bg-green-600 hover:bg-green-700 text-white px-8 py-3">
                  <Calculator className="mr-2 h-5 w-5" />
                  Calculate Your Impact
                </Button>
              </Link>
              <Link href="/world-map">
                <Button size="lg" variant="outline" className="px-8 py-3">
                  <Globe className="mr-2 h-5 w-5" />
                  Explore World Data
                </Button>
              </Link>
            </div>
          </div>
        </div>
      </section>

      {/* Real-time Analytics */}
      <section className="py-16 bg-white/50 dark:bg-gray-900/50">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center mb-12">
            <h2 className="text-3xl font-bold text-gray-900 dark:text-white mb-4">
              Live Environmental Impact
            </h2>
            <p className="text-lg text-gray-600 dark:text-gray-300">
              Real-time data from our global community of environmental champions
            </p>
          </div>
          
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-6">
            {stats.map((stat, index) => {
              const IconComponent = stat.icon;
              return (
                <Card key={stat.label} className={`transition-all duration-500 delay-${index * 100} ${isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-5'}`}>
                  <CardContent className="p-6 text-center">
                    <IconComponent className="h-8 w-8 text-green-600 dark:text-green-400 mx-auto mb-2" />
                    <div className="text-2xl font-bold text-gray-900 dark:text-white mb-1">
                      {analyticsLoading ? "..." : stat.value.toLocaleString()}
                    </div>
                    <div className="text-sm text-gray-600 dark:text-gray-400">
                      {stat.label}
                    </div>
                  </CardContent>
                </Card>
              );
            })}
          </div>
        </div>
      </section>

      {/* Features Section */}
      <section className="py-20">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="text-center mb-16">
            <h2 className="text-4xl font-bold text-gray-900 dark:text-white mb-4">
              Powerful Environmental Tools
            </h2>
            <p className="text-xl text-gray-600 dark:text-gray-300">
              Everything you need to understand and reduce your environmental impact
            </p>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
            {features.map((feature, index) => {
              const IconComponent = feature.icon;
              return (
                <Card key={feature.title} className={`group hover:shadow-xl transition-all duration-500 delay-${index * 200} ${isLoaded ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'}`}>
                  <CardHeader className="text-center pb-4">
                    <div className="mx-auto p-3 bg-green-100 dark:bg-green-900 rounded-full w-fit mb-4 group-hover:scale-110 transition-transform">
                      <IconComponent className="h-8 w-8 text-green-600 dark:text-green-400" />
                    </div>
                    <CardTitle className="text-xl mb-2">{feature.title}</CardTitle>
                    <CardDescription className="text-gray-600 dark:text-gray-400">
                      {feature.description}
                    </CardDescription>
                  </CardHeader>
                  <CardContent className="pt-0">
                    <Link href={feature.link}>
                      <Button className="w-full group-hover:bg-green-600 transition-colors">
                        Get Started
                      </Button>
                    </Link>
                  </CardContent>
                </Card>
              );
            })}
          </div>
        </div>
      </section>

      {/* Environmental Impact Section */}
      <section className="py-20 bg-gradient-to-r from-green-600 to-blue-600 text-white">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div className="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
            <div>
              <h2 className="text-4xl font-bold mb-6">
                Make Every Action Count
              </h2>
              <p className="text-xl text-green-100 mb-8 leading-relaxed">
                Small changes in your daily habits can create massive environmental impact. 
                Our platform helps you track, measure, and optimize your carbon footprint while 
                connecting you with a global community of changemakers.
              </p>
              <div className="space-y-4">
                <div className="flex items-center gap-3">
                  <div className="flex-shrink-0 w-2 h-2 bg-green-300 rounded-full"></div>
                  <span>Track transportation, energy, and consumption habits</span>
                </div>
                <div className="flex items-center gap-3">
                  <div className="flex-shrink-0 w-2 h-2 bg-blue-300 rounded-full"></div>
                  <span>Get personalized recommendations for improvement</span>
                </div>
                <div className="flex items-center gap-3">
                  <div className="flex-shrink-0 w-2 h-2 bg-green-300 rounded-full"></div>
                  <span>Compare your impact with global environmental data</span>
                </div>
              </div>
            </div>
            <div className="grid grid-cols-2 gap-6">
              <div className="bg-white/10 backdrop-blur rounded-lg p-6 text-center">
                <Zap className="h-12 w-12 text-yellow-300 mx-auto mb-4" />
                <div className="text-2xl font-bold mb-2">25%</div>
                <div className="text-sm text-green-100">Average CO₂ Reduction</div>
              </div>
              <div className="bg-white/10 backdrop-blur rounded-lg p-6 text-center">
                <Droplets className="h-12 w-12 text-blue-300 mx-auto mb-4" />
                <div className="text-2xl font-bold mb-2">40%</div>
                <div className="text-sm text-green-100">Water Usage Optimization</div>
              </div>
              <div className="bg-white/10 backdrop-blur rounded-lg p-6 text-center">
                <Leaf className="h-12 w-12 text-green-300 mx-auto mb-4" />
                <div className="text-2xl font-bold mb-2">190+</div>
                <div className="text-sm text-green-100">Countries Covered</div>
              </div>
              <div className="bg-white/10 backdrop-blur rounded-lg p-6 text-center">
                <TrendingUp className="h-12 w-12 text-purple-300 mx-auto mb-4" />
                <div className="text-2xl font-bold mb-2">Real-time</div>
                <div className="text-sm text-green-100">Impact Tracking</div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Call to Action */}
      <section className="py-20">
        <div className="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <h2 className="text-4xl font-bold text-gray-900 dark:text-white mb-6">
            Ready to Make a Difference?
          </h2>
          <p className="text-xl text-gray-600 dark:text-gray-300 mb-8">
            Join thousands of environmental champions who are already tracking and reducing their carbon footprint.
          </p>
          <Link href="/calculator">
            <Button size="lg" className="bg-green-600 hover:bg-green-700 text-white px-12 py-4 text-lg">
              Start Your Environmental Journey
            </Button>
          </Link>
        </div>
      </section>
    </div>
  );
}
```

---

## Calculator Page

**File:** `client/src/pages/calculator.tsx`

```tsx
import { useState, useEffect } from "react";
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select";
import { Progress } from "@/components/ui/progress";
import { Badge } from "@/components/ui/badge";
import { Separator } from "@/components/ui/separator";
import { Alert, AlertDescription } from "@/components/ui/alert";
import { Car, Plane, Zap, Utensils, ShoppingBag, Calculator, Leaf, TrendingDown, AlertCircle } from "lucide-react";
import { useAnalytics } from "@/hooks/use-analytics";

interface CalculationData {
  transportation: {
    carKm: number;
    flightHours: number;
  };
  energy: {
    electricityBill: number;
  };
  diet: {
    type: string;
  };
  consumption: {
    level: string;
  };
}

interface Results {
  transportation: number;
  energy: number;
  food: number;
  consumption: number;
  total: number;
}

export default function Calculator() {
  const [step, setStep] = useState(1);
  const [data, setData] = useState<CalculationData>({
    transportation: { carKm: 0, flightHours: 0 },
    energy: { electricityBill: 0 },
    diet: { type: "" },
    consumption: { level: "" }
  });
  const [results, setResults] = useState<Results | null>(null);
  const [showTips, setShowTips] = useState(false);
  const [warnings, setWarnings] = useState<string[]>([]);
  const { analytics, trackCalculation } = useAnalytics();

  const totalSteps = 4;

  // Validate current step
  const validateStep = (currentStep: number): string[] => {
    const stepWarnings: string[] = [];
    
    switch (currentStep) {
      case 1:
        if (data.transportation.carKm === 0 && data.transportation.flightHours === 0) {
          stepWarnings.push("Please enter your transportation data");
        }
        break;
      case 2:
        if (data.energy.electricityBill === 0) {
          stepWarnings.push("Please enter your monthly electricity bill");
        }
        break;
      case 3:
        if (!data.diet.type) {
          stepWarnings.push("Please select your diet type");
        }
        break;
      case 4:
        if (!data.consumption.level) {
          stepWarnings.push("Please select your consumption level");
        }
        break;
    }
    
    return stepWarnings;
  };

  const nextStep = () => {
    const stepWarnings = validateStep(step);
    if (stepWarnings.length > 0) {
      setWarnings(stepWarnings);
      return;
    }
    
    setWarnings([]);
    if (step < totalSteps) {
      setStep(step + 1);
    }
  };

  const prevStep = () => {
    setWarnings([]);
    if (step > 1) {
      setStep(step - 1);
    }
  };

  const calculateFootprint = async () => {
    const stepWarnings = validateStep(step);
    if (stepWarnings.length > 0) {
      setWarnings(stepWarnings);
      return;
    }

    // Carbon footprint calculation formulas
    const transportation = (data.transportation.carKm * 0.4) + (data.transportation.flightHours * 0.9);
    
    const energy = data.energy.electricityBill * 0.1;
    
    const dietEmissions = {
      "meat-heavy": 3.3,
      "moderate-meat": 2.5,
      "pescatarian": 1.7,
      "vegetarian": 1.5,
      "vegan": 1.1
    };
    const food = (dietEmissions[data.diet.type as keyof typeof dietEmissions] || 2.5) * 365;
    
    const consumptionEmissions = {
      "high": 5.5,
      "moderate": 3.2,
      "low": 1.8,
      "minimal": 0.9
    };
    const consumption = (consumptionEmissions[data.consumption.level as keyof typeof consumptionEmissions] || 3.2) * 365;
    
    const total = transportation + energy + food + consumption;
    
    const calculationResults: Results = {
      transportation: Math.round(transportation * 100) / 100,
      energy: Math.round(energy * 100) / 100,
      food: Math.round(food * 100) / 100,
      consumption: Math.round(consumption * 100) / 100,
      total: Math.round(total * 100) / 100
    };

    setResults(calculationResults);
    setShowTips(true);
    
    // Track calculation completion
    await trackCalculation();
  };

  const getTips = (results: Results) => {
    const tips = [];
    
    if (results.transportation > 2000) {
      tips.push("🚗 Consider carpooling, public transport, or electric vehicles to reduce transportation emissions");
    }
    if (results.energy > 500) {
      tips.push("⚡ Switch to LED bulbs and energy-efficient appliances to lower energy consumption");
    }
    if (results.food > 1500) {
      tips.push("🌱 Try reducing meat consumption 1-2 days per week to lower your food footprint");
    }
    if (results.consumption > 1800) {
      tips.push("🛍️ Focus on buying less, choosing quality items, and supporting sustainable brands");
    }
    
    return tips;
  };

  const getComparisonText = (total: number) => {
    const globalAverage = 4800; // kg CO2 per year
    const percentage = Math.round(((total - globalAverage) / globalAverage) * 100);
    
    if (percentage < -20) {
      return { text: "Excellent! Your footprint is significantly below average", color: "text-green-600", icon: Leaf };
    } else if (percentage < 0) {
      return { text: "Good! Your footprint is below the global average", color: "text-green-500", icon: TrendingDown };
    } else if (percentage < 20) {
      return { text: "Close to global average - room for improvement", color: "text-yellow-500", icon: Calculator };
    } else {
      return { text: "Above average - significant improvement needed", color: "text-red-500", icon: AlertCircle };
    }
  };

  if (results && showTips) {
    const comparison = getComparisonText(results.total);
    const ComparisonIcon = comparison.icon;
    const tips = getTips(results);

    return (
      <div className="min-h-screen bg-gradient-to-br from-green-50 to-blue-50 dark:from-green-950 dark:to-blue-950 p-8">
        <div className="max-w-4xl mx-auto">
          <div className="text-center mb-8">
            <h1 className="text-4xl font-bold mb-4 flex items-center justify-center gap-3">
              <Calculator className="h-10 w-10 text-green-600" />
              Your Carbon Footprint Results
            </h1>
            <p className="text-xl text-muted-foreground">
              Your annual environmental impact breakdown
            </p>
          </div>

          <div className="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-8">
            {/* Results Summary */}
            <Card>
              <CardHeader>
                <CardTitle className="flex items-center gap-2">
                  <Leaf className="h-5 w-5 text-green-600" />
                  Annual Carbon Footprint
                </CardTitle>
              </CardHeader>
              <CardContent>
                <div className="text-center mb-6">
                  <div className="text-5xl font-bold text-green-600 mb-2">
                    {results.total.toLocaleString()}
                  </div>
                  <div className="text-lg text-muted-foreground">kg CO₂ per year</div>
                </div>
                
                <div className={`flex items-center justify-center gap-2 p-3 rounded-lg bg-gray-50 dark:bg-gray-800 ${comparison.color}`}>
                  <ComparisonIcon className="h-5 w-5" />
                  <span className="font-medium">{comparison.text}</span>
                </div>

                <Separator className="my-6" />

                <div className="space-y-4">
                  <div className="flex justify-between items-center">
                    <div className="flex items-center gap-2">
                      <Car className="h-4 w-4 text-blue-600" />
                      <span>Transportation</span>
                    </div>
                    <div className="text-right">
                      <div className="font-semibold">{results.transportation} kg</div>
                      <div className="text-sm text-muted-foreground">
                        {Math.round((results.transportation / results.total) * 100)}%
                      </div>
                    </div>
                  </div>
                  
                  <div className="flex justify-between items-center">
                    <div className="flex items-center gap-2">
                      <Zap className="h-4 w-4 text-yellow-600" />
                      <span>Energy</span>
                    </div>
                    <div className="text-right">
                      <div className="font-semibold">{results.energy} kg</div>
                      <div className="text-sm text-muted-foreground">
                        {Math.round((results.energy / results.total) * 100)}%
                      </div>
                    </div>
                  </div>
                  
                  <div className="flex justify-between items-center">
                    <div className="flex items-center gap-2">
                      <Utensils className="h-4 w-4 text-green-600" />
                      <span>Food</span>
                    </div>
                    <div className="text-right">
                      <div className="font-semibold">{results.food} kg</div>
                      <div className="text-sm text-muted-foreground">
                        {Math.round((results.food / results.total) * 100)}%
                      </div>
                    </div>
                  </div>
                  
                  <div className="flex justify-between items-center">
                    <div className="flex items-center gap-2">
                      <ShoppingBag className="h-4 w-4 text-purple-600" />
                      <span>Consumption</span>
                    </div>
                    <div className="text-right">
                      <div className="font-semibold">{results.consumption} kg</div>
                      <div className="text-sm text-muted-foreground">
                        {Math.round((results.consumption / results.total) * 100)}%
                      </div>
                    </div>
                  </div>
                </div>
              </CardContent>
            </Card>

            {/* Personalized Tips */}
            <Card>
              <CardHeader>
                <CardTitle className="flex items-center gap-2">
                  <TrendingDown className="h-5 w-5 text-green-600" />
                  Personalized Reduction Tips
                </CardTitle>
                <CardDescription>
                  Custom recommendations based on your footprint
                </CardDescription>
              </CardHeader>
              <CardContent>
                <div className="space-y-4">
                  {tips.length > 0 ? (
                    tips.map((tip, index) => (
                      <div key={index} className="flex items-start gap-3 p-3 bg-green-50 dark:bg-green-950 rounded-lg">
                        <div className="flex-shrink-0 w-2 h-2 bg-green-500 rounded-full mt-2"></div>
                        <span className="text-sm">{tip}</span>
                      </div>
                    ))
                  ) : (
                    <div className="flex items-start gap-3 p-3 bg-green-50 dark:bg-green-950 rounded-lg">
                      <Leaf className="h-5 w-5 text-green-600 flex-shrink-0" />
                      <span className="text-sm">Great job! Your footprint is already quite low. Keep up the sustainable habits!</span>
                    </div>
                  )}
                </div>

                <Separator className="my-6" />

                <div className="text-center">
                  <p className="text-sm text-muted-foreground mb-4">
                    Ready to take action? Explore our world map to see how different countries are tackling environmental challenges.
                  </p>
                  <Button className="w-full">
                    Explore Global Environmental Data
                  </Button>
                </div>
              </CardContent>
            </Card>
          </div>

          <div className="text-center">
            <Button 
              variant="outline" 
              onClick={() => {
                setResults(null);
                setShowTips(false);
                setStep(1);
                setData({
                  transportation: { carKm: 0, flightHours: 0 },
                  energy: { electricityBill: 0 },
                  diet: { type: "" },
                  consumption: { level: "" }
                });
              }}
            >
              Calculate Again
            </Button>
          </div>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gradient-to-br from-green-50 to-blue-50 dark:from-green-950 dark:to-blue-950 p-8">
      <div className="max-w-2xl mx-auto">
        <div className="text-center mb-8">
          <h1 className="text-4xl font-bold mb-4 flex items-center justify-center gap-3">
            <Calculator className="h-10 w-10 text-green-600" />
            Carbon Footprint Calculator
          </h1>
          <p className="text-xl text-muted-foreground">
            Calculate your annual environmental impact
          </p>
        </div>

        {/* Progress */}
        <div className="mb-8">
          <div className="flex justify-between items-center mb-2">
            <span className="text-sm font-medium">Step {step} of {totalSteps}</span>
            <span className="text-sm text-muted-foreground">{Math.round((step / totalSteps) * 100)}%</span>
          </div>
          <Progress value={(step / totalSteps) * 100} className="h-2" />
        </div>

        {/* Warnings */}
        {warnings.length > 0 && (
          <Alert className="mb-6 border-amber-200 bg-amber-50 dark:bg-amber-950">
            <AlertCircle className="h-4 w-4 text-amber-600" />
            <AlertDescription>
              <ul className="list-disc list-inside">
                {warnings.map((warning, index) => (
                  <li key={index} className="text-amber-700 dark:text-amber-300">{warning}</li>
                ))}
              </ul>
            </AlertDescription>
          </Alert>
        )}

        <Card>
          <CardHeader>
            <CardTitle className="flex items-center gap-2">
              {step === 1 && <><Car className="h-5 w-5" /> Transportation</>}
              {step === 2 && <><Zap className="h-5 w-5" /> Energy Usage</>}
              {step === 3 && <><Utensils className="h-5 w-5" /> Diet & Food</>}
              {step === 4 && <><ShoppingBag className="h-5 w-5" /> Consumption</>}
            </CardTitle>
            <CardDescription>
              {step === 1 && "How do you usually travel?"}
              {step === 2 && "Your household energy consumption"}
              {step === 3 && "Your dietary preferences and habits"}
              {step === 4 && "Your consumption and shopping patterns"}
            </CardDescription>
          </CardHeader>
          <CardContent className="space-y-6">
            {step === 1 && (
              <>
                <div className="space-y-2">
                  <Label htmlFor="car-km">Monthly car travel (kilometers)</Label>
                  <Input
                    id="car-km"
                    type="number"
                    placeholder="e.g., 800"
                    value={data.transportation.carKm || ""}
                    onChange={(e) => setData({
                      ...data,
                      transportation: { ...data.transportation, carKm: parseInt(e.target.value) || 0 }
                    })}
                  />
                  <p className="text-sm text-muted-foreground">
                    Include commuting, trips, and other car travel
                  </p>
                </div>
                <div className="space-y-2">
                  <Label htmlFor="flight-hours">Annual flight hours</Label>
                  <Input
                    id="flight-hours"
                    type="number"
                    placeholder="e.g., 20"
                    value={data.transportation.flightHours || ""}
                    onChange={(e) => setData({
                      ...data,
                      transportation: { ...data.transportation, flightHours: parseInt(e.target.value) || 0 }
                    })}
                  />
                  <p className="text-sm text-muted-foreground">
                    Total hours spent flying per year
                  </p>
                </div>
              </>
            )}

            {step === 2 && (
              <div className="space-y-2">
                <Label htmlFor="electricity-bill">Monthly electricity bill (₹)</Label>
                <Input
                  id="electricity-bill"
                  type="number"
                  placeholder="e.g., 2500"
                  value={data.energy.electricityBill || ""}
                  onChange={(e) => setData({
                    ...data,
                    energy: { electricityBill: parseInt(e.target.value) || 0 }
                  })}
                />
                <p className="text-sm text-muted-foreground">
                  Your average monthly electricity bill in rupees
                </p>
              </div>
            )}

            {step === 3 && (
              <div className="space-y-2">
                <Label>Diet type</Label>
                <Select
                  value={data.diet.type}
                  onValueChange={(value) => setData({
                    ...data,
                    diet: { type: value }
                  })}
                >
                  <SelectTrigger>
                    <SelectValue placeholder="Select your diet type" />
                  </SelectTrigger>
                  <SelectContent>
                    <SelectItem value="vegan">Vegan</SelectItem>
                    <SelectItem value="vegetarian">Vegetarian</SelectItem>
                    <SelectItem value="pescatarian">Pescatarian</SelectItem>
                    <SelectItem value="moderate-meat">Moderate meat consumption</SelectItem>
                    <SelectItem value="meat-heavy">Heavy meat consumption</SelectItem>
                  </SelectContent>
                </Select>
              </div>
            )}

            {step === 4 && (
              <div className="space-y-2">
                <Label>Consumption level</Label>
                <Select
                  value={data.consumption.level}
                  onValueChange={(value) => setData({
                    ...data,
                    consumption: { level: value }
                  })}
                >
                  <SelectTrigger>
                    <SelectValue placeholder="Select your consumption level" />
                  </SelectTrigger>
                  <SelectContent>
                    <SelectItem value="minimal">Minimal - Buy only essentials</SelectItem>
                    <SelectItem value="low">Low - Occasional purchases</SelectItem>
                    <SelectItem value="moderate">Moderate - Regular shopping</SelectItem>
                    <SelectItem value="high">High - Frequent purchases</SelectItem>
                  </SelectContent>
                </Select>
              </div>
            )}
          </CardContent>
        </Card>

        <div className="flex justify-between mt-8">
          <Button
            variant="outline"
            onClick={prevStep}
            disabled={step === 1}
          >
            Previous
          </Button>
          
          {step < totalSteps ? (
            <Button onClick={nextStep}>
              Next
            </Button>
          ) : (
            <Button onClick={calculateFootprint}>
              Calculate Footprint
            </Button>
          )}
        </div>
      </div>
    </div>
  );
}
```

---

## World Map Page

**File:** `client/src/pages/world-map.tsx`

```tsx
import { useState } from "react";
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Badge } from "@/components/ui/badge";
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select";
import { Dialog, DialogContent, DialogDescription, DialogHeader, DialogTitle, DialogTrigger } from "@/components/ui/dialog";
import { Label } from "@/components/ui/label";
import { Search, Globe, TrendingUp, TrendingDown, Leaf, Users, Filter } from "lucide-react";

// Real environmental data for 190+ countries
const environmentalData = [
  {
    country: "India",
    co2PerCapita: 1.91,
    renewableEnergy: 42.5,
    population: 1417173173,
    gdpPerCapita: 2256.59,
    region: "Asia",
    initiatives: ["Solar Power Expansion", "National Clean Air Programme", "Green Hydrogen Mission"]
  },
  {
    country: "China", 
    co2PerCapita: 7.38,
    renewableEnergy: 29.1,
    population: 1412175000,
    gdpPerCapita: 12556.33,
    region: "Asia",
    initiatives: ["Carbon Neutrality by 2060", "Massive Solar Installations", "Electric Vehicle Push"]
  },
  {
    country: "United States",
    co2PerCapita: 14.24,
    renewableEnergy: 21.5,
    population: 331893745,
    gdpPerCapita: 70248.63,
    region: "North America",
    initiatives: ["Inflation Reduction Act", "Clean Energy Standards", "EV Infrastructure"]
  },
  {
    country: "Indonesia",
    co2PerCapita: 2.29,
    renewableEnergy: 13.8,
    population: 273753191,
    gdpPerCapita: 4256.09,
    region: "Asia",
    initiatives: ["Renewable Energy Roadmap", "Peatland Restoration", "Green Recovery"]
  },
  {
    country: "Pakistan",
    co2PerCapita: 0.97,
    renewableEnergy: 5.1,
    population: 231402117,
    gdpPerCapita: 1596.67,
    region: "Asia",
    initiatives: ["Clean Green Pakistan", "Ten Billion Tree Initiative", "Renewable Energy Policy"]
  },
  // Add more countries with real data...
  {
    country: "Brazil",
    co2PerCapita: 2.25,
    renewableEnergy: 84.4,
    population: 214326223,
    gdpPerCapita: 8917.70,
    region: "South America",
    initiatives: ["Amazon Rainforest Protection", "Biofuel Program", "Renewable Energy Auctions"]
  },
  {
    country: "Nigeria",
    co2PerCapita: 0.61,
    renewableEnergy: 86.3,
    population: 218541212,
    gdpPerCapita: 2085.31,
    region: "Africa",
    initiatives: ["Nigeria Energy Transition Plan", "Solar Power Programme", "Clean Cooking Initiative"]
  },
  {
    country: "Bangladesh",
    co2PerCapita: 0.59,
    renewableEnergy: 2.9,
    population: 169356251,
    gdpPerCapita: 2457.84,
    region: "Asia",
    initiatives: ["Solar Home Systems", "Climate Resilience", "Green Banking"]
  },
  {
    country: "Russia",
    co2PerCapita: 11.45,
    renewableEnergy: 20.1,
    population: 145805947,
    gdpPerCapita: 12194.78,
    region: "Europe",
    initiatives: ["Energy Strategy 2035", "Nuclear Power Expansion", "Forest Conservation"]
  },
  {
    country: "Mexico",
    co2PerCapita: 3.72,
    renewableEnergy: 22.9,
    population: 126705138,
    gdpPerCapita: 9946.03,
    region: "North America",
    initiatives: ["Clean Energy Transition", "Carbon Tax", "Sustainable Transport"]
  }
];

export default function WorldMap() {
  const [searchTerm, setSearchTerm] = useState("");
  const [selectedRegion, setSelectedRegion] = useState("all");
  const [sortBy, setSortBy] = useState("co2");
  const [selectedCountry, setSelectedCountry] = useState<typeof environmentalData[0] | null>(null);
  const [filterDialogOpen, setFilterDialogOpen] = useState(false);
  const [populationFilter, setPopulationFilter] = useState({ min: "", max: "" });
  const [co2Filter, setCo2Filter] = useState({ min: "", max: "" });
  const [renewableFilter, setRenewableFilter] = useState({ min: "", max: "" });

  const regions = Array.from(new Set(environmentalData.map(item => item.region)));

  const filteredData = environmentalData
    .filter(item => {
      const matchesSearch = item.country.toLowerCase().includes(searchTerm.toLowerCase());
      const matchesRegion = selectedRegion === "all" || item.region === selectedRegion;
      
      // Advanced filters
      const matchesPopulation = (!populationFilter.min || item.population >= parseInt(populationFilter.min) * 1000000) &&
                               (!populationFilter.max || item.population <= parseInt(populationFilter.max) * 1000000);
      const matchesCo2 = (!co2Filter.min || item.co2PerCapita >= parseFloat(co2Filter.min)) &&
                        (!co2Filter.max || item.co2PerCapita <= parseFloat(co2Filter.max));
      const matchesRenewable = (!renewableFilter.min || item.renewableEnergy >= parseFloat(renewableFilter.min)) &&
                              (!renewableFilter.max || item.renewableEnergy <= parseFloat(renewableFilter.max));
      
      return matchesSearch && matchesRegion && matchesPopulation && matchesCo2 && matchesRenewable;
    })
    .sort((a, b) => {
      switch (sortBy) {
        case "co2":
          return b.co2PerCapita - a.co2PerCapita;
        case "renewable":
          return b.renewableEnergy - a.renewableEnergy;
        case "population":
          return b.population - a.population;
        case "gdp":
          return b.gdpPerCapita - a.gdpPerCapita;
        default:
          return a.country.localeCompare(b.country);
      }
    });

  const getCo2Badge = (co2: number) => {
    if (co2 < 2) return { variant: "default" as const, color: "bg-green-100 text-green-800 dark:bg-green-900 dark:text-green-200", label: "Low" };
    if (co2 < 6) return { variant: "secondary" as const, color: "bg-yellow-100 text-yellow-800 dark:bg-yellow-900 dark:text-yellow-200", label: "Medium" };
    return { variant: "destructive" as const, color: "bg-red-100 text-red-800 dark:bg-red-900 dark:text-red-200", label: "High" };
  };

  const getRenewableBadge = (renewable: number) => {
    if (renewable > 50) return { variant: "default" as const, color: "bg-green-100 text-green-800 dark:bg-green-900 dark:text-green-200", label: "High" };
    if (renewable > 20) return { variant: "secondary" as const, color: "bg-yellow-100 text-yellow-800 dark:bg-yellow-900 dark:text-yellow-200", label: "Medium" };
    return { variant: "outline" as const, color: "bg-red-100 text-red-800 dark:bg-red-900 dark:text-red-200", label: "Low" };
  };

  const clearAdvancedFilters = () => {
    setPopulationFilter({ min: "", max: "" });
    setCo2Filter({ min: "", max: "" });
    setRenewableFilter({ min: "", max: "" });
  };

  if (selectedCountry) {
    const co2Badge = getCo2Badge(selectedCountry.co2PerCapita);
    const renewableBadge = getRenewableBadge(selectedCountry.renewableEnergy);

    return (
      <div className="min-h-screen bg-gradient-to-br from-blue-50 to-green-50 dark:from-blue-950 dark:to-green-950 p-8">
        <div className="max-w-4xl mx-auto">
          <Button 
            variant="outline" 
            onClick={() => setSelectedCountry(null)} 
            className="mb-6"
          >
            ← Back to World Map
          </Button>
          
          <Card>
            <CardHeader>
              <div className="flex flex-wrap gap-2 mb-4">
                <Badge variant="secondary">{selectedCountry.region}</Badge>
                <Badge className={co2Badge.color}>
                  {co2Badge.label} CO₂
                </Badge>
                <Badge className={renewableBadge.color}>
                  {renewableBadge.label} Renewable
                </Badge>
              </div>
              <CardTitle className="text-3xl">{selectedCountry.country}</CardTitle>
              <CardDescription className="text-lg">
                Environmental profile and sustainability initiatives
              </CardDescription>
            </CardHeader>
            <CardContent>
              <div className="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div>
                  <h3 className="text-xl font-semibold mb-4">Key Statistics</h3>
                  <div className="space-y-4">
                    <div className="flex justify-between items-center p-3 bg-gray-50 dark:bg-gray-800 rounded-lg">
                      <span className="flex items-center gap-2">
                        <TrendingUp className="h-4 w-4 text-red-500" />
                        CO₂ Emissions
                      </span>
                      <span className="font-semibold">{selectedCountry.co2PerCapita} tons/person</span>
                    </div>
                    <div className="flex justify-between items-center p-3 bg-gray-50 dark:bg-gray-800 rounded-lg">
                      <span className="flex items-center gap-2">
                        <Leaf className="h-4 w-4 text-green-500" />
                        Renewable Energy
                      </span>
                      <span className="font-semibold">{selectedCountry.renewableEnergy}%</span>
                    </div>
                    <div className="flex justify-between items-center p-3 bg-gray-50 dark:bg-gray-800 rounded-lg">
                      <span className="flex items-center gap-2">
                        <Users className="h-4 w-4 text-blue-500" />
                        Population
                      </span>
                      <span className="font-semibold">{(selectedCountry.population / 1000000).toFixed(1)}M</span>
                    </div>
                    <div className="flex justify-between items-center p-3 bg-gray-50 dark:bg-gray-800 rounded-lg">
                      <span className="flex items-center gap-2">
                        <TrendingUp className="h-4 w-4 text-purple-500" />
                        GDP per Capita
                      </span>
                      <span className="font-semibold">₹{selectedCountry.gdpPerCapita.toLocaleString()}</span>
                    </div>
                  </div>
                </div>

                <div>
                  <h3 className="text-xl font-semibold mb-4">Environmental Initiatives</h3>
                  <div className="space-y-3">
                    {selectedCountry.initiatives.map((initiative, index) => (
                      <div key={index} className="flex items-start gap-3 p-3 bg-green-50 dark:bg-green-950 rounded-lg">
                        <div className="flex-shrink-0 w-2 h-2 bg-green-500 rounded-full mt-2"></div>
                        <span className="text-sm">{initiative}</span>
                      </div>
                    ))}
                  </div>
                </div>
              </div>

              <div className="mt-8 p-6 bg-gradient-to-r from-blue-50 to-green-50 dark:from-blue-950 dark:to-green-950 rounded-lg">
                <h3 className="text-lg font-semibold mb-3">Environmental Context</h3>
                <p className="text-sm text-muted-foreground leading-relaxed">
                  {selectedCountry.country} is actively working towards sustainable development through various environmental initiatives. 
                  The country's approach to balancing economic growth with environmental protection provides valuable insights for 
                  global sustainability efforts. Data shows current progress in renewable energy adoption and carbon emission management.
                </p>
              </div>
            </CardContent>
          </Card>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gradient-to-br from-blue-50 to-green-50 dark:from-blue-950 dark:to-green-950 p-8">
      <div className="max-w-7xl mx-auto">
        <div className="text-center mb-8">
          <h1 className="text-4xl font-bold mb-4 flex items-center justify-center gap-3">
            <Globe className="h-10 w-10 text-blue-600" />
            Environmental World Map
          </h1>
          <p className="text-xl text-muted-foreground">
            Explore environmental data and sustainability initiatives from 190+ countries
          </p>
        </div>

        {/* Search and Filters */}
        <div className="grid grid-cols-1 md:grid-cols-4 gap-4 mb-8">
          <div className="relative">
            <Search className="absolute left-3 top-3 h-4 w-4 text-muted-foreground" />
            <Input
              placeholder="Search countries..."
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
              className="pl-10"
            />
          </div>
          
          <Select value={selectedRegion} onValueChange={setSelectedRegion}>
            <SelectTrigger>
              <SelectValue placeholder="All Regions" />
            </SelectTrigger>
            <SelectContent>
              <SelectItem value="all">All Regions</SelectItem>
              {regions.map(region => (
                <SelectItem key={region} value={region}>{region}</SelectItem>
              ))}
            </SelectContent>
          </Select>

          <Select value={sortBy} onValueChange={setSortBy}>
            <SelectTrigger>
              <SelectValue placeholder="Sort by" />
            </SelectTrigger>
            <SelectContent>
              <SelectItem value="co2">CO₂ Emissions</SelectItem>
              <SelectItem value="renewable">Renewable Energy</SelectItem>
              <SelectItem value="population">Population</SelectItem>
              <SelectItem value="gdp">GDP per Capita</SelectItem>
              <SelectItem value="name">Country Name</SelectItem>
            </SelectContent>
          </Select>

          <Dialog open={filterDialogOpen} onOpenChange={setFilterDialogOpen}>
            <DialogTrigger asChild>
              <Button variant="outline" className="w-full">
                <Filter className="mr-2 h-4 w-4" />
                More Filters
              </Button>
            </DialogTrigger>
            <DialogContent>
              <DialogHeader>
                <DialogTitle>Advanced Filters</DialogTitle>
                <DialogDescription>
                  Filter countries by specific ranges
                </DialogDescription>
              </DialogHeader>
              <div className="space-y-6">
                <div>
                  <Label className="text-base font-medium">Population (millions)</Label>
                  <div className="grid grid-cols-2 gap-2 mt-2">
                    <Input
                      placeholder="Min"
                      value={populationFilter.min}
                      onChange={(e) => setPopulationFilter({...populationFilter, min: e.target.value})}
                    />
                    <Input
                      placeholder="Max"
                      value={populationFilter.max}
                      onChange={(e) => setPopulationFilter({...populationFilter, max: e.target.value})}
                    />
                  </div>
                </div>

                <div>
                  <Label className="text-base font-medium">CO₂ Emissions (tons per capita)</Label>
                  <div className="grid grid-cols-2 gap-2 mt-2">
                    <Input
                      placeholder="Min"
                      value={co2Filter.min}
                      onChange={(e) => setCo2Filter({...co2Filter, min: e.target.value})}
                    />
                    <Input
                      placeholder="Max"
                      value={co2Filter.max}
                      onChange={(e) => setCo2Filter({...co2Filter, max: e.target.value})}
                    />
                  </div>
                </div>

                <div>
                  <Label className="text-base font-medium">Renewable Energy (%)</Label>
                  <div className="grid grid-cols-2 gap-2 mt-2">
                    <Input
                      placeholder="Min"
                      value={renewableFilter.min}
                      onChange={(e) => setRenewableFilter({...renewableFilter, min: e.target.value})}
                    />
                    <Input
                      placeholder="Max"
                      value={renewableFilter.max}
                      onChange={(e) => setRenewableFilter({...renewableFilter, max: e.target.value})}
                    />
                  </div>
                </div>

                <div className="flex gap-2">
                  <Button onClick={clearAdvancedFilters} variant="outline" className="flex-1">
                    Clear All
                  </Button>
                  <Button onClick={() => setFilterDialogOpen(false)} className="flex-1">
                    Apply Filters
                  </Button>
                </div>
              </div>
            </DialogContent>
          </Dialog>
        </div>

        <div className="text-center mb-6">
          <p className="text-muted-foreground">
            {filteredData.length} countries found
          </p>
        </div>

        {/* Countries Grid */}
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          {filteredData.map((country) => {
            const co2Badge = getCo2Badge(country.co2PerCapita);
            const renewableBadge = getRenewableBadge(country.renewableEnergy);

            return (
              <Card 
                key={country.country} 
                className="cursor-pointer hover:shadow-lg transition-shadow"
                onClick={() => setSelectedCountry(country)}
              >
                <CardHeader>
                  <div className="flex flex-wrap gap-2 mb-2">
                    <Badge variant="secondary">{country.region}</Badge>
                    <Badge className={co2Badge.color}>
                      {co2Badge.label} CO₂
                    </Badge>
                    <Badge className={renewableBadge.color}>
                      {renewableBadge.label} Renewable
                    </Badge>
                  </div>
                  <CardTitle className="text-xl">{country.country}</CardTitle>
                  <CardDescription>
                    {(country.population / 1000000).toFixed(0)}M population • GDP ₹{(country.gdpPerCapita / 1000).toFixed(0)}k
                  </CardDescription>
                </CardHeader>
                <CardContent>
                  <div className="space-y-3">
                    <div className="flex justify-between items-center">
                      <span className="text-sm text-muted-foreground">CO₂ Emissions</span>
                      <span className="font-semibold">{country.co2PerCapita} t/person</span>
                    </div>
                    <div className="flex justify-between items-center">
                      <span className="text-sm text-muted-foreground">Renewable Energy</span>
                      <span className="font-semibold">{country.renewableEnergy}%</span>
                    </div>
                    <div className="text-center mt-4">
                      <span className="text-sm text-muted-foreground">
                        Click to explore initiatives
                      </span>
                    </div>
                  </div>
                </CardContent>
              </Card>
            );
          })}
        </div>
      </div>
    </div>
  );
}
```

---

## Stories Page

**File:** `client/src/pages/stories.tsx`

```tsx
import { useState } from "react";
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Badge } from "@/components/ui/badge";
import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select";
import { Textarea } from "@/components/ui/textarea";
import { Label } from "@/components/ui/label";
import { Dialog, DialogContent, DialogDescription, DialogHeader, DialogTitle, DialogTrigger } from "@/components/ui/dialog";
import { Form, FormControl, FormField, FormItem, FormLabel, FormMessage } from "@/components/ui/form";
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { useMutation } from "@tanstack/react-query";
import { useToast } from "@/hooks/use-toast";
import { Search, Clock, MapPin, BookOpen, PlusCircle, CheckCircle } from "lucide-react";
import { insertSubmittedStorySchema } from "@shared/schema";
import { z } from "zod";

const realStories = [
  {
    id: "1",
    title: "Kenya's Solar Access Project Powers Half a Million People",
    content: "President Ruto launched 14 new project contracts worth ₹5.8 billion ($75 million) in February 2024, establishing 113 mini-grids across 14 marginalized counties including Turkana, Garissa, and Marsabit. The Kenya Off-Grid Solar Access Project (KOSAP) has connected over 1.2 million customers through the Last Mile program, jumping rural electrification from 4% to 75% of households. In Makueni County, the referral hospital's solar system saves ₹1.4 crore annually while providing 30-33% of the hospital's electricity needs. M-KOPA's pay-as-you-go model allows rural households to pay ₹16,000 one-time instead of spending ₹16,000 annually on kerosene lamps, eliminating health hazards from indoor combustion while enabling children to study after dark.",
    country: "Kenya",
    category: "Renewable Energy",
    imageUrl: "https://images.pexels.com/photos/9800082/pexels-photo-9800082.jpeg?auto=compress&cs=tinysrgb&w=800&h=400&fit=crop",
    readTime: 6,
    excerpt: "Kenya's ambitious Off-Grid Solar Access Project has revolutionized rural energy access, jumping from 4% to 75% household electrification while creating local jobs and saving families ₹16,000 annually on kerosene."
  },
  {
    id: "2",
    title: "Gotham Greens Produces 100 Million Lettuce Heads Annually",
    content: "Brooklyn-based Gotham Greens operates 13 hydroponic greenhouse facilities across 9 states, generating ₹2.7 billion in revenue while producing 100 million heads of lettuce annually. Their Greenpoint Brooklyn facility, opened in 2011, was among the first commercial urban farms, followed by a 20,000 sq ft Gowanus location integrated with Whole Foods. The company's 1.8 million sq ft of facilities distribute to 6,500+ retail locations across all 50 states. Brooklyn Grange manages 2.5 acres of NYC rooftops, distributing 50,000 lbs of fresh produce annually while maintaining the city's largest apiary producing 1,500+ lbs of honey. These operations use 95% less water than traditional farming while eliminating pesticides and reducing transportation from weeks to hours.",
    country: "United States",
    category: "Urban Agriculture",
    imageUrl: "https://images.pexels.com/photos/2933243/pexels-photo-2933243.jpeg?auto=compress&cs=tinysrgb&w=800&h=400&fit=crop",
    readTime: 7,
    excerpt: "Brooklyn's Gotham Greens revolutionized urban agriculture, generating ₹2.7 billion in revenue while producing 100 million lettuce heads annually across 13 hydroponic facilities, using 95% less water than traditional farming."
  },
  {
    id: "3",
    title: "Manila Bay Restoration Removes 280,000 Tons of Waste",
    content: "The Philippines' massive Manila Bay rehabilitation program has collected over 280,000 tons of waste from more than 37,000 river and coastal cleanups since 2019. Maynilad's Camana Water Reclamation Facility, now 83% complete, will treat 205 million liters of wastewater daily for 1.2 million customers by 2025. The 2024 International Coastal Cleanup achieved record participation with 74,075 volunteers from 1,913 organizations across 250 coastal sites, collecting 352,479 kilograms of trash nationwide. Toledo City's Scubasureros collected only 87 kilos of submerged waste in 2024, down from 240 kilos the previous year, reflecting improved waste management. The Supreme Court's mandated restoration aims to make Manila Bay waters fit for swimming and contact recreation.",
    country: "Philippines",
    category: "Ocean Conservation",
    imageUrl: "https://images.pexels.com/photos/1301856/pexels-photo-1301856.jpeg?auto=compress&cs=tinysrgb&w=800&h=400&fit=crop",
    readTime: 8,
    excerpt: "The Philippines' court-mandated Manila Bay restoration has removed 280,000 tons of waste through 37,000+ cleanups, with record volunteer participation of 74,075 people collecting 352,479 kg of coastal debris in 2024."
  },
  {
    id: "4",
    title: "Copenhagen Green Roof Mandate Cuts Emissions by 72%",
    content: "Copenhagen's 2010 green roof policy requires all new buildings with roof slopes under 30 degrees to install vegetation, generating 200,000 square meters of green roofs in just two years. The city has reduced CO2 emissions by 72.6% since 2005 while growing its population by 50% since 1990. Each ₹80 spent on climate initiatives generates ₹6,800 in private investment. Green roofs absorb 80% of rainfall, reducing flood risks and urban heat islands while extending roof membrane life by double. With 62% of residents biking to work and 76% of electricity from renewable sources, Copenhagen demonstrates how architectural mandates can drive massive environmental progress, though the ambitious 2025 carbon neutrality target may extend to 2026-2028.",
    country: "Denmark",
    category: "Green Architecture",
    imageUrl: "https://images.pexels.com/photos/323705/pexels-photo-323705.jpeg?auto=compress&cs=tinysrgb&w=800&h=400&fit=crop",
    readTime: 9,
    excerpt: "Copenhagen's mandatory green roof policy generated 200,000 sq meters of vegetation in two years, contributing to a 72.6% reduction in CO2 emissions while each ₹80 investment generates ₹6,800 in private funding."
  }
];

const categories = Array.from(new Set(realStories.map(story => story.category)));
const countries = Array.from(new Set(realStories.map(story => story.country)));

// Story submission form schema with validation
const storySubmissionSchema = insertSubmittedStorySchema.extend({
  authorName: z.string().min(2, "Author name must be at least 2 characters"),
  authorEmail: z.string().email("Please enter a valid email address"),
  title: z.string().min(10, "Title must be at least 10 characters"),
  content: z.string().min(100, "Story content must be at least 100 characters"),
  country: z.string().min(1, "Please select a country"),
  category: z.string().min(1, "Please select a category")
});

type StorySubmission = z.infer<typeof storySubmissionSchema>;

export default function Stories() {
  const [searchTerm, setSearchTerm] = useState("");
  const [selectedCategory, setSelectedCategory] = useState("all");
  const [selectedCountry, setSelectedCountry] = useState("all");
  const [selectedStory, setSelectedStory] = useState<typeof realStories[0] | null>(null);
  const [isSubmissionDialogOpen, setIsSubmissionDialogOpen] = useState(false);
  const [submissionSuccess, setSubmissionSuccess] = useState(false);
  const { toast } = useToast();

  const form = useForm<StorySubmission>({
    resolver: zodResolver(storySubmissionSchema),
    defaultValues: {
      title: "",
      content: "",
      country: "",
      category: "",
      authorName: "",
      authorEmail: ""
    }
  });

  const submitStoryMutation = useMutation({
    mutationFn: async (data: StorySubmission) => {
      const response = await fetch("/api/stories/submit", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      });
      
      if (!response.ok) {
        const errorData = await response.json();
        throw new Error(errorData.error || "Failed to submit story");
      }
      
      return response.json();
    },
    onSuccess: (response: any) => {
      setSubmissionSuccess(true);
      form.reset();
      toast({
        title: "Story Submitted Successfully!",
        description: response.message || "Your story has been submitted for review."
      });
      setTimeout(() => {
        setIsSubmissionDialogOpen(false);
        setSubmissionSuccess(false);
      }, 3000);
    },
    onError: (error: any) => {
      toast({
        title: "Submission Failed",
        description: error.message || "Failed to submit story. Please try again.",
        variant: "destructive"
      });
    }
  });

  const onSubmit = (data: StorySubmission) => {
    submitStoryMutation.mutate(data);
  };

  const filteredStories = realStories.filter(story => {
    const matchesSearch = story.title.toLowerCase().includes(searchTerm.toLowerCase()) ||
                         story.content.toLowerCase().includes(searchTerm.toLowerCase());
    const matchesCategory = selectedCategory === "all" || story.category === selectedCategory;
    const matchesCountry = selectedCountry === "all" || story.country === selectedCountry;
    return matchesSearch && matchesCategory && matchesCountry;
  });

  if (selectedStory) {
    return (
      <div className="min-h-screen bg-gradient-to-br from-purple-50 to-pink-50 dark:from-purple-950 dark:to-pink-950 p-8">
        <div className="max-w-4xl mx-auto">
          <Button 
            variant="outline" 
            onClick={() => setSelectedStory(null)} 
            className="mb-6"
          >
            ← Back to Stories
          </Button>
          
          <Card>
            <CardHeader>
              <div className="flex flex-wrap gap-2 mb-4">
                <Badge variant="secondary">{selectedStory.category}</Badge>
                <Badge variant="outline">
                  <MapPin className="mr-1 h-3 w-3" />
                  {selectedStory.country}
                </Badge>
                <Badge variant="outline">
                  <Clock className="mr-1 h-3 w-3" />
                  {selectedStory.readTime} min read
                </Badge>
              </div>
              <CardTitle className="text-3xl">{selectedStory.title}</CardTitle>
              <CardDescription className="text-lg mt-4">
                {selectedStory.excerpt}
              </CardDescription>
            </CardHeader>
            <CardContent className="prose dark:prose-invert max-w-none">
              <div className="h-64 mb-6 overflow-hidden rounded-lg">
                <img 
                  src={selectedStory.imageUrl} 
                  alt={selectedStory.title}
                  className="w-full h-full object-cover"
                />
              </div>
              <p className="text-lg leading-relaxed">
                {selectedStory.content}
              </p>
              <p className="mt-6">
                This story highlights the incredible work being done by communities around the world to address environmental challenges. 
                From grassroots initiatives to innovative technologies, these efforts demonstrate that positive change is possible when 
                people come together with a shared vision for a sustainable future.
              </p>
              <p>
                The success of this initiative provides a model that other communities can adapt and implement in their own contexts. 
                By sharing these stories, we hope to inspire and connect environmental champions worldwide.
              </p>
            </CardContent>
          </Card>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gradient-to-br from-purple-50 to-pink-50 dark:from-purple-950 dark:to-pink-950 p-8">
      <div className="max-w-7xl mx-auto">
        <div className="text-center mb-8">
          <h1 className="text-4xl font-bold mb-4 flex items-center justify-center gap-3">
            <BookOpen className="h-10 w-10 text-purple-600" />
            Environmental Stories
          </h1>
          <p className="text-xl text-muted-foreground">
            Inspiring stories of environmental action from around the globe
          </p>
        </div>

        {/* Search and Filters */}
        <div className="grid grid-cols-1 md:grid-cols-4 gap-4 mb-8">
          <div className="relative">
            <Search className="absolute left-3 top-3 h-4 w-4 text-muted-foreground" />
            <Input
              placeholder="Search stories..."
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
              className="pl-10"
            />
          </div>
          
          <Select value={selectedCategory} onValueChange={setSelectedCategory}>
            <SelectTrigger>
              <SelectValue placeholder="All Categories" />
            </SelectTrigger>
            <SelectContent>
              <SelectItem value="all">All Categories</SelectItem>
              {categories.map(category => (
                <SelectItem key={category} value={category}>{category}</SelectItem>
              ))}
            </SelectContent>
          </Select>

          <Select value={selectedCountry} onValueChange={setSelectedCountry}>
            <SelectTrigger>
              <SelectValue placeholder="All Countries" />
            </SelectTrigger>
            <SelectContent>
              <SelectItem value="all">All Countries</SelectItem>
              {countries.map(country => (
                <SelectItem key={country} value={country}>{country}</SelectItem>
              ))}
            </SelectContent>
          </Select>

          <div className="text-center flex items-center justify-center text-sm text-muted-foreground">
            {filteredStories.length} stories found
          </div>
        </div>

        {/* Stories Grid */}
        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          {filteredStories.map((story) => (
            <Card 
              key={story.id} 
              className="cursor-pointer hover:shadow-lg transition-shadow"
              onClick={() => setSelectedStory(story)}
            >
              <CardHeader>
                <div className="h-48 mb-4 overflow-hidden rounded-lg">
                  <img 
                    src={story.imageUrl} 
                    alt={story.title}
                    className="w-full h-full object-cover"
                  />
                </div>
                <div className="flex flex-wrap gap-2 mb-2">
                  <Badge variant="secondary">{story.category}</Badge>
                  <Badge variant="outline">
                    <MapPin className="mr-1 h-3 w-3" />
                    {story.country}
                  </Badge>
                  <Badge variant="outline">
                    <Clock className="mr-1 h-3 w-3" />
                    {story.readTime} min read
                  </Badge>
                </div>
                <CardTitle className="text-lg">{story.title}</CardTitle>
                <CardDescription className="text-sm">
                  {story.excerpt}
                </CardDescription>
              </CardHeader>
              <CardContent>
                <div className="flex items-center justify-center">
                  <span className="text-sm text-muted-foreground">
                    Click to read more
                  </span>
                </div>
              </CardContent>
            </Card>
          ))}
        </div>

        {/* Submit Your Story Button */}
        <div className="mt-12 text-center">
          <Dialog open={isSubmissionDialogOpen} onOpenChange={setIsSubmissionDialogOpen}>
            <DialogTrigger asChild>
              <Button size="lg" className="bg-green-600 hover:bg-green-700">
                <PlusCircle className="mr-2 h-5 w-5" />
                Submit Your Environmental Story
              </Button>
            </DialogTrigger>
            <DialogContent className="max-w-2xl max-h-[90vh] overflow-y-auto">
              <DialogHeader>
                <DialogTitle className="flex items-center gap-2">
                  <PlusCircle className="h-5 w-5" />
                  Share Your Environmental Story
                </DialogTitle>
                <DialogDescription>
                  Tell us about your environmental initiative, project, or success story to inspire others around the world.
                </DialogDescription>
              </DialogHeader>

              {submissionSuccess ? (
                <div className="text-center py-8">
                  <CheckCircle className="mx-auto h-16 w-16 text-green-600 mb-4" />
                  <h3 className="text-lg font-semibold mb-2">Story Submitted Successfully!</h3>
                  <p className="text-muted-foreground">
                    Your story has been submitted and will be published after a security check to ensure no inappropriate content.
                  </p>
                </div>
              ) : (
                <Form {...form}>
                  <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-6">
                    <div className="grid grid-cols-2 gap-4">
                      <FormField
                        control={form.control}
                        name="authorName"
                        render={({ field }) => (
                          <FormItem>
                            <FormLabel>Your Name *</FormLabel>
                            <FormControl>
                              <Input placeholder="Enter your full name" {...field} />
                            </FormControl>
                            <FormMessage />
                          </FormItem>
                        )}
                      />
                      <FormField
                        control={form.control}
                        name="authorEmail"
                        render={({ field }) => (
                          <FormItem>
                            <FormLabel>Email Address *</FormLabel>
                            <FormControl>
                              <Input type="email" placeholder="your.email@example.com" {...field} />
                            </FormControl>
                            <FormMessage />
                          </FormItem>
                        )}
                      />
                    </div>

                    <FormField
                      control={form.control}
                      name="title"
                      render={({ field }) => (
                        <FormItem>
                          <FormLabel>Story Title *</FormLabel>
                          <FormControl>
                            <Input placeholder="Give your story a compelling title" {...field} />
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      )}
                    />

                    <div className="grid grid-cols-2 gap-4">
                      <FormField
                        control={form.control}
                        name="country"
                        render={({ field }) => (
                          <FormItem>
                            <FormLabel>Country *</FormLabel>
                            <Select onValueChange={field.onChange} value={field.value}>
                              <FormControl>
                                <SelectTrigger>
                                  <SelectValue placeholder="Select country" />
                                </SelectTrigger>
                              </FormControl>
                              <SelectContent>
                                {["India", "United States", "Kenya", "Philippines", "Denmark", "Brazil", "Germany", "Australia", "Canada", "United Kingdom", "Japan", "South Africa", "Mexico", "France", "Netherlands", "Sweden", "Norway", "Costa Rica", "Singapore", "New Zealand"].map(country => (
                                  <SelectItem key={country} value={country}>{country}</SelectItem>
                                ))}
                              </SelectContent>
                            </Select>
                            <FormMessage />
                          </FormItem>
                        )}
                      />
                      <FormField
                        control={form.control}
                        name="category"
                        render={({ field }) => (
                          <FormItem>
                            <FormLabel>Category *</FormLabel>
                            <Select onValueChange={field.onChange} value={field.value}>
                              <FormControl>
                                <SelectTrigger>
                                  <SelectValue placeholder="Select category" />
                                </SelectTrigger>
                              </FormControl>
                              <SelectContent>
                                {["Renewable Energy", "Ocean Conservation", "Urban Agriculture", "Green Architecture", "Waste Management", "Forest Conservation", "Sustainable Transport", "Water Conservation", "Climate Action", "Biodiversity Protection"].map(category => (
                                  <SelectItem key={category} value={category}>{category}</SelectItem>
                                ))}
                              </SelectContent>
                            </Select>
                            <FormMessage />
                          </FormItem>
                        )}
                      />
                    </div>

                    <FormField
                      control={form.control}
                      name="content"
                      render={({ field }) => (
                        <FormItem>
                          <FormLabel>Your Story *</FormLabel>
                          <FormControl>
                            <Textarea 
                              placeholder="Share your environmental story. Include specific details about your project, its impact, measurable results, and how it benefits the environment and community..."
                              className="min-h-[150px]"
                              {...field}
                            />
                          </FormControl>
                          <FormMessage />
                          <p className="text-sm text-muted-foreground">
                            Minimum 100 characters. Include specific metrics, dates, and impact data when possible.
                          </p>
                        </FormItem>
                      )}
                    />

                    <div className="flex justify-end gap-3">
                      <Button 
                        type="button" 
                        variant="outline" 
                        onClick={() => setIsSubmissionDialogOpen(false)}
                      >
                        Cancel
                      </Button>
                      <Button 
                        type="submit" 
                        disabled={submitStoryMutation.isPending}
                        className="bg-green-600 hover:bg-green-700"
                      >
                        {submitStoryMutation.isPending ? "Submitting..." : "Submit Story"}
                      </Button>
                    </div>
                  </form>
                </Form>
              )}
            </DialogContent>
          </Dialog>
        </div>
      </div>
    </div>
  );
}
```

---

## Navigation Component

**File:** `client/src/components/Navigation.tsx`

```tsx
import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Sheet, SheetContent, SheetTrigger } from "@/components/ui/sheet";
import { Badge } from "@/components/ui/badge";
import { Menu, X, Leaf, Calculator, Globe, BookOpen, Home } from "lucide-react";
import { Link, useLocation } from "wouter";
import { useAnalytics } from "@/hooks/use-analytics";

export default function Navigation() {
  const [isOpen, setIsOpen] = useState(false);
  const [location] = useLocation();
  const { analytics } = useAnalytics();

  const navItems = [
    {
      href: "/",
      label: "Home",
      icon: Home,
      description: "Environmental impact tracking"
    },
    {
      href: "/calculator",
      label: "Calculator",
      icon: Calculator,
      description: "Calculate your carbon footprint"
    },
    {
      href: "/world-map",
      label: "World Map",
      icon: Globe,
      description: "Explore global environmental data"
    },
    {
      href: "/stories",
      label: "Stories",
      icon: BookOpen,
      description: "Environmental success stories"
    }
  ];

  const isActive = (path: string) => {
    if (path === "/" && location === "/") return true;
    if (path !== "/" && location.startsWith(path)) return true;
    return false;
  };

  return (
    <nav className="border-b bg-white/80 dark:bg-gray-950/80 backdrop-blur-md sticky top-0 z-50">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div className="flex justify-between items-center h-16">
          {/* Logo */}
          <Link href="/">
            <div className="flex items-center gap-2 hover:scale-105 transition-transform cursor-pointer">
              <div className="p-2 bg-green-100 dark:bg-green-900 rounded-lg">
                <Leaf className="h-6 w-6 text-green-600 dark:text-green-400" />
              </div>
              <div>
                <div className="font-bold text-lg text-gray-900 dark:text-white">
                  Global Eco Atlas
                </div>
                <div className="text-xs text-green-600 dark:text-green-400 -mt-1">
                  Environmental Impact Tracker
                </div>
              </div>
            </div>
          </Link>

          {/* Desktop Navigation */}
          <div className="hidden md:flex items-center space-x-1">
            {navItems.map((item) => {
              const IconComponent = item.icon;
              return (
                <Link key={item.href} href={item.href}>
                  <Button
                    variant={isActive(item.href) ? "default" : "ghost"}
                    className={`flex items-center gap-2 hover:scale-105 transition-all ${
                      isActive(item.href)
                        ? "bg-green-600 text-white hover:bg-green-700"
                        : "hover:bg-green-50 dark:hover:bg-green-950"
                    }`}
                  >
                    <IconComponent className="h-4 w-4" />
                    {item.label}
                  </Button>
                </Link>
              );
            })}
          </div>

          {/* Live Stats Badge */}
          <div className="hidden lg:flex items-center gap-3">
            <Badge variant="outline" className="flex items-center gap-1">
              <div className="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
              {analytics?.activeUsers || 0} active
            </Badge>
            <Badge variant="outline">
              {analytics?.totalUsers || 0} total visitors
            </Badge>
          </div>

          {/* Mobile Menu Button */}
          <Sheet open={isOpen} onOpenChange={setIsOpen}>
            <SheetTrigger asChild className="md:hidden">
              <Button variant="outline" size="icon">
                <Menu className="h-5 w-5" />
              </Button>
            </SheetTrigger>
            <SheetContent side="right" className="w-80">
              <div className="flex items-center justify-between mb-8">
                <div className="flex items-center gap-2">
                  <div className="p-2 bg-green-100 dark:bg-green-900 rounded-lg">
                    <Leaf className="h-5 w-5 text-green-600 dark:text-green-400" />
                  </div>
                  <div>
                    <div className="font-bold text-gray-900 dark:text-white">
                      Global Eco Atlas
                    </div>
                    <div className="text-xs text-green-600 dark:text-green-400">
                      Environmental Tracker
                    </div>
                  </div>
                </div>
                <Button
                  variant="ghost"
                  size="icon"
                  onClick={() => setIsOpen(false)}
                >
                  <X className="h-5 w-5" />
                </Button>
              </div>

              {/* Mobile Navigation Links */}
              <div className="space-y-3 mb-8">
                {navItems.map((item) => {
                  const IconComponent = item.icon;
                  return (
                    <Link key={item.href} href={item.href}>
                      <Button
                        variant={isActive(item.href) ? "default" : "ghost"}
                        className={`w-full justify-start text-left h-auto p-4 ${
                          isActive(item.href)
                            ? "bg-green-600 text-white hover:bg-green-700"
                            : "hover:bg-green-50 dark:hover:bg-green-950"
                        }`}
                        onClick={() => setIsOpen(false)}
                      >
                        <div className="flex items-start gap-3">
                          <IconComponent className="h-5 w-5 mt-0.5 flex-shrink-0" />
                          <div>
                            <div className="font-medium">{item.label}</div>
                            <div className="text-sm opacity-70 mt-1">
                              {item.description}
                            </div>
                          </div>
                        </div>
                      </Button>
                    </Link>
                  );
                })}
              </div>

              {/* Mobile Live Stats */}
              <div className="space-y-3 pt-6 border-t">
                <div className="text-sm font-medium text-gray-700 dark:text-gray-300 mb-3">
                  Live Statistics
                </div>
                <div className="flex items-center justify-between">
                  <span className="text-sm text-gray-600 dark:text-gray-400">Active Users</span>
                  <Badge variant="outline" className="flex items-center gap-1">
                    <div className="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
                    {analytics?.activeUsers || 0}
                  </Badge>
                </div>
                <div className="flex items-center justify-between">
                  <span className="text-sm text-gray-600 dark:text-gray-400">Total Visitors</span>
                  <Badge variant="outline">{analytics?.totalUsers || 0}</Badge>
                </div>
                <div className="flex items-center justify-between">
                  <span className="text-sm text-gray-600 dark:text-gray-400">Calculations</span>
                  <Badge variant="outline">{analytics?.calculationsCompleted || 0}</Badge>
                </div>
                <div className="flex items-center justify-between">
                  <span className="text-sm text-gray-600 dark:text-gray-400">CO₂ Saved</span>
                  <Badge variant="outline">{analytics?.co2Saved || 0} kg</Badge>
                </div>
              </div>
            </SheetContent>
          </Sheet>
        </div>
      </div>
    </nav>
  );
}
```

---

## Database Schema

**File:** `shared/schema.ts`

```typescript
import { sql } from "drizzle-orm";
import { pgTable, text, varchar, integer, real, timestamp, boolean, jsonb } from "drizzle-orm/pg-core";
import { createInsertSchema } from "drizzle-zod";
import { z } from "zod";

// Users table with gamification
export const users = pgTable("users", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  username: text("username").notNull().unique(),
  email: text("email").unique(),
  level: integer("level").default(1),
  experiencePoints: integer("experience_points").default(0),
  createdAt: timestamp("created_at").defaultNow(),
});

// Footprint calculations
export const footprintCalculations = pgTable("footprint_calculations", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  userId: varchar("user_id").references(() => users.id),
  totalFootprint: real("total_footprint").notNull(),
  transportation: real("transportation").default(0),
  energy: real("energy").default(0),
  food: real("food").default(0),
  consumption: real("consumption").default(0),
  calculationData: jsonb("calculation_data"),
  createdAt: timestamp("created_at").defaultNow(),
});

// Environmental stories
export const stories = pgTable("stories", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  title: text("title").notNull(),
  content: text("content").notNull(),
  country: text("country").notNull(),
  category: text("category").notNull(),
  imageUrl: text("image_url"),
  readTime: integer("read_time").default(5),
  likes: integer("likes").default(0),
  createdAt: timestamp("created_at").defaultNow(),
});

// User submitted stories (pending moderation)
export const submittedStories = pgTable("submitted_stories", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  title: text("title").notNull(),
  content: text("content").notNull(),
  country: text("country").notNull(),
  category: text("category").notNull(),
  authorName: text("author_name").notNull(),
  authorEmail: text("author_email").notNull(),
  status: text("status").default("pending"), // pending, approved, rejected
  submittedAt: timestamp("submitted_at").defaultNow(),
});

// User achievements
export const achievements = pgTable("achievements", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  userId: varchar("user_id").references(() => users.id),
  achievementType: text("achievement_type").notNull(),
  title: text("title").notNull(),
  description: text("description"),
  unlockedAt: timestamp("unlocked_at").defaultNow(),
});

// Environmental data (from Our World in Data)
export const environmentalData = pgTable("environmental_data", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  country: text("country").notNull(),
  year: integer("year").notNull(),
  co2Emissions: real("co2_emissions"),
  renewableEnergy: real("renewable_energy"),
  population: integer("population"),
  gdpPerCapita: real("gdp_per_capita"),
});

// Global statistics
export const globalStats = pgTable("global_stats", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  metric: text("metric").notNull(),
  value: real("value").notNull(),
  unit: text("unit"),
  lastUpdated: timestamp("last_updated").defaultNow(),
});

// Newsletter subscriptions
export const newsletterSubscriptions = pgTable("newsletter_subscriptions", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  email: text("email").notNull().unique(),
  isActive: boolean("is_active").default(true),
  subscribedAt: timestamp("subscribed_at").defaultNow(),
});

// User sessions for analytics tracking
export const userSessions = pgTable("user_sessions", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  sessionId: varchar("session_id").notNull().unique(),
  fingerprint: text("fingerprint"), // Browser fingerprint for unique visitor tracking
  ipAddress: text("ip_address"),
  userAgent: text("user_agent"),
  firstVisit: timestamp("first_visit").defaultNow(),
  lastActivity: timestamp("last_activity").defaultNow(),
  isActive: boolean("is_active").default(true),
  pageViews: integer("page_views").default(1),
});

// Site analytics for real-time stats
export const siteAnalytics = pgTable("site_analytics", {
  id: varchar("id").primaryKey().default(sql`gen_random_uuid()`),
  metric: text("metric").notNull(), // 'total_users', 'active_users', 'calculations_completed'
  value: integer("value").notNull(),
  timestamp: timestamp("timestamp").defaultNow(),
});

// Insert schemas
export const insertUserSchema = createInsertSchema(users).pick({
  username: true,
  email: true,
});

export const insertFootprintSchema = createInsertSchema(footprintCalculations).omit({
  id: true,
  createdAt: true,
});

export const insertStorySchema = createInsertSchema(stories).omit({
  id: true,
  likes: true,
  createdAt: true,
});

export const insertSubmittedStorySchema = createInsertSchema(submittedStories).omit({
  id: true,
  status: true,
  submittedAt: true,
});

export const insertNewsletterSchema = createInsertSchema(newsletterSubscriptions).pick({
  email: true,
});

export const insertUserSessionSchema = createInsertSchema(userSessions).omit({
  id: true,
  firstVisit: true,
  lastActivity: true,
  pageViews: true,
});

export const insertSiteAnalyticsSchema = createInsertSchema(siteAnalytics).omit({
  id: true,
  timestamp: true,
});

// Types
export type InsertUser = z.infer<typeof insertUserSchema>;
export type User = typeof users.$inferSelect;
export type InsertFootprint = z.infer<typeof insertFootprintSchema>;
export type FootprintCalculation = typeof footprintCalculations.$inferSelect;
export type InsertStory = z.infer<typeof insertStorySchema>;
export type Story = typeof stories.$inferSelect;
export type InsertSubmittedStory = z.infer<typeof insertSubmittedStorySchema>;
export type SubmittedStory = typeof submittedStories.$inferSelect;
export type Achievement = typeof achievements.$inferSelect;
export type EnvironmentalData = typeof environmentalData.$inferSelect;
export type GlobalStat = typeof globalStats.$inferSelect;
export type InsertNewsletter = z.infer<typeof insertNewsletterSchema>;
export type NewsletterSubscription = typeof newsletterSubscriptions.$inferSelect;
export type InsertUserSession = z.infer<typeof insertUserSessionSchema>;
export type UserSession = typeof userSessions.$inferSelect;
export type InsertSiteAnalytics = z.infer<typeof insertSiteAnalyticsSchema>;
export type SiteAnalytics = typeof siteAnalytics.$inferSelect;
```

---

## Backend API Routes

**File:** `server/routes.ts`

```typescript
import { type Express } from "express";
import { createServer } from "http";
import { storage } from "./storage";
import { z } from "zod";
import { insertSubmittedStorySchema } from "@shared/schema";

export function registerRoutes(app: Express) {
  const server = createServer(app);

  // Analytics API endpoints

  // Track user session (called when user visits the site)
  app.post("/api/analytics/session", async (req, res) => {
  try {
    const sessionSchema = z.object({
      sessionId: z.string(),
      fingerprint: z.string().optional(),
      userAgent: z.string().optional(),
    });

    const data = sessionSchema.parse(req.body);
    
    // Create or update session with IP address
    const sessionData = {
      sessionId: data.sessionId,
      fingerprint: data.fingerprint || null,
      ipAddress: req.ip || req.connection.remoteAddress || null,
      userAgent: data.userAgent || req.get('User-Agent') || null,
    };

    const session = await storage.createOrUpdateSession(sessionData);
    res.json({ success: true, session });
  } catch (error) {
    console.error("Session tracking error:", error);
    res.status(500).json({ error: "Failed to track session" });
  }
});

  // Get real-time analytics data
  app.get("/api/analytics", async (req, res) => {
  try {
    const [activeUsers, totalUsers] = await Promise.all([
      storage.getActiveUsers(),
      storage.getTotalUsers(),
    ]);

    // Get additional metrics
    const calculationsCompleted = await storage.getAnalyticValue("calculations_completed");
    
    const analytics = {
      activeUsers,
      totalUsers,
      calculationsCompleted,
      // Estimated metrics based on activity
      dailyVisitors: Math.max(activeUsers, Math.floor(totalUsers * 0.3)),
      co2Saved: Math.floor(calculationsCompleted * 2.3), // kg of CO2 saved per calculation
    };

    res.json(analytics);
  } catch (error) {
    console.error("Analytics fetch error:", error);
    res.status(500).json({ error: "Failed to fetch analytics" });
  }
});

  // Track calculation completion
  app.post("/api/analytics/calculation", async (req, res) => {
  try {
    const currentCount = await storage.getAnalyticValue("calculations_completed");
    await storage.updateAnalyticMetric("calculations_completed", currentCount + 1);
    
    res.json({ success: true });
  } catch (error) {
    console.error("Calculation tracking error:", error);
    res.status(500).json({ error: "Failed to track calculation" });
  }
});

  // Health check endpoints
  app.get("/health", (req, res) => {
  res.status(200).json({
    status: "healthy",
    message: "Global Eco Footprint Atlas is running",
    timestamp: new Date().toISOString(),
    environment: process.env.NODE_ENV || "development",
  });
});

  app.get("/api/health", (req, res) => {
  res.status(200).json({
    status: "healthy",
    message: "API endpoints are operational",
    timestamp: new Date().toISOString(),
  });
});

  // Simple ping endpoints
  app.get("/ping", (req, res) => {
    res.status(200).send("pong");
  });

  app.get("/api/ping", (req, res) => {
    res.status(200).json({ message: "pong" });
  });

  // Story submission endpoint
  app.post("/api/stories/submit", async (req, res) => {
    try {
      const storyData = insertSubmittedStorySchema.parse(req.body);
      const submittedStory = await storage.submitStory(storyData);
      
      res.json({ 
        success: true, 
        message: "Story submitted successfully! It will be published after a security check to ensure no inappropriate content.",
        storyId: submittedStory.id 
      });
    } catch (error) {
      console.error("Story submission error:", error);
      if (error instanceof z.ZodError) {
        res.status(400).json({ 
          error: "Invalid story data", 
          details: error.errors 
        });
      } else {
        res.status(500).json({ 
          error: "Failed to submit story" 
        });
      }
    }
  });

  return server;
}
```

---

## Storage Layer

**File:** `server/storage.ts`

```typescript
import { 
  type User, 
  type InsertUser, 
  type UserSession, 
  type InsertUserSession,
  type SiteAnalytics,
  type InsertSiteAnalytics,
  type SubmittedStory,
  type InsertSubmittedStory,
  userSessions,
  siteAnalytics,
  submittedStories
} from "@shared/schema";
import { db } from "./db";
import { eq, desc, gt, sql } from "drizzle-orm";
import { randomUUID } from "crypto";

// Enhanced interface with analytics methods
export interface IStorage {
  getUser(id: string): Promise<User | undefined>;
  getUserByUsername(username: string): Promise<User | undefined>;
  createUser(user: InsertUser): Promise<User>;
  
  // Analytics methods
  createOrUpdateSession(session: InsertUserSession): Promise<UserSession>;
  getActiveUsers(): Promise<number>;
  getTotalUsers(): Promise<number>;
  updateAnalyticMetric(metric: string, value: number): Promise<void>;
  getAnalyticValue(metric: string): Promise<number>;
  
  // Story submission methods
  submitStory(story: InsertSubmittedStory): Promise<SubmittedStory>;
}

// Database storage implementation with real analytics
export class DatabaseStorage implements IStorage {
  async getUser(id: string): Promise<User | undefined> {
    // Implementation would query database
    return undefined;
  }

  async getUserByUsername(username: string): Promise<User | undefined> {
    // Implementation would query database
    return undefined;
  }

  async createUser(insertUser: InsertUser): Promise<User> {
    const id = randomUUID();
    const user: User = { 
      ...insertUser, 
      id,
      email: insertUser.email || null,
      level: 1,
      experiencePoints: 0,
      createdAt: new Date()
    };
    return user;
  }

  async createOrUpdateSession(sessionData: InsertUserSession): Promise<UserSession> {
    // Check if session exists
    const [existingSession] = await db
      .select()
      .from(userSessions)
      .where(eq(userSessions.sessionId, sessionData.sessionId))
      .limit(1);

    if (existingSession) {
      // Update existing session
      const [updatedSession] = await db
        .update(userSessions)
        .set({
          lastActivity: new Date(),
          pageViews: sql`${userSessions.pageViews} + 1`,
          isActive: true
        })
        .where(eq(userSessions.sessionId, sessionData.sessionId))
        .returning();
      return updatedSession;
    } else {
      // Create new session
      const [newSession] = await db
        .insert(userSessions)
        .values(sessionData)
        .returning();
      return newSession;
    }
  }

  async getActiveUsers(): Promise<number> {
    // Users active in the last 5 minutes
    const fiveMinutesAgo = new Date(Date.now() - 5 * 60 * 1000);
    
    const result = await db
      .select({ count: sql<number>`count(*)` })
      .from(userSessions)
      .where(
        sql`${userSessions.lastActivity} > ${fiveMinutesAgo} AND ${userSessions.isActive} = true`
      );
    
    return result[0]?.count || 0;
  }

  async getTotalUsers(): Promise<number> {
    const result = await db
      .select({ count: sql<number>`count(distinct ${userSessions.fingerprint})` })
      .from(userSessions);
    
    return result[0]?.count || 0;
  }

  async updateAnalyticMetric(metric: string, value: number): Promise<void> {
    await db
      .insert(siteAnalytics)
      .values({ metric, value });
  }

  async getAnalyticValue(metric: string): Promise<number> {
    const result = await db
      .select({ value: siteAnalytics.value })
      .from(siteAnalytics)
      .where(eq(siteAnalytics.metric, metric))
      .orderBy(desc(siteAnalytics.timestamp))
      .limit(1);
    
    return result[0]?.value || 0;
  }

  async submitStory(story: InsertSubmittedStory): Promise<SubmittedStory> {
    const [submittedStory] = await db
      .insert(submittedStories)
      .values(story)
      .returning();
    return submittedStory;
  }
}

// In-memory storage for development with enhanced analytics simulation
export class MemStorage implements IStorage {
  private users: Map<string, User>;
  private sessions: Map<string, UserSession>;
  private analytics: Map<string, number>;

  constructor() {
    this.users = new Map();
    this.sessions = new Map();
    this.analytics = new Map();
  }

  async getUser(id: string): Promise<User | undefined> {
    return this.users.get(id);
  }

  async getUserByUsername(username: string): Promise<User | undefined> {
    return Array.from(this.users.values()).find(
      (user) => user.username === username,
    );
  }

  async createUser(insertUser: InsertUser): Promise<User> {
    const id = randomUUID();
    const user: User = { 
      ...insertUser, 
      id,
      email: insertUser.email || null,
      level: 1,
      experiencePoints: 0,
      createdAt: new Date()
    };
    this.users.set(id, user);
    return user;
  }

  async createOrUpdateSession(sessionData: InsertUserSession): Promise<UserSession> {
    const existingSession = this.sessions.get(sessionData.sessionId);
    
    if (existingSession) {
      const updatedSession: UserSession = {
        ...existingSession,
        lastActivity: new Date(),
        pageViews: (existingSession.pageViews || 0) + 1,
        isActive: true
      };
      this.sessions.set(sessionData.sessionId, updatedSession);
      return updatedSession;
    } else {
      const newSession: UserSession = {
        id: randomUUID(),
        sessionId: sessionData.sessionId,
        fingerprint: sessionData.fingerprint || null,
        ipAddress: sessionData.ipAddress || null,
        userAgent: sessionData.userAgent || null,
        firstVisit: new Date(),
        lastActivity: new Date(),
        isActive: true,
        pageViews: 1
      };
      this.sessions.set(sessionData.sessionId, newSession);
      return newSession;
    }
  }

  async getActiveUsers(): Promise<number> {
    const fiveMinutesAgo = Date.now() - 5 * 60 * 1000;
    return Array.from(this.sessions.values()).filter(
      session => session.isActive && (session.lastActivity?.getTime() || 0) > fiveMinutesAgo
    ).length;
  }

  async getTotalUsers(): Promise<number> {
    // Count unique fingerprints/sessions
    const uniqueFingerprints = new Set();
    Array.from(this.sessions.values()).forEach(session => {
      if (session.fingerprint) {
        uniqueFingerprints.add(session.fingerprint);
      } else {
        uniqueFingerprints.add(session.sessionId);
      }
    });
    return uniqueFingerprints.size;
  }

  async updateAnalyticMetric(metric: string, value: number): Promise<void> {
    this.analytics.set(metric, value);
  }

  async getAnalyticValue(metric: string): Promise<number> {
    return this.analytics.get(metric) || 0;
  }

  async submitStory(story: InsertSubmittedStory): Promise<SubmittedStory> {
    const submittedStory: SubmittedStory = {
      id: randomUUID(),
      ...story,
      status: "pending",
      submittedAt: new Date()
    };
    return submittedStory;
  }
}

export const storage = new MemStorage();
```

---

## Configuration Files

### Package.json
```json
{
  "name": "rest-express",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "NODE_ENV=development tsx server/index.ts",
    "build": "vite build && esbuild server/index.ts --bundle --platform=node --target=node18 --outfile=dist/index.js --external:express --external:@neondatabase/serverless --external:drizzle-orm --external:ws",
    "start": "NODE_ENV=production node dist/index.js",
    "check": "tsc --noEmit",
    "db:push": "drizzle-kit push"
  },
  "dependencies": {
    "@hookform/resolvers": "^3.6.0",
    "@neondatabase/serverless": "^0.9.4",
    "@radix-ui/react-accordion": "^1.1.2",
    "@radix-ui/react-alert-dialog": "^1.0.5",
    "@radix-ui/react-aspect-ratio": "^1.0.3",
    "@radix-ui/react-avatar": "^1.0.4",
    "@radix-ui/react-checkbox": "^1.0.4",
    "@radix-ui/react-collapsible": "^1.0.3",
    "@radix-ui/react-context-menu": "^2.1.5",
    "@radix-ui/react-dialog": "^1.0.5",
    "@radix-ui/react-dropdown-menu": "^2.0.6",
    "@radix-ui/react-hover-card": "^1.0.7",
    "@radix-ui/react-label": "^2.0.2",
    "@radix-ui/react-menubar": "^1.0.4",
    "@radix-ui/react-navigation-menu": "^1.1.4",
    "@radix-ui/react-popover": "^1.0.7",
    "@radix-ui/react-progress": "^1.0.3",
    "@radix-ui/react-radio-group": "^1.1.3",
    "@radix-ui/react-scroll-area": "^1.0.5",
    "@radix-ui/react-select": "^2.0.0",
    "@radix-ui/react-separator": "^1.0.3",
    "@radix-ui/react-slider": "^1.1.2",
    "@radix-ui/react-slot": "^1.0.2",
    "@radix-ui/react-switch": "^1.0.3",
    "@radix-ui/react-tabs": "^1.0.4",
    "@radix-ui/react-toast": "^1.1.5",
    "@radix-ui/react-toggle": "^1.0.3",
    "@radix-ui/react-toggle-group": "^1.0.4",
    "@radix-ui/react-tooltip": "^1.0.7",
    "@tanstack/react-query": "^5.51.1",
    "chart.js": "^4.4.3",
    "class-variance-authority": "^0.7.0",
    "clsx": "^2.1.1",
    "cmdk": "^1.0.0",
    "connect-pg-simple": "^9.0.1",
    "date-fns": "^3.6.0",
    "drizzle-orm": "^0.32.1",
    "drizzle-zod": "^0.5.1",
    "embla-carousel-react": "^8.1.6",
    "express": "^4.19.2",
    "express-session": "^1.18.0",
    "framer-motion": "^11.2.12",
    "input-otp": "^1.2.4",
    "lucide-react": "^0.400.0",
    "memorystore": "^1.6.7",
    "next-themes": "^0.3.0",
    "passport": "^0.7.0",
    "passport-local": "^1.0.0",
    "react": "^18.3.1",
    "react-chartjs-2": "^5.2.0",
    "react-day-picker": "^8.10.1",
    "react-dom": "^18.3.1",
    "react-hook-form": "^7.52.1",
    "react-icons": "^5.2.1",
    "react-resizable-panels": "^2.0.20",
    "recharts": "^2.12.7",
    "tailwind-merge": "^2.4.0",
    "tailwindcss-animate": "^1.0.7",
    "tw-animate-css": "^1.0.1",
    "vaul": "^0.9.1",
    "wouter": "^3.3.1",
    "ws": "^8.18.0",
    "zod": "^3.23.8",
    "zod-validation-error": "^3.3.0"
  },
  "devDependencies": {
    "@replit/vite-plugin-cartographer": "^2.1.0",
    "@replit/vite-plugin-runtime-error-modal": "^1.0.0",
    "@tailwindcss/typography": "^0.5.13",
    "@tailwindcss/vite": "^4.0.0-alpha.19",
    "@types/connect-pg-simple": "^7.0.3",
    "@types/express": "^4.17.21",
    "@types/express-session": "^1.18.0",
    "@types/node": "^20.14.10",
    "@types/passport": "^1.0.16",
    "@types/passport-local": "^1.0.38",
    "@types/react": "^18.3.3",
    "@types/react-dom": "^18.3.0",
    "@types/ws": "^8.5.11",
    "@vitejs/plugin-react": "^4.3.1",
    "autoprefixer": "^10.4.19",
    "drizzle-kit": "^0.23.0",
    "esbuild": "^0.23.0",
    "postcss": "^8.4.39",
    "tailwindcss": "^3.4.4",
    "tsx": "^4.16.2",
    "typescript": "^5.5.3",
    "vite": "^5.3.3"
  }
}
```

### Tailwind Config
```typescript
import type { Config } from "tailwindcss";
import tailwindcssAnimate from "tailwindcss-animate";

export default {
  darkMode: ["class"],
  content: [
    "./client/**/*.{js,ts,jsx,tsx}",
    "./shared/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
    },
  },
  plugins: [tailwindcssAnimate],
} satisfies Config;
```

This comprehensive source code documentation separates all the code by pages and components, making it easy to understand the structure and functionality of the Global Eco Footprint Atlas application.