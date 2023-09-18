## Vendoring Python Dependencies

### Updating the _vendor folder
* Install OS dependencies prior to starting:
```
brew install snappy; export CPPFLAGS="-I/usr/local/include -L/usr/local/lib" # on Mac
sudo yum install csnappy-devel -y # on RPM-based
sudo apt-get install libsnappy-dev # on DEB-based
```

* Using **pip**, store Python dependencies into local **_vendor** folder 
(NOTE: You may need to manually remove failing dependencies from requirements.txt):
```
export TARGET_ARCH=manylinux_2_17_x86_64 # or desired target architecture
export TARGET_PY_VERSION=3.9
git clone </git/clone/url/of/python/app> parent
cd parent && rm -rf .git/ && cp ../requirements.txt . 
pip install --target="../_vendor" --ignore-installed --platform=$TARGET_ARCH --no-deps --python-version="$TARGET_PY_VERSION" -r requirements.txt
cd - && rm -rf parent
```

* To add the vendored dependencies to a git repository as a tar file:
```
tar -cvzf vendor.tar.gz _vendor
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