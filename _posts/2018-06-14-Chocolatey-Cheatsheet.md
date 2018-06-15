**Links:**

*   [https://chocolatey.org/](https://chocolatey.org/)  
     
*   [Chocolatey Packages](https://chocolatey.org/packages)  
      
     

- - -

**Install command on Windows (10) using CMD (Run as Administrator):**

@"%SystemRoot%\\System32\\WindowsPowerShell\\v1.0\\powershell.exe" -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\\chocolatey\\bin"

- - -

**Package Installs:**

Application

Command

Notes

7-Zip

choco install 7zip.install -y

Strange syntax...

Filezilla

choco install filezilla -y

Removed old version!

Node.js

choco install nodejs -y

Gets the latest version of Node.js

VLC

choco install vlc -y

Did not remove old version!
