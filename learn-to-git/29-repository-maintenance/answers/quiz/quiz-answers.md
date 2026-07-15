# Quiz Answers: Maintain Large and Long-Lived Repositories

1. Loose and packed object counts, sizes, and related storage information.
2. Missing, invalid, or disconnected repository objects and references.
3. It can destroy recent recovery opportunities and may be unsafe with concurrent Git activity.
4. No. Older reachable commits still name it.
5. The credential must be revoked or rotated, and any history rewrite affects commit hashes and every clone, so it requires coordinated incident handling.
