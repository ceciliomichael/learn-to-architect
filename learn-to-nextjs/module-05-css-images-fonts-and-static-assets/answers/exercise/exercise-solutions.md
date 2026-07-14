# Exercise Solution: CSS, Images, Fonts, and Static Assets

```tsx
import Image from "next/image";
export function ProfileImage() {
  return <Image src="/profile.jpg" alt="Ada at her desk" width={320} height={240} />;
}
```

## Why this works

Use scoped or global CSS deliberately, next/image for sized and optimized images, next/font for controlled font loading, and public for files that truly need stable public URLs. The reference keeps the example intentionally small so the lesson boundary remains visible. A larger solution is correct only when it preserves the same ownership, accessibility, runtime validation, and recovery rules.