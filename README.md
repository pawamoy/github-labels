# GitHub labels

Use the following command to clone labels from this repository into another:

```bash
gh label clone -f pawamoy/github-labels -R pawamoy/duty
```

Shell commands to apply labels to all repositories within a GitHub user account:

```bash
for repo in $(gh repo list pawamoy --json name --jq '.[].name' --limit 100 --source --no-archived --visibility public | \
    grep -ve github-labels -e website -e stars -e pawamoy -e awesome); do
  gh label clone -f pawamoy/github-labels -R pawamoy/$repo
done
```
