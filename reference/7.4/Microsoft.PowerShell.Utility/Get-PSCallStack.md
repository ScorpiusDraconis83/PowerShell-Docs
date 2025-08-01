---
external help file: Microsoft.PowerShell.Commands.Utility.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Utility
ms.date: 06/28/2023
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.utility/get-pscallstack?view=powershell-7.4&WT.mc_id=ps-gethelp
schema: 2.0.0
aliases:
  - gcs
title: Get-PSCallStack
---

# Get-PSCallStack

## SYNOPSIS
Displays the current call stack.

## SYNTAX

```
Get-PSCallStack [<CommonParameters>]
```

## DESCRIPTION

The `Get-PSCallStack` cmdlet displays the current call stack.

Although it is designed to be used with the Windows PowerShell debugger, you can use this cmdlet to
display the call stack in a script or function outside of the debugger.

To run a `Get-PSCallStack` command while in the debugger, type `k` or `Get-PSCallStack`.

## EXAMPLES

### Example 1: Get the call stack for a function

```powershell
PS C:\> function My-Alias {
$p = $args[0]
Get-Alias | where {$_.Definition -like "*$p"} | Format-Table Definition, Name -Auto
}
PS C:\ps-test> Set-PSBreakpoint -Command My-Alias
Command    : My-Alias
Action     :
Enabled    : True
HitCount   : 0
Id         : 0
Script     : prompt PS C:\> My-Alias Get-Content

Entering debug mode. Use h or ? for help.
Hit Command breakpoint on 'prompt:My-Alias'
My-Alias Get-Content
[DBG]: PS C:\ps-test> s
$p = $args[0]
DEBUG: Stepped to ':    $p = $args[0]    '
[DBG]: PS C:\ps-test> s
Get-Alias | where {$_.Definition -like "*$p*"} | Format-Table Definition,
[DBG]: PS C:\ps-test>Get-PSCallStack

Name        CommandLineParameters         UnboundArguments              Location
----        ---------------------         ----------------              --------
prompt      {}                            {}                            prompt
My-Alias    {}                            {Get-Content}                 prompt
prompt      {}                            {}                            prompt

PS C:\> [DBG]: PS C:\ps-test> o
Definition  Name
----------  ----
Get-Content gc
Get-Content cat
Get-Content type
```

This command uses the `Get-PSCallStack` cmdlet to display the call stack for `My-Alias`, a simple
function that gets the aliases for a cmdlet name.

The first command enters the function at the Windows PowerShell prompt. The second command uses the
`Set-PSBreakpoint` cmdlet to set a breakpoint on the `My-Alias` function. The third command uses the
`My-Alias` function to get all of the aliases in the current session for the `Get-Content` cmdlet.

The debugger breaks in at the function call. Two consecutive `step-into` (`s`) commands begin
executing the function line by line. Then, a `Get-PSCallStack` command is used to retrieve the call
stack.

The final command is a `Step-Out` command (`o`) that exits the debugger and continues executing the
script to completion.

## PARAMETERS

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose,
-WarningAction, and -WarningVariable. For more information, see
[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

You can't pipe objects to this cmdlet.

## OUTPUTS

### System.Management.Automation.CallStackFrame

This cmdlet returns an object representing the items in the call stack.

## NOTES

PowerShell includes the following aliases for `Get-PSCallStack`:

- All platforms:
  - `gcs`

## RELATED LINKS

[Disable-PSBreakpoint](Disable-PSBreakpoint.md)

[Enable-PSBreakpoint](Enable-PSBreakpoint.md)

[Format-Table](Format-Table.md)

[Get-PSBreakpoint](Get-PSBreakpoint.md)

[Remove-PSBreakpoint](Remove-PSBreakpoint.md)

[Set-PSBreakpoint](Set-PSBreakpoint.md)
