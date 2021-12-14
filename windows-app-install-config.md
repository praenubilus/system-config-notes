# Apps Installation List for Windows Dev Environment

## App management Software

Chocolatey tool

## Config X Server to display GUI from SSH session

- Install X Server App(Xming)

  ```ps1
  choco install xming
  ```

- Set Display Environment Variable
  
  ```ps1
  $env:DISPLAY = 'localhost:0.0'
  ```

- Connect with Authorized X11 Forwarding

  ```ps1
  ssh -v -Y <username>@<ipaddress> -p <port>
  ```

## Windows cannot Run Script in Powershell

```ps1
# check execution policy
 Get-ExecutionPolicy --List
# change policy for current user
 Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
# change policy for local machine(most users and scripts)
 Set-ExecutionPolicy RemoteSigned -Scope LocalMachine
```

## Set startup application in Windows

`Win+R`-> `shell:startup`-> right click then create a shortcut

## Install WSL

```ps1
wsl --install 
```

## Misc System and Productivity Apps

- AutoHotKey
  
  ```ps1
  choco install autohotkey
  ```

- Github Desktop
  
  ```ps1
  choco install github-desktop
  ```
  
- copyq
  
  ```ps1
  choco install copyq
  ```

- oh-my-posh (2.0)
  
  ```ps1
  choco install oh-my-posh
  # after installation, we need to modify the profile file
  code $PROFILE
  # append 
  # Invoke-Expression (oh-my-posh --init --shell pwsh --config $env:LocalAppData/Programs/oh-my-posh/themes/pure.omp.json) 
  # to the end of the file
  ```

- poshgit
  
  ```ps1
  choco install poshgit
  ```

- vscode

  ```ps1
  choco install vscode
  ```

- Teams
  
  ```ps1
  choco install microsoft-teams
  ```
