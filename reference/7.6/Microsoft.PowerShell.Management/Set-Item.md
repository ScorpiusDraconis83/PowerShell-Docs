---
external help file: Microsoft.PowerShell.Commands.Management.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Management
ms.date: 02/16/2023
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.management/set-item?view=powershell-7.6&WT.mc_id=ps-gethelp
schema: 2.0.0
aliases:
  - si
title: Set-Item
---

# Set-Item

## SYNOPSIS
Changes the value of an item to the value specified in the command.

## SYNTAX

### Path (Default) - All providers

```
Set-Item [-Path] <String[]> [[-Value] <Object>] [-Force] [-PassThru] [-Filter <String>] [-Include <String[]>]
 [-Exclude <String[]>] [-Credential <PSCredential>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### LiteralPath - All providers

```
Set-Item -LiteralPath <String[]> [[-Value] <Object>] [-Force] [-PassThru] [-Filter <String>]
 [-Include <String[]>] [-Exclude <String[]>] [-Credential <PSCredential>]
 [-WhatIf] [-Confirm] [<CommonParameters>]
```

### Path (Default) - Alias and Function providers

```
Set-Item [-Path] <string[]> [[-Value] <Object>] [-Force] [-PassThru] [-Filter <string>]
 [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>] [-WhatIf] [-Confirm]
 [-Options <ScopedItemOptions>] [<CommonParameters>]
```

### LiteralPath - Alias and Function providers

```
Set-Item [[-Value] <Object>] -LiteralPath <string[]> [-Force] [-PassThru] [-Filter <string>]
 [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>] [-WhatIf] [-Confirm]
 [-Options <ScopedItemOptions>] [<CommonParameters>]
```

### Path (Default) - Registry provider

```
Set-Item [-Path] <string[]> [[-Value] <Object>] [-Force] [-PassThru] [-Filter <string>]
 [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>] [-WhatIf] [-Confirm]
 [-Type <RegistryValueKind>] [<CommonParameters>]
```

### LiteralPath - Registry provider

```
Set-Item [[-Value] <Object>] -LiteralPath <string[]> [-Force] [-PassThru] [-Filter <string>]
 [-Include <string[]>] [-Exclude <string[]>] [-Credential <pscredential>] [-WhatIf] [-Confirm]
 [-Type <RegistryValueKind>] [<CommonParameters>]
```

## DESCRIPTION

The `Set-Item` cmdlet changes the value of an item, such as a variable or registry key, to the value
specified in the command.

## EXAMPLES

### Example 1: Create an alias

This command creates an alias of np for Notepad.

```powershell
Set-Item -Path Alias:np -Value "C:\windows\notepad.exe"
```

### Example 2: Change the value of an environment variable

This command changes the value of the UserRole environment variable to Administrator.

```powershell
Set-Item -Path Env:UserRole -Value "Administrator"
```

### Example 3: Modify your prompt function

This command changes the prompt function so that it displays the time before the path.

```powershell
Set-Item -Path Function:prompt -Value {'PS '+ (Get-Date -Format t) + " " + (Get-Location) + '> '}
```

### Example 4: Set options for your prompt function

This command sets the **AllScope** and **ReadOnly** options for the prompt function.
This command uses the **Options** dynamic parameter of `Set-Item`.
The **Options** parameter is available in `Set-Item` only when you use it with the **Alias** or
**Function** provider.

```powershell
Set-Item -Path Function:prompt -Options "AllScope,ReadOnly"
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

Specifies a filter to qualify the **Path** parameter. The [FileSystem](../Microsoft.PowerShell.Core/About/about_FileSystem_Provider.md)
provider is the only installed PowerShell provider that supports the use of filters. You can find
the syntax for the **FileSystem** filter language in [about_Wildcards](../Microsoft.PowerShell.Core/About/about_Wildcards.md).
Filters are more efficient than other parameters, because the provider applies them when the cmdlet
gets the objects rather than having PowerShell filter the objects after they are retrieved.

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

Forces the cmdlet to set items that cannot otherwise be changed, such as read-only alias or
variables. The cmdlet cannot change constant aliases or variables.
Implementation varies from provider to provider.
For more information, see [about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md).
Even using the *Force* parameter, the cmdlet cannot override security restrictions.

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

### -LiteralPath

Specifies a path to one or more locations. The value of **LiteralPath** is used exactly as it is
typed. No characters are interpreted as wildcards. If the path includes escape characters, enclose
it in single quotation marks. Single quotation marks tell PowerShell not to interpret any characters
as escape sequences.

For more information, see [about_Quoting_Rules](../Microsoft.Powershell.Core/About/about_Quoting_Rules.md).

```yaml
Type: System.String[]
Parameter Sets: LiteralPath
Aliases: PSPath, LP

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Options

This is a dynamic parameter made available by the **Alias** and **Function** providers. For more
information, see [about_Alias_Provider](../Microsoft.PowerShell.Core/About/about_Alias_Provider.md)
and [about_Function_Provider](../Microsoft.PowerShell.Core/About/about_Function_Provider.md).

Specifies the value of the **Options** property of an alias.

Valid values are:

- `None`: The alias has no constraints (default value)
- `ReadOnly`: The alias can be deleted but can't be changed without using the **Force** parameter
- `Constant`: The alias can't be deleted or changed
- `Private`: The alias is available only in the current scope
- `AllScope`: The alias is copied to any new scopes that are created
- `Unspecified`: The option isn't specified

```yaml
Type: System.Management.Automation.ScopedItemOptions
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PassThru

Passes an object that represents the item to the pipeline.
By default, this cmdlet does not generate any output.

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

### -Path

Specifies a path of the location of the items.
Wildcard characters are permitted.

```yaml
Type: System.String[]
Parameter Sets: Path
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

### -Value

Specifies a new value for the item.

```yaml
Type: System.Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: True (ByPropertyName, ByValue)
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

### System.Object

You can pipe an object that represents the new value of the item to this cmdlet.

## OUTPUTS

### None

By default, this cmdlet returns no output.

### System.Object

When you use the **PassThru** parameter, this cmdlet returns an object representing the item.

## NOTES

PowerShell includes the following aliases for `Set-Item`:

- All platforms:
  - `si`

- `Set-Item` is not supported by the PowerShell FileSystem provider. To change the values of items in
  the file system, use the `Set-Content` cmdlet.
- In the Registry drives, `HKLM:` and `HKCU:`, `Set-Item` changes the data in the (Default) value of a
  registry key.
  - To create and change the names of registry keys, use the `New-Item` and `Rename-Item` cmdlet.
  - To change the names and data in registry values, use the `New-ItemProperty`, `Set-ItemProperty`, and
    `Rename-ItemProperty` cmdlets.
- `Set-Item` is designed to work with the data exposed by any provider.
  To list the providers available in your session, type `Get-PSProvider`.
  For more information, see [about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md).

## RELATED LINKS

[Clear-Item](Clear-Item.md)

[Copy-Item](Copy-Item.md)

[Get-Item](Get-Item.md)

[Invoke-Item](Invoke-Item.md)

[Move-Item](Move-Item.md)

[New-Item](New-Item.md)

[Remove-Item](Remove-Item.md)

[Rename-Item](Rename-Item.md)

[about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md)
