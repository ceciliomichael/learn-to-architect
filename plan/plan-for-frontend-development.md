# Plan for Frontend Development with TypeScript

## Boundary

This 26-module course follows Web Foundations and Learn TypeScript. It teaches the browser platform without React, Vue, or another UI framework. Learners must understand the platform behavior that frameworks later organize.

## Roadmap

### Browser programs and the DOM

- [x] 01: Browser Runtime, Project Setup, and Generated JavaScript
- [x] 02: The DOM Tree and Safe Element Queries
- [x] 03: Create, Update, Move, and Remove Content
- [x] 04: Events, Event Objects, and Default Behavior
- [x] 05: Propagation, Delegation, and Listener Cleanup
- [x] 06: Forms, FormData, and Submission
- [x] 07: Native Validation, Custom Rules, and Accessible Errors
- [x] 08: UI State and Predictable Rendering without a Framework
- [x] 09: Browser Modules, Package Imports, and Build Output

### Browser and network APIs

- [x] 10: URLs, Search Parameters, History, and Navigation
- [x] 11: Fetch, HTTP Results, Headers, and Content Types
- [x] 12: Async Ownership, Abort Signals, Timeouts, and Stale Results
- [x] 13: JSON Boundaries and Runtime Validation
- [x] 14: Local Storage, Session Storage, and Data Lifetimes
- [x] 15: Cookies, Credentials, and Server-Controlled Sessions
- [x] 16: Same-Origin Policy, CORS, CSP, and Trusted Content
- [x] 17: Files, Blobs, Object URLs, and Downloads
- [x] 18: Timers, Animation Frames, and Observer APIs
- [x] 19: Custom Elements, Shadow DOM, and Web Component Boundaries

### Application quality

- [x] 20: Unit Testing Browser Logic
- [x] 21: DOM Integration and End-to-End Testing
- [x] 22: Error States, Logging, and User Recovery
- [x] 23: Rendering, Network, and Asset Performance
- [x] 24: Accessibility in Dynamic Interfaces
- [x] 25: Service Workers, Offline Behavior, and Update Safety
- [x] 26: Build, Configure, Deploy, and Maintain a Browser Application

## Dependency rules

1. Direct DOM updates come before a rendering abstraction.
2. Basic events come before propagation and delegation.
3. HTTP results come before JSON decoding.
4. Abort ownership comes before concurrent search or navigation examples.
5. Storage is never presented as an authorization or secret-storage boundary.
6. Dynamic accessibility comes before framework component courses.

## Verification

- [x] Create 26 modules and five required files per module
- [x] Type-check examples with strict TypeScript DOM libraries
- [x] Run representative browser tests
- [x] Verify security claims against current browser-platform guidance
- [x] Check that no framework API appears
