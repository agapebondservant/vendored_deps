## Vendoring Python Dependencies

### Updating the _vendor folder
* Using **pip**, store Python dependencies into local **_vendor** folder 
(NOTE: You may need to manually remove failing dependencies from requirements.txt):
```
git clone </git/clone/url/of/python/app> parent
cd parent && rm -rf .git/ && cp ../requirements.txt . 
pip install --target="../_vendor" --ignore-installed -r requirements.txt
cd - && rm -rf parent
```

* To add the vendored dependencies to a git repository as a tar file:
```
tar -cvzf vendor.tar.gz _vendor
git lfs track "vendor.tar.gz"
```
Then add vendor.tar.gz to your repository.

### Adding vendored dependencies to the Python module search path
* If adding from a tar file, extract the tar file first:
```
tar -xvzf vendor.tar.gz _vendor
```

* Copy the _vendor path to your app's root directory:
```
cp -r _vendor/ /path/to/app/root/directory 
```
* Before loading your app, add the following Python code to a new module and import the module:
```
import sys
import os
if os.path.exists('_vendor'):
    sys.path.append('_vendor') 
```