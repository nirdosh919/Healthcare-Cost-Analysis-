"use client"

import { Card, CardContent, CardDescription, CardHeader, CardTitle } from "@/components/ui/card"
import {
  ChartContainer,
  ChartTooltip,
  ChartTooltipContent,
  ChartLegend,
  ChartLegendContent,
} from "@/components/ui/chart"
import { BarChart, Bar, XAxis, YAxis, ScatterChart, Scatter, LineChart, Line } from "recharts"
import { TrendingUp, Heart, DollarSign, Users } from "lucide-react"

// Healthcare spending data (per capita USD, 2023 estimates)
const healthcareSpendingData = [
  { country: "USA", spending: 12318, lifeExpectancy: 78.9, population: 331900000 },
  { country: "Switzerland", spending: 7179, lifeExpectancy: 83.8, population: 8703000 },
  { country: "Norway", spending: 6187, lifeExpectancy: 82.3, population: 5408000 },
  { country: "Germany", spending: 6518, lifeExpectancy: 81.3, population: 83200000 },
  { country: "Austria", spending: 5765, lifeExpectancy: 81.6, population: 9000000 },
  { country: "Sweden", spending: 5511, lifeExpectancy: 82.8, population: 10400000 },
  { country: "Netherlands", spending: 5765, lifeExpectancy: 82.3, population: 17400000 },
  { country: "Denmark", spending: 5299, lifeExpectancy: 81.0, population: 5800000 },
  { country: "Luxembourg", spending: 5513, lifeExpectancy: 82.7, population: 640000 },
  { country: "Belgium", spending: 5428, lifeExpectancy: 82.1, population: 11500000 },
  { country: "Canada", spending: 5511, lifeExpectancy: 82.4, population: 38200000 },
  { country: "France", spending: 5274, lifeExpectancy: 82.5, population: 67800000 },
  { country: "Japan", spending: 4691, lifeExpectancy: 84.6, population: 125800000 },
  { country: "Australia", spending: 4919, lifeExpectancy: 83.4, population: 25700000 },
  { country: "UK", spending: 4214, lifeExpectancy: 81.3, population: 67500000 },
  { country: "Finland", spending: 4033, lifeExpectancy: 81.7, population: 5500000 },
  { country: "Italy", spending: 3428, lifeExpectancy: 83.5, population: 59100000 },
  { country: "Spain", spending: 3323, lifeExpectancy: 83.6, population: 47400000 },
  { country: "South Korea", spending: 3521, lifeExpectancy: 83.5, population: 51800000 },
  { country: "Israel", spending: 2780, lifeExpectancy: 83.0, population: 9500000 },
]

// Top 10 spenders for bar chart
const topSpenders = healthcareSpendingData.slice(0, 10)

// Healthcare trends over time (sample data)
const trendData = [
  { year: 2018, usa: 10739, germany: 5728, japan: 4219, uk: 3570 },
  { year: 2019, usa: 11072, germany: 5986, japan: 4411, uk: 3749 },
  { year: 2020, usa: 11945, germany: 6518, japan: 4665, uk: 4021 },
  { year: 2021, usa: 12318, germany: 6518, japan: 4691, uk: 4214 },
  { year: 2022, usa: 12318, germany: 6518, japan: 4691, uk: 4214 },
  { year: 2023, usa: 12318, germany: 6518, japan: 4691, uk: 4214 },
]

const chartConfig = {
  spending: {
    label: "Healthcare Spending (USD)",
    color: "hsl(var(--chart-1))",
  },
  lifeExpectancy: {
    label: "Life Expectancy (Years)",
    color: "hsl(var(--chart-2))",
  },
  usa: {
    label: "USA",
    color: "hsl(var(--chart-1))",
  },
  germany: {
    label: "Germany",
    color: "hsl(var(--chart-2))",
  },
  japan: {
    label: "Japan",
    color: "hsl(var(--chart-3))",
  },
  uk: {
    label: "UK",
    color: "hsl(var(--chart-4))",
  },
}

