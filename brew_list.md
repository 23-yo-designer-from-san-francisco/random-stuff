List all homebrew packages and sort them by size

[Original post](https://gist.github.com/eguven/23d8c9fc78856bd20f65f8bcf03e691b)

```bash
brew list --formula | xargs -n1 -P8 -I {} \
    sh -c "brew info {} | egrep '[0-9]* files, ' | sed 's/^.*[0-9]* files, \(.*\)).*$/{} \1/'" | \
    sort -h -r -k2 - | column -t
```
