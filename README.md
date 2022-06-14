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

## parallel computing for for loops
```javascript
import multiprocessing

pool = multiprocessing.Pool(10)
# if you have multi-parameters 
# wrap your function like this

def multi_run_wrapper(args):
    return yourparallelfunction(*args)
def yourparallelfunction(para1, para2, ...)
    return example
para_list = [(para1, para2, ...) for range(i)]
# save results
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
* add new files to remote repo
```
git add file.jpg file2.jpg file3.pdf
git commit -m 'comment'
git push -f origin main
```


## Some geospatial operations 
* Geopandas, shapely, osmnx. networkx.
* generates points along line 
```javascript
distance_delta = 0.9
distances = np.arange(0, line.length, distance_delta)
points = [line.interpolate(distance) for distance in distances] + [line.boundary[1]]
multipoint = unary_union(points)  # or new_line = LineString(points)
```

# get timezone from lat long.
```javascript
from timezonefinder import TimezoneFinder

tf = TimezoneFinder()
sub_dc['TZname'] = sub_dc[['Lat', 'Long']].apply(lambda x: tf.timezone_at(lng=x[1], lat=x[0]), axis=1)
# convert time zone and localize the date.
sub_dc['localtime'] = sub_dc[['pubDate', 'TZname']].apply(lambda x: pd.to_datetime(x[0], format='%a %b %d %H:%M:%S %z %Y').tz_convert(x[1]).tz_localize(None), axis=1)
```

# matlab make gif from a set of figures. 
```Matlab
% made by Yangsogng on Tue, 6//2022
% make fig from a set of images
img_folder = 'C:\Work\isochrone Travel Time\figures\80pct\';
filename = 'isochrone TT.gif'
for i = 1:24
    
    f = [img_folder,sprintf('0_0.8_%d.c.png', i-1)];
    img = imread(f);
    [I, map] = rgb2ind(img, 256);
    if (i==1)
        imwrite(I, map, filename, 'DelayTime', 0.1, 'LoopCount', Inf)
    else
        imwrite(I, map, filename, 'WriteMode', 'append', 'DelayTime', 0.1)
    end
end
```

# python subprocess package, run py script as python script
* good for monitoring the code
* introduction: https://code.luasoftware.com/tutorials/python/simple-guide-to-subprocess/
## sample code
```javascript
p = subprocess.Popen(['python', 'test.py'])
```
the code can be wrapped in a while loop, so that the while loop can continue execute the script if it stopped. 


# JS code if you want to load local csv file or json file when writing HTML 
* run a virtual web server, go to folder where html file is saved, and open cmd, type
```javascript
python -m http.server
```
* turn on the google browser, and type: `localhost:8000/index.html` on search window.
* then, you can use d3.js or fetch method to load local file now. 


