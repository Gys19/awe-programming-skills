# awe-programming-skills
to collect some awe programming skills


## parallel computing and show the progress bar at the same time 
Cite from [link](https://github.com/tqdm/tqdm/issues/484)

```javascript
import time
import random
from multiprocessing import Pool
from tqdm import tqdm

def myfunc(a):
    time.sleep(random.random())
    return a ** 2
pool = Pool(2)

for _ in tqdm(pool.imap_unordered(myfunc, range(100)), total=100):
    pass
pbar = tqdm(total=100)
def update(*a):
    pbar.update()
    # tqdm.write(str(a))
for i in range(pbar.total):
    pool.apply_async(myfunc, args=(i,), callback=update)
# tqdm.write('scheduled')
pool.close()
pool.join()
```

## Git Bash commands
* check and change the branch name
```
git branch
git branch -m <old name> <new name>
git branch -m <new name>
```
* pull the remote repo to local 
```
git pull origin main 
```
* push the local to remote repo
```
git push origin main
```
* commit changes
```
git commit -m "First commit Message"
```
* delete the old branch
```
git push origin --delete <oldname>
```
* push new branch to repo
```
git push origin -u <newname>
```
