# Option 04: CLI Markdown Note & Snippet Manager

**Difficulty:** Intermediate
**Primary Concepts:** Async Node.js I/O (`fs/promises`), interfaces, project structure, error handling, JSON storage

---

## Project Brief

You are building a command-line tool that developers can use to save, tag, search, and manage code snippets and markdown notes directly from their terminal.

Unlike web apps where data lives on a server, CLI tools interact directly with the local file system. You will manage local `.json` and `.md` files asynchronously, handling file corruption, missing directories, and concurrent access gracefully.

---

## Domain

A **Note** consists of metadata and markdown content:

```typescript
interface NoteMetadata {
  id: string;             // Short hash or timestamp string
  title: string;
  tags: string[];
  language?: string;      // e.g., "typescript", "sql", "bash" (optional)
  createdAt: string;      // ISO string
  updatedAt: string;
}

interface Note extends NoteMetadata {
  content: string;        // Raw markdown or code snippet
}
```

---

## Core Requirements

Build a `NoteRepository` and `NoteService` supporting these operations:

```typescript
// All operations must interact with local files asynchronously using fs/promises.
// Store metadata in a central `index.json` file inside a local `.notes/` folder.
// Store note body contents as individual files: `.notes/files/{id}.md`.

async init(): Promise<void>
// Ensures `.notes/` and `.notes/files/` directories exist along with `index.json`.

async createNote(input: { title: string; content: string; tags: string[]; language?: string }): Promise<Note>

async getNote(id: string): Promise<Note>
// Reads metadata from index.json and content from the markdown file.
// Throws NoteNotFoundError if missing.

async listNotes(filter?: { tag?: string; language?: string; search?: string }): Promise<NoteMetadata[]>
// If 'search' is provided, it must search inside both titles AND raw content.

async updateNote(id: string, input: Partial<{ title: string; content: string; tags: string[]; language: string }>): Promise<Note>

async deleteNote(id: string): Promise<void>
// Deletes both metadata entry and the local .md file.

async exportToHtml(id: string, outputPath: string): Promise<void>
// Simple converter turning markdown code blocks (```ts ... ```) into HTML <pre><code> blocks
// and saving to the requested output path.
```

---

## Robust Error Handling Requirements

CLI file operations fail in specific ways. You must handle and wrap standard Node.js `ENOENT` (file not found) and `EACCES` (permission denied) errors into custom, human-readable domain errors:

- `NoteNotFoundError`
- `StoragePermissionError`
- `CorruptedIndexError` (thrown if `index.json` contains invalid JSON upon reading)

If `index.json` is corrupted, your app should not crash violently with a raw `SyntaxError`. It should catch it, backup the corrupted file to `index.json.bak`, and reinitialize a clean index automatically while logging a warning.

---

## File Structure You Must Use

```
src/
├── types/
│   └── note.ts
├── errors/
│   └── storageErrors.ts
├── storage/
│   └── fileSystem.ts       -  Raw fs/promises wrapper handling paths and init
├── repositories/
│   └── noteRepository.ts   -  Manages index.json and file reads/writes
├── services/
│   └── noteService.ts      -  Business rules, filtering, searching
└── index.ts                -  Simulated CLI execution flow
```

---

## What Your Final index.ts Should Demonstrate

Simulate a user session:
1. Initialize storage.
2. Create 3 distinct notes (e.g., a TypeScript snippet, a SQL query snippet, and a general meeting note).
3. List all notes filtered by the tag `"code"`.
4. Search for a keyword that appears only inside the raw content of one note.
5. Update the title and tags of one note.
6. Export one snippet to an HTML file and verify creation.
7. Delete a note and verify it disappears from listings.
