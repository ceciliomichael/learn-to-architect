# Question 05 (Answer)

Thinking of Git as an automatic cloud backup system (like Google Drive or Dropbox) is a dangerous misconception that leads to massive data loss and corrupted repositories for beginners.

Systems like Google Drive operate implicitly and automatically. The moment you press `Ctrl + S` in a word processor, the file is instantly synced to a server in the background without any further interaction.

Git operates explicitly and locally. It does absolutely nothing in the background. If you do not explicitly tell Git to track a file, stage a file, and commit a file, Git will ignore it. Furthermore, Git commits only save data locally to the hidden `.git` directory on your specific hard drive. Until you deliberately push those commits to a remote server (which is covered in later modules), your code is not backed up to the cloud at all. Relying on Git to passively save your work like Google Drive means you will inevitably lose hours or days of progress when you realize no snapshots were ever actually recorded.
