# Option 05: Type-Safe ETL Data Pipeline Engine

**Difficulty:** Advanced
**Primary Concepts:** Generics, async pipelines, iterator patterns, `Promise.allSettled`, error resilience

---

## Project Brief

Modern data engineering relies on Extract-Transform-Load (ETL) pipelines. Raw records are ingested from sources (files, APIs), transformed (cleaned, validated, enriched), and loaded into destinations (databases, analytics stores).

In real pipelines, raw data is dirty. If processing 10,000 records, throwing an exception on record #4,102 and aborting the entire run is unacceptable. You will build a **batch processing engine** that processes records concurrently, isolates failures, collects detailed execution metrics, and guarantees strict end-to-end type safety.

---

## Core Pipeline Architecture

Your engine must allow developers to chain typed steps together
```typescript
// Example pipeline usage
const pipeline = new Pipeline<RawUserRecord, CleanUserProfile>()
  .extract(userFileReader)
  .transform(validateUser)
  .transform(enrichWithGeoData)
  .load(databaseWriter);

const report = await pipeline.run({ concurrency: 5 });
```

---

## Required Interfaces

```typescript
interface StepResult<T> {
  success: boolean;
  data?: T;
  error?: string;
}

// Extract step produces an array of initial input records
type Extractor<TIn> = () => Promise<TIn[]>;

// Transform step receives TIn and returns TOut (or throws/returns error)
type Transformer<TIn, TOut> = (item: TIn) => Promise<TOut> | TOut;

// Load step receives the final transformed records
type Loader<TOut> = (batch: TOut[]) => Promise<void>;

interface PipelineReport<TOut> {
  totalExtracted: number;
  successfulLoads: number;
  failedRecords: Array<{
    recordIndex: number;
    failedStep: string;
    reason: string;
    rawInput: unknown;
  }>;
  durationMs: number;
}
```

---

## Core Requirements

Build the `Pipeline<TIn, TCurrent>` class supporting
```typescript
extract(extractor: Extractor<TIn>): Pipeline<TIn, TIn>

transform<TNext>(
  stepName: string,
  transformer: Transformer<TCurrent, TNext>
): Pipeline<TIn, TNext>
// Note how each transform call shifts the pipeline's current type from TCurrent to TNext
load(loader: Loader<TCurrent>): RunnablePipeline<TIn, TCurrent>

run(options?: { batchSize?: number }): Promise<PipelineReport<TCurrent>>
// Executes the pipeline
// 1. Calls extractor.
// 2. Runs records through transformers sequentially per record.
// 3. Collects successful records into batches of size `batchSize` (default 50)
//    and passes them to the loader.
// 4. Catches any error inside any step without stopping other records.
```

---

## File Structure You Must Use

```
src/
├── types/
│   └── pipeline.ts         -  Extractor, Transformer, Loader, Report interfaces
├── engine/
│   ├── stepRunner.ts       -  Isolates error execution per item
│   └── pipeline.ts         -  Chaining and batching orchestration
└── index.ts                -  Demonstration with a mock data pipeline
```

---

## What Your Final index.ts Should Demonstrate

Simulate a dirty dataset ingestion
1. Extract 10 mock records where 2 have invalid email strings and 1 has a negative age.
2. Step 1 (`"sanitize"`): Strip whitespace and lowercase emails.
3. Step 2 (`"validate"`): Throw validation errors for invalid emails or negative ages.
4. Step 3 (`"enrich"`): Map age to an age bracket string (`"youth" | "adult" | "senior"`).
5. Load: Print the successfully transformed batch.
6. Print the full `PipelineReport` showing exactly which indexes failed and why.
