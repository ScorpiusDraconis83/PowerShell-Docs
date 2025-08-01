---
external help file: System.Management.Automation.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Core
ms.date: 09/15/2023
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.core/invoke-history?view=powershell-7.4&WT.mc_id=ps-gethelp
schema: 2.0.0
aliases:
  - ihy
  - r
title: Invoke-History
---
# Invoke-History

## SYNOPSIS
Runs commands from the session history.

## SYNTAX

```
Invoke-History [[-Id] <String>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

The `Invoke-History` cmdlet runs commands from the session history. You can pass objects
representing the commands from Get-History to `Invoke-History`, or you can identify commands in the
current history by using their **Id** number. To find the identification number of a command, use
the `Get-History` cmdlet.

The session history is managed separately from the history maintained by the **PSReadLine** module.
Both histories are available in sessions where **PSReadLine** is loaded. This cmdlet only works with
the session history. For more information see, [about_PSReadLine](../PSReadLine/About/about_PSReadLine.md).

## EXAMPLES

### Example 1: Run the most recent command in the history

This example runs the last, or most recent, command in the session history. You can abbreviate this
command as `r`, the alias for `Invoke-History`.

```powershell
Invoke-History
```

### Example 2: Run the command that has a specified ID

This example runs the command in the session history with **Id** 132. Because the name of the **Id**
parameter is optional, you can abbreviate this command as the following: `Invoke-History 132`,
`ihy 132`, or `r 132`.

```powershell
Invoke-History -Id 132
```

### Example 3: Run the most recent command by using the command text

This example runs the most recent `Get-Process` command in the session history. When you type
characters for the **Id** parameter, `Invoke-History` runs the first command that it finds that
matches the pattern, starting with the most recent commands.

```powershell
Invoke-History -Id get-pr
```

> [!NOTE]
> Pattern matching is case-insensitive, but the pattern matches the beginning of the line.

### Example 4: Run a sequence of commands from the history

This example runs commands 16 through 24. Because you can list only one **Id** value, the command
uses the `ForEach-Object` cmdlet to run the `Invoke-History` command one time for each **Id** value.

```powershell
16..24 | ForEach-Object {Invoke-History -Id $_ }
```

### Example 5

This example runs the seven commands in the history that end with command 255 (249 through 255). It
uses the `Get-History` cmdlet to retrieve the commands. Because you can list only one **Id** value,
the command uses the `ForEach-Object` cmdlet to run the `Invoke-History` command once for each
**Id** value.

```powershell
Get-History -Id 255 -Count 7 | ForEach-Object {Invoke-History -Id $_.Id}
```

## PARAMETERS

### -Id

Specifies the **Id** of a command in the history. You can type the **Id** number of the command or
the first few characters of the command.

If you type characters, `Invoke-History` matches the most recent commands first. If you omit this
parameter, `Invoke-History` runs the last, or most recent, command. To find the **Id** number of a
command, use the `Get-History` cmdlet.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
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

Shows what would happen if the cmdlet runs. The cmdlet is not run.

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
[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### System.String

You can pipe a history **Id** to this cmdlet.

## OUTPUTS

### None

This cmdlet returns no output of its own, but the commands it runs may return their own output.

## NOTES

PowerShell includes the following aliases for `Invoke-History`:

- All platforms:
  - `ihy`
  - `r`

The session history is a list of the commands entered during the session. The session history
represents the order of execution, the status, and the start and end times of the command. As you
enter each command, PowerShell adds it to the history so that you can reuse it. For more information
about the session history, see [about_History](About/about_History.md).

## RELATED LINKS

[Add-History](Add-History.md)

[Clear-History](Clear-History.md)

[Get-History](Get-History.md)
