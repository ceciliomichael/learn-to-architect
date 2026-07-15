# Exercise Solution: Effects for External Synchronization

```tsx
import { useEffect } from "react";
type Connection = { disconnect: () => void };
type RoomProps = { roomId: string; connect: (roomId: string) => Connection };
export function Room({ roomId, connect }: RoomProps) {
  useEffect(() => {
    const connection = connect(roomId);
    return () => connection.disconnect();
  }, [connect, roomId]);
  return <p>Connected to {roomId}.</p>;
}
```

## Why this works

Effects synchronize React state with an external system and return cleanup for subscriptions or owned resources. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.