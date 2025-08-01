---
external help file: Microsoft.PowerShell.Commands.Management.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Management
ms.date: 02/16/2023
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.management/set-itemproperty?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
aliases:
  - sp
title: Set-ItemProperty
---

# Set-ItemProperty

## SYNOPSIS
Creates or changes the value of a property of an item.

## SYNTAX

### propertyValuePathSet (Default) - All providers

```
Set-ItemProperty [-Path] <string[]> [-Name] <string> [-Value] <Object> [-PassThru] [-Force]
 [-Filter <string>] [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>]
 [-WhatIf] [-Confirm] [-UseTransaction] [<CommonParameters>]
```

### propertyPSObjectPathSet - All providers

```
Set-ItemProperty [-Path] <string[]> -InputObject <psobject> [-PassThru] [-Force]
 [-Filter <string>] [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>]
 [-WhatIf] [-Confirm] [-UseTransaction] [<CommonParameters>]
```

### propertyValueLiteralPathSet - All providers

```
Set-ItemProperty [-Name] <string> [-Value] <Object> -LiteralPath <string[]> [-PassThru] [-Force]
 [-Filter <string>] [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>]
 [-WhatIf] [-Confirm] [-UseTransaction] [<CommonParameters>]
```

### propertyPSObjectLiteralPathSet - All providers

```
Set-ItemProperty -LiteralPath <string[]> -InputObject <psobject> [-PassThru] [-Force]
 [-Filter <string>] [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>]
 [-WhatIf] [-Confirm] [-UseTransaction] [<CommonParameters>]
```

### propertyValuePathSet (Default) - Registry provider

```
Set-ItemProperty [-Path] <string[]> [-Name] <string> [-Value] <Object> [-PassThru] [-Force]
 [-Filter <string>] [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>]
 [-WhatIf] [-Confirm] [-UseTransaction] [-Type <RegistryValueKind>] [<CommonParameters>]
```

### propertyPSObjectPathSet - Registry provider

```
Set-ItemProperty [-Path] <string[]> -InputObject <psobject> [-PassThru] [-Force]
 [-Filter <string>] [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>]
 [-WhatIf] [-Confirm] [-UseTransaction] [-Type <RegistryValueKind>] [<CommonParameters>]
```

### propertyValueLiteralPathSet - Registry provider

```
Set-ItemProperty [-Name] <string> [-Value] <Object> -LiteralPath <string[]> [-PassThru] [-Force]
 [-Filter <string>] [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>]
 [-WhatIf] [-Confirm] [-UseTransaction] [-Type <RegistryValueKind>] [<CommonParameters>]
```

### propertyPSObjectLiteralPathSet - Registry provider

```
Set-ItemProperty -LiteralPath <string[]> -InputObject <psobject> [-PassThru] [-Force]
 [-Filter <string>] [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>]
 [-WhatIf] [-Confirm] [-UseTransaction] [-Type <RegistryValueKind>] [<CommonParameters>]
```

## DESCRIPTION

The `Set-ItemProperty` cmdlet changes the value of the property of the specified item.
You can use the cmdlet to establish or change the properties of items.
For example, you can use `Set-ItemProperty` to set the value of the **IsReadOnly** property of a
file object to `$true`.

You also use `Set-ItemProperty` to create and change registry values and data.
For example, you can add a new registry entry to a key and establish or change its value.

## EXAMPLES

### Example 1: Set a property of a file

This command sets the value of the **IsReadOnly** property of the "final.doc" file to "true".
It uses **Path** to specify the file, **Name** to specify the name of the property, and the
**Value** parameter to specify the new value.

The file is a **System.IO.FileInfo** object and **IsReadOnly** is just one of its properties.
To see all of the properties, type `Get-Item C:\GroupFiles\final.doc | Get-Member -MemberType
Property`.

The `$true` automatic variable represents a value of "TRUE". For more information, see
[about_Automatic_Variables](../Microsoft.PowerShell.Core/About/about_Automatic_Variables.md).

```powershell
Set-ItemProperty -Path C:\GroupFiles\final.doc -Name IsReadOnly -Value $true
```

### Example 2: Create a registry entry and value

