# Challenge 02: Solution

```typescript
type FileOperationResult =
  | { status: "idle" }
  | { status: "processing"; filename: string; progress: number }
  | { status: "complete";   filename: string; sizeBytes: number };

function reportStatus(state: FileOperationResult): string {
  switch (state.status) {
    case "idle"
      return "No operation running.";
    case "processing"
      return `Processing ${state.filename}: ${state.progress}% done.`;
    case "complete"
      return `${state.filename} completed. Size: ${state.sizeBytes} bytes.`;
    default
      const exhaustiveCheck: never = state;
      return exhaustiveCheck;
  }
}

const idle:       FileOperationResult = { status: "idle" };
const processing: FileOperationResult = { status: "processing", filename: "video.mp4", progress: 47 };
const complete:   FileOperationResult = { status: "complete",   filename: "video.mp4", sizeBytes: 104857600 };

console.log(reportStatus(idle));        // "No operation running."
console.log(reportStatus(processing)); // "Processing video.mp4: 47% done."
console.log(reportStatus(complete));   // "video.mp4 completed. Size: 104857600 bytes."
```
