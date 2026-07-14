# Exercise Solutions: Methods, Embedding, and Composition

```go
package main

import "fmt"

type Audit struct{ CreatedBy string }

type Account struct {
	Audit
	Owner        string
	BalanceCents int
}

func (account *Account) Deposit(cents int) error {
	if cents <= 0 {
		return fmt.Errorf("deposit must be positive")
	}
	account.BalanceCents += cents
	return nil
}

func (account *Account) Withdraw(cents int) error {
	if cents <= 0 || cents > account.BalanceCents {
		return fmt.Errorf("invalid withdrawal")
	}
	account.BalanceCents -= cents
	return nil
}

func (account Account) DisplayBalance() string {
	return fmt.Sprintf("PHP %d.%02d", account.BalanceCents/100, account.BalanceCents%100)
}

func main() {
	first := Account{Audit: Audit{CreatedBy: "system"}, Owner: "Ava", BalanceCents: 1000}
	second := Account{Owner: "Ben", BalanceCents: 500}
	if err := first.Deposit(250); err != nil {
		fmt.Println("deposit failed:", err)
		return
	}
	if err := second.Withdraw(100); err != nil {
		fmt.Println("withdrawal failed:", err)
		return
	}
	fmt.Println(first.DisplayBalance(), second.DisplayBalance(), first.CreatedBy)
}
```

The methods validate before mutation and every returned error is observed. A named `Audit Audit` field would be clearer if callers should always say `account.Audit.CreatedBy`.
