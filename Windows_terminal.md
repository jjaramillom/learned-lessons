# Windows terminal

# Findings

## Have a better appearance in PowerShell


1.  Install oh my posh from https://github.com/JanDeDobbeleer/oh-my-posh

    ```bash
    Install-Module oh-my-posh -Scope CurrentUser -AllowPrerelease
    Install-Module posh-git -Scope CurrentUser
    ```

    If there is the **"A parameter cannot be found that matches parameter name AllowPrerelease."** error, run these commands and restart:

    ```bash
    Install-Module -Name PackageManagement -Repository PSGallery -Force
    Install-Module -Name PowerShellGet -Repository PSGallery -Force
    ```

2.  Enable the engine within PowerShell profile.

    ```bash
    if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
    notepad $PROFILE
    ```

    Then add the following in the opened file and save it.

    ```bash
    Import-Module posh-git
    Import-Module oh-my-posh
    Set-Theme Paradox
    ```

3.  Install a font from https://github.com/ryanoasis/nerd-fonts/releases/tag/v2.1.0
    One that has worked quite well is **_CodeNewRoman (CodeNewRoman NF)_**.
    Add this to the VS Code setting `"terminal.integrated.fontFamily"` and to the PowerShell profile in Windows Terminal settings as `"fontFace"`.
4.  Install Terminal-icons from https://github.com/devblackops/Terminal-Icons

    ```bash
    Install-Module -Name Terminal-Icons -Repository PSGallery
    ```

    Add them to the `"$Profile"` file as:

    ```
    Import-Module -Name Terminal-Icons
    ```

## Aliases

1. cd =>
   `function cddi {set-location C:\Users\Jacobo\dev_main\DI\microservices}`

2. GIT =>
   ```bash
   function merge {git merge remotes/origin/develop}
   function ci ($comment) {git commit -m $comment}
   ```
3. general =>
   1. remove directory
      ```bash
      function rm_dir($dir) {
          Write-Host 'Are you sure to delete "' $dir '"?'
          $userConfirmation = Read-Host -Prompt '[y/n]'
          Write-Host $userConfirmation
          if ($userConfirmation -eq 'y' -or $userConfirmation -eq 'Y'){
              Remove-Item -Recurse -Force $dir
              Write-Host 'Directory deleted'
          }
      }
      ```
