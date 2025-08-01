---
external help file: Microsoft.PowerShell.Commands.Management.dll-Help.xml
Locale: en-US
Module Name: Microsoft.PowerShell.Management
ms.date: 03/15/2023
online version: https://learn.microsoft.com/powershell/module/microsoft.powershell.management/set-content?view=powershell-7.6&WT.mc_id=ps-gethelp
schema: 2.0.0
aliases:
  - sc
title: Set-Content
---

# Set-Content

## SYNOPSIS
Writes new content or replaces existing content in a file.

## SYNTAX

### Path (Default) - FileSystem provider

```
Set-Content [-Path] <string[]> [-Value] <Object[]> [-PassThru] [-Filter <string>]
 [-Include <string[]>] [-Exclude <string[]>] [-Force] [-Credential <pscredential>]
 [-WhatIf] [-Confirm] [-NoNewline] [-Encoding <Encoding>] [-AsByteStream] [-Stream <string>]
 [<CommonParameters>]
```

### LiteralPath - FileSystem provider

```
Set-Content [-Value] <Object[]> -LiteralPath <string[]> [-PassThru] [-Filter <string>]
 [-Include <string[]>] [-Exclude <string[]>] [-Force] [-Credential <pscredential>]
 [-WhatIf] [-Confirm] [-NoNewline] [-Encoding <Encoding>] [-AsByteStream] [-Stream <string>]
 [<CommonParameters>]
```

### Path (Default) - All providers

```
Set-Content [-Path] <string[]> [-Value] <Object[]> [-PassThru] [-Filter <string>]
 [-Include <string[]>] [-Exclude <string[]>] [-Force] [-Credential <pscredential>] [-WhatIf]
 [-Confirm] [<CommonParameters>]
```

### LiteralPath - All providers

```
Set-Content [-Value] <Object[]> -LiteralPath <string[]> [-PassThru] [-Filter <string>]
 [-Include <string[]>] [-Exclude <string[]>] [-Force] [-Credential <pscredential>] [-WhatIf]
 [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

`Set-Content` is a string-processing cmdlet that writes new content or replaces the content in a
file. `Set-Content` replaces the existing content and differs from the `Add-Content` cmdlet that
appends content to a file. To send content to `Set-Content` you can use the **Value** parameter on
the command line or send content through the pipeline.

If you need to create files or directories for the following examples, see [New-Item](New-Item.md).

## EXAMPLES

### Example 1: Replace the contents of multiple files in a directory

This example replaces the content for multiple files in the current directory.

```powershell
Get-ChildItem -Path .\Test*.txt
```

```Output
Test1.txt
Test2.txt
Test3.txt
```

```powershell
Set-Content -Path .\Test*.txt -Value 'Hello, World'
Get-Content -Path .\Test*.txt
```

```Output
Hello, World
Hello, World
Hello, World
```

The `Get-ChildItem` cmdlet uses the **Path** parameter to list **.txt** files that begin with
`Test*` in the current directory. The `Set-Content` cmdlet uses the **Path** parameter to specify
the `Test*.txt` files. The **Value** parameter provides the text string **Hello, World** that
replaces the existing content in each file. The `Get-Content` cmdlet uses the **Path** parameter to
specify the `Test*.txt` files and displays each file's content in the PowerShell console.

### Example 2: Create a new file and write content

This example creates a new file and writes the current date and time to the file.

```powershell
Set-Content -Path .\DateTime.txt -Value (Get-Date)
Get-Content -Path .\DateTime.txt
```

```Output
1/30/2019 09:55:08
```

`Set-Content` uses the **Path** and **Value** parameters to create a new file named **DateTime.txt**
in the current directory. The **Value** parameter uses `Get-Date` to get the current date and time.
`Set-Content` writes the **DateTime** object to the file as a string. The `Get-Content` cmdlet uses
the **Path** parameter to display the content of **DateTime.txt** in the PowerShell console.

### Example 3: Replace text in a file

This command replaces all instances of word within an existing file.

```powershell
Get-Content -Path .\Notice.txt
```

```Output
Warning
Replace Warning with a new word.
The word Warning was replaced.
```

```powershell
(Get-Content -Path .\Notice.txt) |
    ForEach-Object {$_ -replace 'Warning', 'Caution'} |
        Set-Content -Path .\Notice.txt