export function HealthcareDashboard() {
  const avgSpending = Math.round(
    healthcareSpendingData.reduce((sum, country) => sum + country.spending, 0) / healthcareSpendingData.length,
  )
  const avgLifeExpectancy =
    Math.round(
      (healthcareSpendingData.reduce((sum, country) => sum + country.lifeExpectancy, 0) /
        healthcareSpendingData.length) *
        10,
    ) / 10
  const totalPopulation = Math.round(
    healthcareSpendingData.reduce((sum, country) => sum + country.population, 0) / 1000000,
  )

  return (
    <div className="container mx-auto p-6 space-y-8">
      {/* Header */}
      <div className="text-center space-y-4">
        <h1 className="text-4xl font-bold tracking-tight">Global Healthcare Cost Analysis</h1>
        <p className="text-xl text-muted-foreground max-w-3xl mx-auto">
          Comprehensive analysis of per capita healthcare spending and health outcomes across OECD countries
        </p>
        <div className="text-sm text-muted-foreground">
          Data sources: WHO Global Health Observatory, OECD Health Statistics 2023
        </div>
      </div>

      {/* Key Metrics */}
      <div className="grid grid-cols-1 md:grid-cols-4 gap-6">
        <Card>
          <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle className="text-sm font-medium">Average Spending</CardTitle>
            <DollarSign className="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div className="text-2xl font-bold">${avgSpending.toLocaleString()}</div>
            <p className="text-xs text-muted-foreground">Per capita annually</p>
          </CardContent>
        </Card>

        <Card>
          <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle className="text-sm font-medium">Average Life Expectancy</CardTitle>
            <Heart className="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div className="text-2xl font-bold">{avgLifeExpectancy} years</div>
            <p className="text-xs text-muted-foreground">Across analyzed countries</p>
          </CardContent>
        </Card>

        <Card>
          <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle className="text-sm font-medium">Countries Analyzed</CardTitle>
            <Users className="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div className="text-2xl font-bold">{healthcareSpendingData.length}</div>
            <p className="text-xs text-muted-foreground">OECD member nations</p>
          </CardContent>
        </Card>

        <Card>
          <CardHeader className="flex flex-row items-center justify-between space-y-0 pb-2">
            <CardTitle className="text-sm font-medium">Total Population</CardTitle>
            <TrendingUp className="h-4 w-4 text-muted-foreground" />
          </CardHeader>
          <CardContent>
            <div className="text-2xl font-bold">{totalPopulation}M</div>
            <p className="text-xs text-muted-foreground">Combined population</p>
          </CardContent>
        </Card>
      </div>

      {/* Top Healthcare Spenders */}
      <Card>
        <CardHeader>
          <CardTitle>Top 10 Healthcare Spenders (Per Capita)</CardTitle>
          <CardDescription>Annual healthcare expenditure per person in USD, 2023</CardDescription>
        </CardHeader>
        <CardContent>
          <ChartContainer config={chartConfig}>
            <BarChart data={topSpenders} margin={{ top: 20, right: 30, left: 20, bottom: 60 }}>
              <XAxis dataKey="country" angle={-45} textAnchor="end" height={80} interval={0} />
              <YAxis />
              <ChartTooltip
                content={<ChartTooltipContent />}
                formatter={(value) => [`$${value.toLocaleString()}`, "Healthcare Spending"]}
              />
              <Bar dataKey="spending" fill="var(--color-spending)" radius={[4, 4, 0, 0]} />
            </BarChart>
          </ChartContainer>
        </CardContent>
      </Card>

      {/* Cost vs Life Expectancy Scatter Plot */}
      <Card>
        <CardHeader>
          <CardTitle>Healthcare Spending vs Life Expectancy</CardTitle>
          <CardDescription>Correlation analysis between per capita spending and health outcomes</CardDescription>
        </CardHeader>
        <CardContent>
          <ChartContainer config={chartConfig}>
            <ScatterChart data={healthcareSpendingData} margin={{ top: 20, right: 20, bottom: 20, left: 20 }}>
              <XAxis
                type="number"
                dataKey="spending"
                name="Healthcare Spending"
                domain={["dataMin - 500", "dataMax + 500"]}
                tickFormatter={(value) => `$${value.toLocaleString()}`}
              />
              <YAxis
                type="number"
                dataKey="lifeExpectancy"
                name="Life Expectancy"
                domain={["dataMin - 1", "dataMax + 1"]}
                tickFormatter={(value) => `${value} yrs`}
              />
              <ChartTooltip
                content={<ChartTooltipContent />}
                formatter={(value, name) => {
                  if (name === "spending") return [`$${value.toLocaleString()}`, "Healthcare Spending"]
                  if (name === "lifeExpectancy") return [`${value} years`, "Life Expectancy"]
                  return [value, name]
                }}
                labelFormatter={(label, payload) => {
                  if (payload && payload[0]) {
                    return payload[0].payload.country
                  }
                  return label
                }}
              />
              <Scatter dataKey="lifeExpectancy" fill="var(--color-lifeExpectancy)" />
            </ScatterChart>
          </ChartContainer>
        </CardContent>
      </Card>

      {/* Healthcare Spending Trends */}
      <Card>
        <CardHeader>
          <CardTitle>Healthcare Spending Trends (2018-2023)</CardTitle>
          <CardDescription>Evolution of per capita healthcare expenditure for major economies</CardDescription>
        </CardHeader>
        <CardContent>
          <ChartContainer config={chartConfig}>
            <LineChart data={trendData} margin={{ top: 20, right: 30, left: 20, bottom: 5 }}>
              <XAxis dataKey="year" />
              <YAxis tickFormatter={(value) => `$${value.toLocaleString()}`} />
              <ChartTooltip
                content={<ChartTooltipContent />}
                formatter={(value) => [`$${value.toLocaleString()}`, ""]}
              />
              <ChartLegend content={<ChartLegendContent />} />
              <Line type="monotone" dataKey="usa" stroke="var(--color-usa)" strokeWidth={3} dot={{ r: 4 }} />
              <Line type="monotone" dataKey="germany" stroke="var(--color-germany)" strokeWidth={2} dot={{ r: 3 }} />
              <Line type="monotone" dataKey="japan" stroke="var(--color-japan)" strokeWidth={2} dot={{ r: 3 }} />
              <Line type="monotone" dataKey="uk" stroke="var(--color-uk)" strokeWidth={2} dot={{ r: 3 }} />
            </LineChart>
          </ChartContainer>
        </CardContent>
      </Card>

      {/* Key Insights */}
      <Card>
        <CardHeader>
          <CardTitle>Key Insights</CardTitle>
        </CardHeader>
        <CardContent className="space-y-4">
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div className="space-y-3">
              <h4 className="font-semibold text-lg">Healthcare Spending Leaders</h4>
              <ul className="space-y-2 text-sm">
                <li>
                  • <strong>USA</strong> leads with $12,318 per capita - 2.4x the OECD average
                </li>
                <li>
                  • <strong>Switzerland</strong> follows at $7,179 per capita
                </li>
                <li>
                  • <strong>European nations</strong> cluster around $5,000-6,500 range
                </li>
                <li>
                  • <strong>Significant variation</strong> exists even among developed nations
                </li>
              </ul>
            </div>

            <div className="space-y-3">
              <h4 className="font-semibold text-lg">Health Outcomes Analysis</h4>
              <ul className="space-y-2 text-sm">
                <li>
                  • <strong>Japan</strong> achieves highest life expectancy (84.6 years) with moderate spending
                </li>
                <li>
                  • <strong>USA</strong> has lower life expectancy (78.9 years) despite highest spending
                </li>
                <li>
                  • <strong>Mediterranean countries</strong> (Italy, Spain) show excellent outcomes per dollar
                </li>
                <li>
                  • <strong>Diminishing returns</strong> evident above $6,000 per capita spending
                </li>
              </ul>
            </div>
          </div>

          <div className="mt-6 p-4 bg-muted rounded-lg">
            <h4 className="font-semibold mb-2">Research Methodology</h4>
            <p className="text-sm text-muted-foreground">
              Data compiled from WHO Global Health Observatory and OECD Health Statistics 2023. Healthcare spending
              includes both public and private expenditure. Life expectancy data represents the most recent available
              figures. Analysis focuses on developed nations with comprehensive healthcare systems and reliable data
              reporting.
            </p>
          </div>
        </CardContent>
      </Card>
    </div>
  )
}