This example shows how to use `Set-ItemProperty` to create a new registry entry and to assign a
value to the entry. It creates the "NoOfEmployees" entry in the "ContosoCompany" key in
`HKLM\Software` key and sets its value to 823.

Because registry entries are considered to be properties of the registry keys, which are items, you
use `Set-ItemProperty` to create registry entries, and to establish and change their values.

```powershell
Set-ItemProperty -Path "HKLM:\Software\ContosoCompany" -Name "NoOfEmployees" -Value 823
Get-ItemProperty -Path "HKLM:\Software\ContosoCompany"
```

```Output
PSPath        : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\software\contosocompany
PSParentPath  : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\software
PSChildName   : contosocompany
PSDrive       : HKLM
PSProvider    : Microsoft.PowerShell.Core\Registry
NoOfLocations : 2
NoOfEmployees : 823
```

```powershell
Set-ItemProperty -Path "HKLM:\Software\ContosoCompany" -Name "NoOfEmployees" -Value 824
Get-ItemProperty -Path "HKLM:\Software\ContosoCompany"
```

```Output
PSPath        : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\software\contosocompany
PSParentPath  : Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\software
PSChildName   : contosocompany
PSDrive       : HKLM
PSProvider    : Microsoft.PowerShell.Core\Registry
NoOfLocations : 2
NoOfEmployees : 824
```

The first command creates the registry entry.
It uses **Path** to specify the path of the `HKLM:` drive and the `Software\MyCompany` key.
The command uses **Name** to specify the entry name and **Value** to specify a value.

The second command uses the `Get-ItemProperty` cmdlet to see the new registry entry.
If you use the `Get-Item` or `Get-ChildItem` cmdlets, the entries do not appear because they are
properties of a key, not items or child items.

The third command changes the value of the **NoOfEmployees** entry to 824.

You can also use the `New-ItemProperty` cmdlet to create the registry entry and its value and then
use `Set-ItemProperty` to change the value.

For more information about the `HKLM:` drive, type `Get-Help Get-PSDrive`.
For more information about how to use PowerShell to manage the registry, type `Get-Help Registry`.

### Example 3: Modify an item by using the pipeline

Th example uses `Get-ChildItem` to get the `weekly.txt` file. The file object is piped to
`Set-ItemProperty`. The `Set-ItemProperty` command uses the **Name** and **Value** parameters to
specify the property and its new value.

```powershell
Get-ChildItem weekly.txt | Set-ItemProperty -Name IsReadOnly -Value $true
```

## PARAMETERS

### -Credential

> [!NOTE]
> This parameter is not supported by any providers installed with PowerShell.
> To impersonate another user, or elevate your credentials when running this cmdlet,
> use [Invoke-Command](../Microsoft.PowerShell.Core/Invoke-Command.md).

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: Current user
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Exclude

Specifies, as a string array, an item or items that this cmdlet excludes in the operation. The value
of this parameter qualifies the **Path** parameter. Enter a path element or pattern, such as
`*.txt`. Wildcard characters are permitted. The **Exclude** parameter is effective only when the
command includes the contents of an item, such as `C:\Windows\*`, where the wildcard character
specifies the contents of the `C:\Windows` directory.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -Filter

Specifies a filter to qualify the **Path** parameter. The
[FileSystem](../Microsoft.PowerShell.Core/About/about_FileSystem_Provider.md) provider is the only
installed PowerShell provider that supports the use of filters. You can find the syntax for the
**FileSystem** filter language in
[about_Wildcards](../Microsoft.PowerShell.Core/About/about_Wildcards.md). Filters are more efficient
than other parameters, because the provider applies them when the cmdlet gets the objects rather
than having PowerShell filter the objects after they are retrieved.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -Force

Forces the cmdlet to set a property on items that cannot otherwise be accessed by the user.
Implementation varies by provider. For more information, see
[about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md).

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Include

