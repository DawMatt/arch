# VS Code Extensions

## Installing via command-line

From https://stackoverflow.com/questions/58513266/how-to-install-multiple-extensions-in-vscode-using-command-line

Create extension file
```
code --list-extensions > extensions.txt
```

Install via script on Mac
```bash
cat extensions.txt | while read extension || [[ -n $extension ]];
do
  code --install-extension $extension --force
done
```

or windows
```powershell
Get-Content extensions.txt | ForEach-Object {code --install-extension $_}
```

Other ideas:
- https://stackoverflow.com/questions/34286515/how-to-install-visual-studio-code-extensions-from-command-line
