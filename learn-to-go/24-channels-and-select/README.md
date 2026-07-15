# Module 24: Channels and Select

## What you will learn

You will transfer values between goroutines, assign channel-closing ownership, and wait on several events.

```go
package main

import "fmt"

func produce(output chan<- int) {
	defer close(output)
	for number := 1; number <= 3; number++ {
		output <- number
	}
}

func main() {
	values := make(chan int)
	go produce(values)
	for value := range values {
		fmt.Println(value)
	}
}
```

An unbuffered send and receive meet before either completes. A buffered channel can hold a bounded number of values, but buffering is not a cure for missing lifecycle design.

The sending owner closes when no more values will ever be sent. Closing is a broadcast about future sends, not cleanup. Receivers do not close merely because they are finished. Receiving after close yields remaining values, then the zero value with `ok == false`.

`select` waits for one ready communication. If several are ready, one is chosen. A `default` makes it nonblocking and can create a busy loop. Timeouts and cancellation need clear resource cleanup.

Do not use `time.After` repeatedly in a long loop when a reusable timer with explicit stop and reset better matches ownership.

## Check your understanding

You are ready when you can name the sender, receiver, closer, buffer bound, and shutdown event for a channel.
