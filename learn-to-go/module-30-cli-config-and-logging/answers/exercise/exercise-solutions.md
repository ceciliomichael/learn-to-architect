# Exercise Solutions: Command-Line Programs, Configuration, and Logging

```go
package main

import (
	"flag"
	"fmt"
	"io"
	"log/slog"
	"os"
	"strings"
)

func run(arguments []string, output, diagnostics io.Writer) int {
	flags := flag.NewFlagSet("reader", flag.ContinueOnError)
	flags.SetOutput(diagnostics)
	limit := flags.Int("limit", 20, "maximum bytes to print")
	verbose := flags.Bool("verbose", false, "enable diagnostic logging")
	if err := flags.Parse(arguments); err != nil {
		return 2
	}
	if flags.NArg() != 1 || *limit < 1 || *limit > 1_000_000 {
		fmt.Fprintln(diagnostics, "usage: reader [-limit N] path")
		return 2
	}
	mode := strings.ToLower(strings.TrimSpace(os.Getenv("APP_MODE")))
	if mode != "development" && mode != "production" {
		fmt.Fprintln(diagnostics, "APP_MODE must be development or production")
		return 2
	}
	level := slog.LevelInfo
	if *verbose {
		level = slog.LevelDebug
	}
	logger := slog.New(slog.NewTextHandler(diagnostics, &slog.HandlerOptions{Level: level}))
	file, err := os.Open(flags.Arg(0))
	if err != nil {
		logger.Error("read failed", "operation", "read input")
		return 1
	}
	defer file.Close()
	content, err := io.ReadAll(io.LimitReader(file, int64(*limit)+1))
	if err != nil {
		logger.Error("read failed", "operation", "read input")
		return 1
	}
	if len(content) > *limit {
		content = content[:*limit]
	}
	logger.Info("read completed", "bytes", len(content), "mode", mode)
	fmt.Fprintln(output, string(content))
	return 0
}

func main() { os.Exit(run(os.Args[1:], os.Stdout, os.Stderr)) }
```

The log records counts and mode but not raw contents, tokens, or the environment variable source. A streaming implementation is preferable when files can exceed the program's memory policy.
