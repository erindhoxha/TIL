## Day 21

If we want to reset staging or any branch, here's the snippet we need:

```
git switch main # Switch to main branch
git branch -D staging # delete local staging branch
git switch -c staging # Create new staging branch based on main
git merge API-XXX # Merge your feature branch
git push --force # Force push
```

This way, we can reset staging with main if staging has differences along the way, or if there's been any force pushes.

Learned more about @extend in scss.

https://sass-lang.com/documentation/at-rules/extend/
