# Challenge 03: Solution

```typescript
interface WordMap {
  [word: string]: string;
}

const spanishDict: WordMap = {
  hello: "hola",
  cat: "gato",
  dog: "perro",
  water: "agua",
  house: "casa"
};

// Accessing a translation using dot notation:
console.log(spanishDict.hello); // "hola"
console.log(spanishDict.cat);   // "gato"

// spanishDict.wordCount = 5;
// ERROR: Type 'number' is not assignable to type 'string'.
// The index signature says ALL values must be strings.

// Adding a new word pair after the initial declaration (valid):
spanishDict.fire = "fuego";
console.log(spanishDict.fire); // "fuego"
```
