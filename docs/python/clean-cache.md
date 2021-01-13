# Clean Python cache files

```bash
declare -a cache_dir=(".pytest_cache" "__pycache__")
# Iterate the string array using for loop
for val in ${cache_dir[@]}; do
   find . -name $val -exec rm -rvf {} +
done
```
