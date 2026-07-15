# Exercise Solutions: HTTP Servers and Middleware

```go
package main

import (
	"fmt"
	"net/http"
	"net/http/httptest"
	"os"
	"strings"
	"time"
)

func health(writer http.ResponseWriter, request *http.Request) {
	if request.Method != http.MethodGet {
		writer.Header().Set("Allow", http.MethodGet)
		http.Error(writer, "method not allowed", http.StatusMethodNotAllowed)
		return
	}
	writer.Header().Set("Content-Type", "application/json")
	fmt.Fprint(writer, `{"status":"ok"}`)
}

func requestID(next http.Handler) http.Handler {
	return http.HandlerFunc(func(writer http.ResponseWriter, request *http.Request) {
		writer.Header().Set("X-Request-ID", "practice-1")
		next.ServeHTTP(writer, request)
	})
}

func main() {
	handler := requestID(http.HandlerFunc(health))
	recorder := httptest.NewRecorder()
	request := httptest.NewRequest(http.MethodGet, "/health", nil)
	handler.ServeHTTP(recorder, request)
	if recorder.Code != http.StatusOK || recorder.Header().Get("Content-Type") != "application/json" || !strings.Contains(recorder.Body.String(), `"ok"`) {
		fmt.Fprintln(os.Stderr, "health contract failed")
		os.Exit(1)
	}
	fmt.Println(recorder.Code, recorder.Header().Get("X-Request-ID"))

	server := &http.Server{
		Addr:              ":8080",
		Handler:           handler,
		ReadHeaderTimeout: 5 * time.Second,
		ReadTimeout:       10 * time.Second,
		WriteTimeout:      10 * time.Second,
		IdleTimeout:       60 * time.Second,
	}
	fmt.Println("configured server:", server.Addr)
}
```

Production startup runs `ListenAndServe` in an observed goroutine, waits for an operating-system signal, then calls `Shutdown` with a separately timed context. The exercise does not open a public port.
