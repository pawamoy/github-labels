# GitHub labels

Use the following command to clone labels from this repository into another:

```bash
gh label clone -f pawamoy/github-labels -R pawamoy/duty
```

Shell script to apply labels to some repositories within a GitHub user account:

```bash
unwanted_labels=(
  "documentation"
  "enhancement"
  "good first issue"
  "help wanted"
  "invalid"
  "question"
  "wontfix"
)
for repo in $(gh repo list pawamoy --json name --jq '.[].name' --limit 100 \
    --source --no-archived --visibility public --language python,jinja | \
    grep -ve github-labels -e website -e stars -e pawamoy -e awesome); do
  gh label clone -f pawamoy/github-labels -R pawamoy/$repo
  for label in "${unwanted_labels[@]}"; do
    gh label delete "$label" -R pawamoy/$repo --yes
  done 
done
```
