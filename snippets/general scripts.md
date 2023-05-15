run a script on all changed files 
```bash
git status -s | grep '.M ' | cut -c 4- | xargs echo
```
replace echo with script e.g. 
```bash
git status -s | grep '.M ' | cut -c 4- | xargs npx organize-imports-cli
```