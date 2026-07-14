# Exercise Solutions: Files, Paths, and Streams

```go
package main

import (
	"bufio"
	"errors"
	"fmt"
	"io"
	"os"
	"path/filepath"
)

func printLines(path string) (err error) {
	input, err := os.Open(path)
	if err != nil {
		return fmt.Errorf("open lines: %w", err)
	}
	defer func() {
		if closeErr := input.Close(); err == nil && closeErr != nil {
			err = fmt.Errorf("close lines: %w", closeErr)
		}
	}()

	scanner := bufio.NewScanner(input)
	for number := 1; scanner.Scan(); number++ {
		fmt.Println(number, scanner.Text())
	}
	if err := scanner.Err(); err != nil {
		return fmt.Errorf("scan lines: %w", err)
	}
	return nil
}

func copyFile(sourcePath, destinationPath string) (err error) {
	source, err := os.Open(sourcePath)
	if err != nil {
		return fmt.Errorf("open source: %w", err)
	}
	defer func() {
		if closeErr := source.Close(); err == nil && closeErr != nil {
			err = fmt.Errorf("close source: %w", closeErr)
		}
	}()

	destination, err := os.OpenFile(destinationPath, os.O_CREATE|os.O_WRONLY|os.O_TRUNC, 0o600)
	if err != nil {
		return fmt.Errorf("open destination: %w", err)
	}
	defer func() {
		if closeErr := destination.Close(); err == nil && closeErr != nil {
			err = fmt.Errorf("close destination: %w", closeErr)
		}
	}()

	if _, err := io.Copy(destination, source); err != nil {
		return fmt.Errorf("copy file: %w", err)
	}
	return nil
}

func replaceFile(directory, path string) (err error) {
	temporary, err := os.CreateTemp(directory, "replacement-")
	if err != nil {
		return fmt.Errorf("create replacement: %w", err)
	}
	temporaryPath := temporary.Name()
	closed := false
	defer func() {
		if !closed {
			if closeErr := temporary.Close(); err == nil && closeErr != nil {
				err = fmt.Errorf("close replacement: %w", closeErr)
			}
		}
		if removeErr := os.Remove(temporaryPath); err == nil && removeErr != nil && !errors.Is(removeErr, os.ErrNotExist) {
			err = fmt.Errorf("clean replacement: %w", removeErr)
		}
	}()

	if _, err := temporary.WriteString("replacement\n"); err != nil {
		return fmt.Errorf("write replacement: %w", err)
	}
	if err := temporary.Close(); err != nil {
		return fmt.Errorf("close replacement: %w", err)
	}
	closed = true
	if err := os.Remove(path); err != nil {
		return fmt.Errorf("remove old file: %w", err)
	}
	if err := os.Rename(temporaryPath, path); err != nil {
		return fmt.Errorf("rename replacement: %w", err)
	}
	return nil
}

func run() (err error) {
	directory, err := os.MkdirTemp("", "go-files-")
	if err != nil {
		return fmt.Errorf("create practice directory: %w", err)
	}
	defer func() {
		if removeErr := os.RemoveAll(directory); err == nil && removeErr != nil {
			err = fmt.Errorf("remove practice directory: %w", removeErr)
		}
	}()

	path := filepath.Join(directory, "notes.txt")
	if err := os.WriteFile(path, []byte("one\ntwo\nthree\n"), 0o600); err != nil {
		return fmt.Errorf("write notes: %w", err)
	}
	if err := printLines(path); err != nil {
		return err
	}
	if err := copyFile(path, filepath.Join(directory, "copy.txt")); err != nil {
		return err
	}

	missingPath := filepath.Join(directory, "missing.txt")
	missingFile, missingErr := os.Open(missingPath)
	if missingErr == nil {
		if err := missingFile.Close(); err != nil {
			return fmt.Errorf("close unexpected file: %w", err)
		}
		return fmt.Errorf("expected %s to be missing", missingPath)
	}
	fmt.Println("missing:", errors.Is(missingErr, os.ErrNotExist))

	if err := replaceFile(directory, path); err != nil {
		return err
	}
	return nil
}

func main() {
	if err := run(); err != nil {
		fmt.Fprintln(os.Stderr, "file exercise failed:", err)
		os.Exit(1)
	}
}
```

The temporary directory makes the exercise repeatable. Removing the old path before rename is portable but creates a gap and is not an atomic replacement. A production policy must use a tested platform strategy and define permissions, synchronization, link handling, durability, and recovery.
