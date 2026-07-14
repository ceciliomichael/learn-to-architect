# Exercise: Collect worker messages

1. Create an `mpsc` channel.
2. Start three threads. Each receives its own cloned sender and sends its worker number.
3. Drop the original sender after spawning the workers.
4. Collect messages until the channel closes, then sort and print them.
5. Join every worker and report any panic.
