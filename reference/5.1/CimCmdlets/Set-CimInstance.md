---
external help file: Microsoft.Management.Infrastructure.CimCmdlets.dll-Help.xml
Locale: en-US
Module Name: CimCmdlets
ms.date: 12/09/2022
online version: https://learn.microsoft.com/powershell/module/cimcmdlets/set-ciminstance?view=powershell-5.1&WT.mc_id=ps-gethelp
schema: 2.0.0
aliases:
  - scim
title: Set-CimInstance
---
# Set-CimInstance

## SYNOPSIS
Modifies a CIM instance on a CIM server by calling the ModifyInstance method of the CIM class.

## SYNTAX

### CimInstanceComputerSet (Default)

```
Set-CimInstance [-ComputerName <String[]>] [-ResourceUri <Uri>]
 [-OperationTimeoutSec <UInt32>] [-InputObject] <CimInstance> [-Property <IDictionary>]
 [-PassThru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### CimInstanceSessionSet

```
Set-CimInstance -CimSession <CimSession[]> [-ResourceUri <Uri>]
 [-OperationTimeoutSec <UInt32>] [-InputObject] <CimInstance> [-Property <IDictionary>]
 [-PassThru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### QuerySessionSet

```
Set-CimInstance -CimSession <CimSession[]> [-Namespace <String>]
 [-OperationTimeoutSec <UInt32>] [-Query] <String> [-QueryDialect <String>]
 -Property <IDictionary> [-PassThru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### QueryComputerSet

```
Set-CimInstance [-ComputerName <String[]>] [-Namespace <String>]
 [-OperationTimeoutSec <UInt32>] [-Query] <String> [-QueryDialect <String>]
 -Property <IDictionary> [-PassThru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

## DESCRIPTION

This cmdlet modifies a CIM instance on a CIM server.

If the **InputObject** parameter is not specified, the cmdlet works in one of the following ways:

- If neither the **ComputerName** parameter nor the **CimSession** parameter is specified, then this
  cmdlet works on local Windows Management Instrumentation (WMI) using a Component Object Model
  (COM) session.
- If either the **ComputerName** parameter or the **CimSession** parameter is specified, then this
  cmdlet works against the CIM server specified by either the **ComputerName** parameter or the
  **CimSession** parameter.

If the **InputObject** parameter is specified, the cmdlet works in one of the following ways:

- If neither the **ComputerName** parameter nor the **CimSession** parameter is specified, then this
  cmdlet uses the CIM session or computer name from the input object.
- If the either the **ComputerName** parameter or the **CimSession** parameter is specified, then
  this cmdlet uses the either the **CimSession** parameter value or **ComputerName** parameter
  value. This is not very common.

## EXAMPLES

### Example 1: Set the CIM instance

This example sets the value of the **VariableValue** property to **abcd** using the **Query**
parameter. You can modify instances matching a Windows Management Instrumentation Query Language
(WQL) query.

```powershell
$instance = @ {
    Query = 'Select * from Win32_Environment where name LIKE "testvar%"'
    Property = @{VariableValue="abcd"}
}
Set-CimInstance @instance
```

### Example 2: Set the CIM instance property using pipeline

This example retrieves the CIM instance object filtered by the **Query** parameter using the
`Get-CimInstance` cmdlet. The `Set-CimInstance` cmdlet modifies the value of **VariableValue**
property to **abcd**.

```powershell
Get-CimInstance -Query 'Select * from Win32_Environment where name LIKE "testvar%"' |
  Set-CimInstance -Property @{VariableValue="abcd"}
```

### Example 3: Set the CIM instance property using input object

```powershell
$x = Get-CimInstance -Query 'Select * from Win32_Environment where Name="testvar"'
Set-CimInstance -InputObject $x -Property @{VariableValue="somevalue"} -PassThru
```

This example retrieves the CIM instance objects filtered by the Query parameter in to a variable
`$x` using `Get-CimInstance`, and then passes the contents of the variable to the `Set-CimInstance`
cmdlet. `Set-CimInstance` then modifies the **VariableValue** property to **somevalue**. Because the
**PassThru** parameter is used, This example returns a modified CIM instance object.

### Example 4: Set the CIM instance property

This example retrieves the CIM instance object that is specified in the **Query** parameter into a
variable `$x` using the `Get-CimInstance` cmdlet, and changes the **VariableValue** property value
of the object to change. The CIM instance object is then saved using the `Set-CimInstance` cmdlet.
Because the **PassThru** parameter is used, This example returns a modified CIM instance object.

```powershell
$x = Get-CimInstance -Query 'Select * from Win32_Environment where name="testvar"'
$x.VariableValue = "Change"
Set-CimInstance -CimInstance $x -PassThru
```

### Example 5: Show the list of CIM instances to modify using WhatIf

This example uses the common parameter **WhatIf** to specify that the modification should not be
done, but only output what would happen if it were done.

```powershell
$instance = @{
    Query = 'Select * from Win32_Environment where name LIKE "testvar%"'
    Property = @{VariableValue="abcd"}
    WhatIf = $true
}
Set-CimInstance @instance
```

### Example 6: Set the CIM instance after confirmation from the user

This example uses the common parameter **Confirm** to specify that the modification should be done
only after confirmation from the user.

```powershell
$instance = @{
    Query = 'Select * from Win32_Environment where name LIKE "testvar%"'
    Property = @{VariableValue="abcd"}
    Confirm = $true
}
Set-CimInstance @instance
```

### Example 7: Set the created CIM instance

This example creates a CIM instance with the specified properties using the `New-CimInstance`
cmdlet, and retrieves its contents in to a variable `$x`. The variable is then passed to the
`Set-CimInstance` cmdlet, which modifies the value of **VariableValue** property to **somevalue**.
Because the **PassThru** parameter is used, This example returns a modified CIM instance object.

```powershell
$instance = @{
    ClassName = 'Win32_Environment'
    Property = @{
        Name="testvar"
        UserName="domain\user"
    }
    Key = 'Name', 'UserName'
    ClientOnly = $true
}
$x = New-CimInstance @instance
Set-CimInstance -CimInstance $x -Property @{VariableValue="somevalue"} -PassThru
```

## PARAMETERS

### -CimSession

Runs the cmdlets on a remote computer. Enter a computer name or a session object, such as the output
of a `New-CimSession` or `Get-CimSession` cmdlet.

```yaml
Type: Microsoft.Management.Infrastructure.CimSession[]
Parameter Sets: CimInstanceSessionSet, QuerySessionSet
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -ComputerName

Specifies the name of the computer on which you want to run the CIM operation. You can specify a
fully qualified domain name (FQDN) or a NetBIOS name.

If you do not specify this parameter, the cmdlet performs the operation on the local computer using
Component Object Model (COM).

If you specify this parameter, the cmdlet creates a temporary session to the specified computer
using the WsMan protocol.

If multiple operations are being performed on the same computer, connecting using a CIM session
gives better performance.

```yaml
Type: System.String[]
Parameter Sets: CimInstanceComputerSet, QueryComputerSet
Aliases: CN, ServerName

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -InputObject

Specifies a CIM instance object to use as input.

The **InputObject** parameter doesn't enumerate over collections. If a collection is passed, an
error is thrown. When working with collections, pipe the input to enumerate the values.

```yaml
Type: Microsoft.Management.Infrastructure.CimInstance
Parameter Sets: CimInstanceComputerSet, CimInstanceSessionSet
Aliases: CimInstance

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -Namespace

Specifies the namespace for the CIM operation. The default namespace is **root/CIMV2**. You can use
tab completion to browse the list of namespaces, because PowerShell gets a list of namespaces from
the local WMI server to provide the list of namespaces.

```yaml
Type: System.String
Parameter Sets: QuerySessionSet, QueryComputerSet
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -OperationTimeoutSec

Specifies the amount of time that the cmdlet waits for a response from the computer. By default, the
value of this parameter is 0, which means that the cmdlet uses the default timeout value for the
server.

If the **OperationTimeoutSec** parameter is set to a value less than the robust connection retry
timeout of 3 minutes, network failures that last more than the value of the **OperationTimeoutSec**
parameter are not recoverable, because the operation on the server times out before the client can
reconnect.

```yaml
Type: System.UInt32
Parameter Sets: (All)
Aliases: OT

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -PassThru

Returns an object representing the item with which you are working. By default, this cmdlet does not
generate any output.

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

### -Property

Specifies the properties of the CIM instance as a hash table (using name-value pairs). Only the
properties specified using this parameter are changed. Other properties of the CIM instance are not
changed.

```yaml
Type: System.Collections.IDictionary
Parameter Sets: CimInstanceComputerSet, CimInstanceSessionSet, QuerySessionSet, QueryComputerSet
Aliases: Arguments

Required: True (QuerySessionSet, QueryComputerSet), False (CimInstanceComputerSet, CimInstanceSessionSet)
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -Query

Specifies a query to run on the CIM server to retrieve CIM instances on which to run the cmdlet. You
can specify the query dialect using the QueryDialect parameter.

If the value specified contains double quotes (`"`), single quotes (`'`), or a backslash (`\`), you
must escape those characters by prefixing them with the backslash (`\`) character. If the value
specified uses the WQL **LIKE** operator, then you must escape the following characters by enclosing
them in square brackets (`[]`): percent (`%`), underscore (`_`), or opening square bracket (`[`).

```yaml
Type: System.String
Parameter Sets: QuerySessionSet, QueryComputerSet
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -QueryDialect

Specifies the query language used for the Query parameter. The acceptable values for this parameter
are: **WQL** or **CQL**. The default value is **WQL**.

```yaml
Type: System.String
Parameter Sets: QuerySessionSet, QueryComputerSet
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: True (ByPropertyName)
Accept wildcard characters: False
```

### -ResourceUri

Specifies the resource uniform resource identifier (URI) of the resource class or instance. The URI
is used to identify a specific type of resource, such as disks or processes, on a computer.

A URI consists of a prefix and a path to a resource. For example:

- `http://schemas.microsoft.com/wbem/wsman/1/wmi/root/cimv2/Win32_LogicalDisk`
- `http://intel.com/wbem/wscim/1/amt-schema/1/AMT_GeneralSettings`

By default, if you do not specify this parameter, the DMTF standard resource URI
`http://schemas.dmtf.org/wbem/wscim/1/cim-schema/2/` is used and the class name is appended to it.

**ResourceUri** can only be used with CIM sessions created using the WSMan protocol, or when
specifying the **ComputerName** parameter, which creates a CIM session using WSMan. If you specify
this parameter without specifying the **ComputerName** parameter, or if you specify a CIM session
created using DCOM protocol, you will get an error, because the DCOM protocol does not support the
**ResourceUri** parameter.

If both the **ResourceUri** parameter and the **Filter** parameter are specified, the **Filter**
parameter is ignored.

```yaml
Type: System.Uri
Parameter Sets: CimInstanceComputerSet, CimInstanceSessionSet
Aliases:

Required: False
Position: Named
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

### Microsoft.Management.Infrastructure.CimInstance

## OUTPUTS

### None

By default, this cmdlet returns no output.

### Microsoft.Management.Infrastructure.CimInstance

When you use the **PassThru** parameter, this cmdlet returns the modified CIM instance object.

## NOTES

## RELATED LINKS

[Get-CimInstance](Get-CimInstance.md)

[New-CimInstance](New-CimInstance.md)

[Remove-CimInstance](Remove-CimInstance.md)
