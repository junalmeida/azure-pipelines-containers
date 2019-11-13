FROM mcr.microsoft.com/dotnet/framework/sdk:4.8
LABEL maintainer="Marcos Junior <junalmeida@gmail.com>"

RUN powershell " `
    $VSPath = "${env:ProgramFiles(x86)}\Microsoft Visual Studio\2019\BuildTools"; `
    $VC141 = "$VSPath\MSBuild\Microsoft\VC\v150\Platforms\x64\PlatformToolsets\v141\Toolset.props"; `
    if ((Test-Path "$VC141") -eq $False) { `
        $VSBootstrapperURL = "https://aka.ms/vs/16/release/vs_BuildTools.exe"; `
        $FilePath = "${env:Temp}\vs_BuildTools.exe"; `
        Invoke-WebRequest -Uri $VSBootstrapperURL -OutFile "$FilePath"; `
        echo "Installing VC v141 Toolset..."; `
        Start-Process -FilePath $FilePath -ArgumentList "modify", "--installPath", "`"$VSPath`"", "--add", "Microsoft.VisualStudio.Component.VC.v141.x86.x64", "--quiet", "--norestart", "--wait" -Wait -PassThru; `
    } `
    else `
    { `
        echo "VC v141 ToolSet already exists."; `
    } `
    `
    # Cleanup `
    Remove-Item -Force -Recurse "${env:ProgramFiles(x86)}\Microsoft Visual Studio\Installer" `
    Remove-Item -Force -Recurse "${env:Temp}\*" `
    Remove-Item -Force -Recurse "${env:ProgramData}\Package Cache" `
    `
    #Chocolatey
    Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')); `
    `
    choco install nodejs --version=9.11.2 -y --force; `
    `
    npm install -g yarn; `
    `