Get-Content -Path .\Notice.txt
```

```Output
Caution
Replace Caution with a new word.
The word Caution was replaced.
```

The `Get-Content` cmdlet uses the **Path** parameter to specify the **Notice.txt** file in the
current directory. The `Get-Content` command is wrapped with parentheses so that the command
finishes before being sent down the pipeline.

The contents of the **Notice.txt** file are sent down the pipeline to the `ForEach-Object` cmdlet.
`ForEach-Object` uses the automatic variable `$_` and replaces each occurrence of **Warning** with
**Caution**. The objects are sent down the pipeline to the `Set-Content` cmdlet. `Set-Content` uses
the **Path** parameter to specify the **Notice.txt** file and writes the updated content to the
file.

The last `Get-Content` cmdlet displays the updated file content in the PowerShell console.

### Example 4: Use Filters with Set-Content

You can specify a filter to the `Set-Content` cmdlet. When using filters to qualify the **Path**
parameter, you need to include a trailing asterisk (`*`) to indicate the contents of the
path.

The following command set the content all `*.txt` files in the `C:\Temp`
directory to the **Value** empty.

```powershell
Set-Content -Path C:\Temp\* -Filter *.txt -Value "Empty"
```

## PARAMETERS

### -AsByteStream

This is a dynamic parameter made available by the **FileSystem** provider. For more information, see
[about_FileSystem_Provider](../Microsoft.PowerShell.Core/About/about_FileSystem_Provider.md).

Specifies that the content should be written as a stream of bytes. This parameter was introduced in
PowerShell 6.0.

A warning occurs when you use the **AsByteStream** parameter with the **Encoding** parameter. The
**AsByteStream** parameter ignores any encoding and the output is written as a stream of bytes.

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
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Encoding

This is a dynamic parameter made available by the **FileSystem** provider. For more information, see
[about_FileSystem_Provider](../Microsoft.PowerShell.Core/About/about_FileSystem_Provider.md).

Specifies the type of encoding for the target file. The default value is `utf8NoBOM`.

Encoding is a dynamic parameter that the FileSystem provider adds to `Set-Content`. This parameter
works only in file system drives.

The acceptable values for this parameter are as follows:

- `ascii`: Uses the encoding for the ASCII (7-bit) character set.
- `ansi`: Uses the encoding for the for the current culture's ANSI code page. This option was added
  in PowerShell 7.4.
- `bigendianunicode`: Encodes in UTF-16 format using the big-endian byte order.
- `bigendianutf32`: Encodes in UTF-32 format using the big-endian byte order.
- `oem`: Uses the default encoding for MS-DOS and console programs.
- `unicode`: Encodes in UTF-16 format using the little-endian byte order.
- `utf7`: Encodes in UTF-7 format.
- `utf8`: Encodes in UTF-8 format.
- `utf8BOM`: Encodes in UTF-8 format with Byte Order Mark (BOM)
- `utf8NoBOM`: Encodes in UTF-8 format without Byte Order Mark (BOM)
- `utf32`: Encodes in UTF-32 format.

Beginning with PowerShell 6.2, the **Encoding** parameter also allows numeric IDs of registered code
pages (like `-Encoding 1251`) or string names of registered code pages (like
`-Encoding "windows-1251"`). For more information, see the .NET documentation for
[Encoding.CodePage](/dotnet/api/system.text.encoding.codepage?view=netcore-2.2).

Starting with PowerShell 7.4, you can use the `Ansi` value for the **Encoding** parameter to pass
the numeric ID for the current culture's ANSI code page without having to specify it manually.

> [!NOTE]
> **UTF-7*** is no longer recommended to use. As of PowerShell 7.1, a warning is written if you
> specify `utf7` for the **Encoding** parameter.

```yaml
Type: System.Text.Encoding
Parameter Sets: (All)
Aliases:
Accepted values: ASCII, BigEndianUnicode, BigEndianUTF32, OEM, Unicode, UTF7, UTF8, UTF8BOM, UTF8NoBOM, UTF32

Required: False
Position: Named
Default value: utf8NoBOM
Accept pipeline input: False
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

Forces the cmdlet to set the contents of a file, even if the file is read-only. Implementation
varies from provider to provider. For more information, see
[about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md). The **Force** parameter
does not override security restrictions.

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

For more information, see
[about_Quoting_Rules](../Microsoft.Powershell.Core/About/about_Quoting_Rules.md).

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

### -NoNewline

This is a dynamic parameter made available by the **FileSystem** provider. For more information, see
[about_FileSystem_Provider](../Microsoft.PowerShell.Core/About/about_FileSystem_Provider.md).

The string representations of the input objects are concatenated to form the output. No spaces or
newlines are inserted between the output strings. No newline is added after the last output string.

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

### -PassThru

Returns an object that represents the content. By default, this cmdlet does not generate any output.

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

Specifies the path of the item that receives the content.
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

### -Stream

This is a dynamic parameter made available by the **FileSystem** provider. This Parameter is only
available on Windows. For more information, see
[about_FileSystem_Provider](../Microsoft.PowerShell.Core/About/about_FileSystem_Provider.md).

Specifies an alternative data stream for content. If the stream does not exist, this cmdlet creates
it. Wildcard characters are not supported.

**Stream** is a dynamic parameter that the **FileSystem** provider adds to `Set-Content`. This
parameter works only in file system drives.

You can use the `Set-Content` cmdlet to create or update the content of any alternate data stream,
such as `Zone.Identifier`. However, we do not recommend this as a way to eliminate security checks
that block files that are downloaded from the Internet. If you verify that a downloaded file is
safe, use the `Unblock-File` cmdlet.

This parameter was introduced in PowerShell 3.0. As of PowerShell 7.2, `Set-Content` can set the
content of alternative data streams from directories as well as files.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Value

Specifies the new content for the item.

```yaml
Type: System.Object[]
Parameter Sets: (All)
Aliases:

Required: True
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

### System.Object

You can pipe an object that contains the new value for the item to this cmdlet.

## OUTPUTS

### None

By default, this cmdlet returns no output.

### System.String

When you use the **PassThru** parameter, this cmdlet returns a string representing the content.

## NOTES

- `Set-Content` is designed for string processing. If you pipe non-string objects to `Set-Content`,
  it converts the object to a string before writing it. To write objects to files, use `Out-File`.
- The `Set-Content` cmdlet is designed to work with the data exposed by any provider. To list the
  providers available in your session, type `Get-PSProvider`. For more information, see
  [about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md).

## RELATED LINKS

[about_Aliases](../Microsoft.PowerShell.Core/About/about_Aliases.md)

[about_Automatic_Variables.md](../Microsoft.PowerShell.Core/About/about_Automatic_Variables.md)

[about_Providers](../Microsoft.PowerShell.Core/About/about_Providers.md)

[Add-Content](Add-Content.md)

[Clear-Content](Clear-Content.md)

[Get-ChildItem](Get-ChildItem.md)

[Get-Content](Get-Content.md)

[ForEach-Object](../Microsoft.PowerShell.Core/ForEach-Object.md)

[New-Item](New-Item.md)
