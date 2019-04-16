# WinCredManager

Provides cmdlets for reading, writing and removing Generic and DomainPassword credentials from the Windows Credential Manager.

## Usage

List all credentials:
```powershell
Get-WCMCredential
```

Get a specific named credential:
```powershell
Get-WCMCredential -Name Test1 -Type Generic
```

Add a DomainPassword credential. DomainPassword credentials are automatically used by Windows when accessing a server resource
with the specified name. Many Windows resources are supported, such as RPC, SMB and SQL servers (if the port is provided).
DomainPassword credentials cannot be decrypted (by normal means).
```powershell
Add-WCMCredential -Name server.domain.org -Type DomainPassword
```

Add a Generic credential. Generic credentials can be decrypted.
```powershell
Add-WCMCredential -Name MySqlServer1 -Type Generic -Username User01 -Password SecretPassword
Add-WCMCredential -Name MySqlServer2 -Type Generic -Credential (Get-Credential -Message "Enter MySQL Creds")
```

Remove a credential:
```powershell
Remove-WCMCredential -Name MySqlServer1 -Type Generic
```

Show a list of credentials in Out-GridView, the selected credentials will be removed:
```powershell
Get-WCMCredential | Out-GridView -PassThru -Title "Select credentials to remove" | Remove-WCMCredential
```