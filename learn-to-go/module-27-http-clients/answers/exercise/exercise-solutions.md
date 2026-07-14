# Exercise Solutions: HTTP Clients

```go
package main

import (
	"context"
	"encoding/json"
	"fmt"
	"io"
	"net/http"
	"net/http/httptest"
	"strings"
	"time"
)

type Status struct {
	Message string `json:"message"`
}

func fetch(ctx context.Context, client *http.Client, endpoint string) (Status, error) {
	request, err := http.NewRequestWithContext(ctx, http.MethodGet, endpoint, nil)
	if err != nil {
		return Status{}, fmt.Errorf("create request: %w", err)
	}
	response, err := client.Do(request)
	if err != nil {
		return Status{}, fmt.Errorf("perform request: %w", err)
	}
	defer response.Body.Close()
	if response.StatusCode != http.StatusOK {
		return Status{}, fmt.Errorf("unexpected status: %d", response.StatusCode)
	}
	if !strings.HasPrefix(response.Header.Get("Content-Type"), "application/json") {
		return Status{}, fmt.Errorf("unexpected content type")
	}
	decoder := json.NewDecoder(io.LimitReader(response.Body, 4096))
	var status Status
	if err := decoder.Decode(&status); err != nil {
		return Status{}, fmt.Errorf("decode response: %w", err)
	}
	if strings.TrimSpace(status.Message) == "" {
		return Status{}, fmt.Errorf("empty message")
	}
	return status, nil
}

func main() {
	server := httptest.NewServer(http.HandlerFunc(func(writer http.ResponseWriter, request *http.Request) {
		writer.Header().Set("Content-Type", "application/json")
		fmt.Fprint(writer, `{"message":"ready"}`)
	}))
	defer server.Close()
	client := &http.Client{Timeout: time.Second}
	status, err := fetch(context.Background(), client, server.URL)
	if err != nil {
		fmt.Println("request failed:", err)
		return
	}
	fmt.Println(status.Message)
}
```

For the cancellation exercise, make the handler wait longer than the client timeout and confirm the returned error reports a deadline. Keep the server local and deterministic.
