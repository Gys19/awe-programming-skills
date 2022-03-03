# awe-programming-skills
to collect some awe programming skills


## parallel computing and show the progress bar at the same time 
Cite from [link](https://github.com/tqdm/tqdm/issues/484)

There are two points we need to pay attention when we apply below code.
* if you have a function wrote in a class object, please aovid any function callback in __init__ function 
* please add a output for pool if possible. 
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
for i in range(pbar.total):
    pool.apply_async(myfunc, args=(i,), callback=update)
pool.close()
pool.join()
```

## Git Bash commands
* initialization, the second line is used to link to your remote repo
```
git init
git remote add origin https://...
```

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

## Some geospatial operations 
* Geopandas, shapely, osmnx. networkx.
* generates points along line 
```javascript
distance_delta = 0.9
distances = np.arange(0, line.length, distance_delta)
# or alternatively without NumPy:
# points_count = int(line.length // distance_delta) + 1
# distances = (distance_delta * i for i in range(points_count))
points = [line.interpolate(distance) for distance in distances] + [line.boundary[1]]
multipoint = unary_union(points)  # or new_line = LineString(points)
```
