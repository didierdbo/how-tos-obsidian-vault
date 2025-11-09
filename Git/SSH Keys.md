1. Generate a SSH key (e.g via WSL on Windows):
```bash
ssh-keygen -t ed25519 -C "your_email"
```
2. Add key to ssh-agent:
```bash
eval "$(ssh-agent -s)" ssh-add ~/.ssh/id_ed25519
```
3. Copy the public key:
```bash
cat ~/.ssh/id_ed25519.pub
```
4. On GitHub, go to "SSH and GPG keys" settings and create a new SSH key with this public key

5. Check:
```bash
ssh -T git@github.com
git push
```
6. Then, for each new repo:
```bash
git clone git@github.com:USERNAME/new-repo.git
```
7. Or change existing repos:
```bash
git remote set-url origin git@github.com:USERNAME/repo.git
```


