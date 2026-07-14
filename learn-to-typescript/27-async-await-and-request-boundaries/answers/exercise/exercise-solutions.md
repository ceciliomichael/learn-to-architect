# Module 27 Exercise Solutions

## Exercise 1

```typescript
async function createLabel(): Promise<string> {
  const value = await Promise.resolve(5);
  const doubled = value * 2;
  return `Result: ${doubled}`;
}
```

## Exercise 2

```typescript
async function fetchJson(url: string): Promise<unknown> {
  const response = await fetch(url);

  if (!response.ok) {
    throw new Error(`Request failed with status ${response.status}`);
  }

  const value: unknown = await response.json();
  return value;
}
```

## Exercise 3

```typescript
interface WeatherReading {
  city: string;
  temperature: number;
}

function isWeatherReading(value: unknown): value is WeatherReading {
  if (typeof value !== "object" || value === null || Array.isArray(value)) {
    return false;
  }

  const record = value as { [key: string]: unknown };
  return typeof record["city"] === "string" && typeof record["temperature"] === "number";
}

async function fetchWeather(url: string): Promise<WeatherReading> {
  const value = await fetchJson(url);

  if (!isWeatherReading(value)) {
    throw new Error("Invalid weather response");
  }

  return value;
}
```

## Exercise 4

User then orders is sequential. Independent weather and news can run with `Promise.all`. A generated id required by step 2 makes those saves sequential.

## Exercise 5

```typescript
const results = await Promise.allSettled([
  Promise.resolve("first"),
  Promise.reject(new Error("second failed")),
  Promise.resolve("third"),
]);

for (const result of results) {
  if (result.status === "fulfilled") {
    console.log(`Success: ${result.value}`);
  } else {
    console.log("Failure", result.reason);
  }
}
```
