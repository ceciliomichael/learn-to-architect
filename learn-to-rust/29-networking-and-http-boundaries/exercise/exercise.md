# Exercise: Fetch a bounded response

Create a Cargo project and add reqwest plus Tokio as shown in the lesson.

1. Build one client with a ten-second total timeout.
2. Request `https://example.com/`.
3. Turn unsuccessful HTTP status codes into errors.
4. Read the response with `chunk()` and stop with an error if it exceeds 100,000 bytes.
5. Print the final byte count. Report errors to stderr and exit unsuccessfully.
