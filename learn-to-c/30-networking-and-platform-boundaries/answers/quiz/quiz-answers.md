# Quiz Answers: Networking and Platform Boundaries

1. **Are sockets part of ISO C?**

   No. Operating systems and platform libraries provide them.

2. **Why wrap socket operations?**

   To localize type, setup, cleanup, error, and build differences.

3. **Does one receive equal one complete message?**

   No. A stream may split or combine application messages.

4. **Are received bytes automatically a C string?**

   No. A terminator must be verified or added within known capacity.

5. **What must a protocol define?**

   Framing, lengths, limits, byte order, errors, timeouts, and required security.

