
A collection of usefull copy &amp; paste powershell programs


# Filename postfix remover

replace `astringtoremove` with the actual string you want to remove

```powershell
$RemoveMinFromFileNameFunction = {
    param(
        [string]$FolderPath
    )

    if (-not (Test-Path -Path $FolderPath -PathType Container)) {
        Write-Host "Folder not found: $FolderPath"
        return
    }

    $files = Get-ChildItem -Path $FolderPath -File

    foreach ($file in $files) {
        $newName = $file.Name -replace 'astringtoremove(\.[^.]+)$', '$1'
        if ($newName -ne $file.Name) {
            $newPath = Join-Path -Path $FolderPath -ChildPath $newName
            Rename-Item -Path $file.FullName -NewName $newName
            Write-Host "Renamed $($file.Name) to $newName"
        }
    }
}

& $RemoveMinFromFileNameFunction -FolderPath "."


```
