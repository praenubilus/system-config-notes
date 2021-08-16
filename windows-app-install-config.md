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
