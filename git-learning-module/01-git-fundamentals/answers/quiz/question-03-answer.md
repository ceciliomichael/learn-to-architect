# Question 03 (Answer)

If you edit a file, skip `git add`, and directly execute `git commit`, Git will abort the operation and output a message similar to: `no changes added to commit`.

This occurs because `git commit` only looks at the **Staging Area** to determine what to save into the permanent history. If you have not executed `git add` on your modified file, that file only exists in the Working Directory (the "Workshop"). It has not been moved into the Staging Area (the "Viewfinder").

In the Photography Studio analogy, trying to commit without adding is like pressing the shutter button on your camera while the lens cap is on and the props are sitting out of frame. The camera can only capture what is currently loaded into the viewfinder. Therefore, Git requires you to explicitly stage the changes first before it permits a snapshot to be recorded.
