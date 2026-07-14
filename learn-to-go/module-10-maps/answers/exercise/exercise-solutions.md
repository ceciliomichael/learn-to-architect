# Exercise Solutions: Maps

```go
package main

import (
	"fmt"
	"sort"
	"strings"
)

func main() {
	prices := map[string]int{"pen": 125, "gift": 0}
	prices["book"] = 1200
	prices["pen"] = 150
	delete(prices, "book")

	price, found := prices["gift"]
	fmt.Println(price, found)
	_, found = prices["missing"]
	fmt.Println(found)

	counts := make(map[string]int)
	for _, word := range strings.Fields("go is clear and go is small") {
		counts[word]++
	}

	copyOfCounts := make(map[string]int, len(counts))
	for key, value := range counts {
		copyOfCounts[key] = value
	}
	copyOfCounts["go"] = 99

	keys := make([]string, 0, len(counts))
	for key := range counts {
		keys = append(keys, key)
	}
	sort.Strings(keys)
	for _, key := range keys {
		fmt.Println(key, counts[key])
	}
}
```

The `gift` key is present even though its value is zero. Sorting keys makes output deterministic without pretending the map itself is ordered.