Specifies, as a string array, an item or items that this cmdlet includes in the operation. The value
of this parameter qualifies the **Path** parameter. Enter a path element or pattern, such as
`"*.txt"`. Wildcard characters are permitted. The **Include** parameter is effective only when the
command includes the contents of an item, such as `C:\Windows\*`, where the wildcard character
specifies the contents of the `C:\Windows` directory.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: True
```

### -InputObject

Specifies the object that has the properties that this cmdlet changes.
Enter a variable that contains the object or a command that gets the object.

```yaml
Type: System.Management.Automation.PSObject
Parameter Sets: propertyPSObjectPathSet, propertyPSObjectLiteralPathSet
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
Accept wildcard characters: False
```

### -LiteralPath

Specifies a path to one or more locations. The value of **LiteralPath** is used exactly as it is
typed. No characters are interpreted as wildcards. If the path includes escape characters, enclose
it in single quotation marks. Single quotation marks tell PowerShell not to interpret any characters
as escape sequences.

For more information, see
[about_Quoting_Rules](../Microsoft.Powershell.Core/About/about_Quoting_Rules.md).

```yaml
Type: System.String[]
Parameter Sets: propertyValueLiteralPathSet, propertyPSObjectLiteralPathSet
Aliases: PSPath

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Name

Specifies the name of the property.

```yaml
Type: System.String
Parameter Sets: propertyValuePathSet, propertyValueLiteralPathSet
Aliases: PSProperty

Required: True
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -PassThru

Returns an object that represents the item property.
By default, this cmdlet does not generate any output.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Path

Specifies the path of the items with the property to modify.
Wildcard characters are permitted.

```yaml
Type: System.String[]
Parameter Sets: propertyValuePathSet, propertyPSObjectPathSet
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: True
```

### -Type

This is a dynamic parameter made available by the **Registry** provider. The **Registry** provider
and this parameter are only available on Windows.

Specifies the type of property that this cmdlet adds. The acceptable values for this parameter are:

- `String`: Specifies a null-terminated string. Used for **REG_SZ** values.
- `ExpandString`: Specifies a null-terminated string that contains unexpanded references to
  environment variables that are expanded when the value is retrieved. Used for **REG_EXPAND_SZ**
  values.
- `Binary`: Specifies binary data in any form. Used for **REG_BINARY** values.
- `DWord`: Specifies a 32-bit binary number. Used for **REG_DWORD** values.
- `MultiString`: Specifies an array of null-terminated strings terminated by two null characters.
  Used for **REG_MULTI_SZ** values.
- `Qword`: Specifies a 64-bit binary number. Used for **REG_QWORD** values.
- `Unknown`: Indicates an unsupported registry data type, such as **REG_RESOURCE_LIST** values.

```yaml
Type: Microsoft.Win32.RegistryValueKind
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -UseTransaction

Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see [about_Transactions](../Microsoft.PowerShell.Core/About/about_Transactions.md).

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases: usetx

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -Value

Specifies the value of the property.

```yaml
Type: System.Object
Parameter Sets: propertyValuePathSet, propertyValueLiteralPathSet
Aliases:

Required: True
Position: 2
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Confirm

Prompts you for confirmation before running the cmdlet.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf

Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](../Microsoft.PowerShell.Core/About/about_CommonParameters.md).

## INPUTS

### System.Management.Automation.PSObject

You can pipe objects to this cmdlet.

## OUTPUTS

### None

By default, this cmdlet returns no output.

### System.Management.Automation.PSCustomObject

When you use the **PassThru** parameter, this cmdlet returns a **PSCustomObject** object
representing the item that was changed and its new property value.

## NOTES

Windows PowerShell includes the following aliases for `Set-ItemProperty`:

- `sp`

`Set-ItemProperty` is designed to work with the data exposed by any provider. To list the providers
available in your session, type `Get-PSProvider`. For more information, see
[about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md).

## RELATED LINKS

[Clear-ItemProperty](Clear-ItemProperty.md)

[Copy-ItemProperty](Copy-ItemProperty.md)

[Get-ItemProperty](Get-ItemProperty.md)

[Move-ItemProperty](Move-ItemProperty.md)

[New-ItemProperty](New-ItemProperty.md)

[Remove-ItemProperty](Remove-ItemProperty.md)

[Rename-ItemProperty](Rename-ItemProperty.md)

[about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md)
