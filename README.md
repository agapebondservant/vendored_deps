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

### Adding vendored dependencies to the Python module search path