# Question 04 (Answer)

A **SHA-1 Hash** in Git is a 40-character hexadecimal string (for example, `a1b2c3d4e5f6`) that acts as a mathematically unique identifier, or "receipt number", for a specific commit snapshot.

Its importance to the "Photo Album" (the Repository) stems from data integrity and immutability. When you execute a commit, Git runs the entire contents of the staged files, along with the author metadata and timestamp, through a cryptographic hashing algorithm to generate this unique string.

Because of how the cryptography works, it is mathematically impossible to silently alter even a single character in a past commit without the resulting SHA-1 Hash changing entirely. This guarantees that your Git history is an indestructible, verifiable record. If a specific snapshot is identified by a specific SHA-1 Hash, you can trust with absolute certainty that the code within it has not been tampered with since the moment the snapshot was created.
