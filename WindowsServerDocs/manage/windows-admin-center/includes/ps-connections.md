```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to a .csv file
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from a .csv file
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files, and remove any connections that are not explictly in the imported file using the -prune switch parameter 
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv" -prune
```
### <a name="csv-file-format-for-importing-connections"></a>接続をインポートする場合の CSV ファイルの形式

CSV ファイルの形式は、4 つの見出し ```"name","type","tags","groupId"``` で始まり、新しい行に各接続が続きます。

**name** は接続の FQDN です

**type** は接続の種類です。 Windows Admin Center に含まれる既定の接続については、次のいずれかを使用します。

| 接続の種類 | 接続文字列 |
|------|-------------------------------|
| Windows Server | msft.sme.connection-type.server |
| Windows 10 PC | msft.sme.connection-type.windows-client |
| フェールオーバー クラスター | msft.sme.connection-type.cluster |
| ハイパーコンバージド クラスター | msft.sme.connection-type.hyper-converged-cluster |

**tags** はパイプで区切られます。

**groupId** は共有接続に使用されます。 これを共有接続にするには、この列の値 ```global``` を使用します。

> [!NOTE]
> 共有接続の変更はゲートウェイ管理者に限定されています。ユーザーは PowerShell を使用して、自分の個人用接続リストを変更できます。

### <a name="example-csv-file-for-importing-connections"></a>接続をインポートする場合の CSV ファイルの例

```
"name","type","tags","groupId"
"myServer.contoso.com","msft.sme.connection-type.server","hyperv"
"myDesktop.contoso.com","msft.sme.connection-type.windows-client","hyperv"
"teamcluster.contoso.com","msft.sme.connection-type.cluster","legacyCluster|WS2016","global"
"myHCIcluster.contoso.com,"msft.sme.connection-type.hyper-converged-cluster","myHCIcluster|hyperv|JIT|WS2019"
"teamclusterNode.contoso.com","msft.sme.connection-type.server","legacyCluster|WS2016","global"
"myHCIclusterNode.contoso.com","msft.sme.connection-type.server","myHCIcluster|hyperv|JIT|WS2019"
```

## <a name="import-rdcman-connections"></a>RDCman 接続をインポートする

次のスクリプトを使用して、[RDCman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/) 内の保存されている接続をファイルにエクスポートします。 次に、Windows Admin Center にファイルをインポートし、タグを使用して RDCMan グループの階層を維持することができます。 お試しください。

1. 次のコードをコピーし、PowerShell セッションに貼り付けます。

   ```powershell
   #Helper function for RdgToWacCsv
   function AddServers {
    param (
    [Parameter(Mandatory = $true)]
    [Xml.XmlLinkedNode]
    $node,
    [Parameter()]
    [String[]]
    $tags,
    [Parameter(Mandatory = $true)]
    [String]
    $csvPath
    )
    if ($node.LocalName -eq 'server') {
        $serverName = $node.properties.name
        $tagString = $tags -join "|"
        Add-Content -Path $csvPath -Value ('"'+ $serverName + '","msft.sme.connection-type.server","'+ $tagString +'"')
    } 
    elseif ($node.LocalName -eq 'group' -or $node.LocalName -eq 'file') {
        $groupName = $node.properties.name
        $tags+=$groupName
        $currNode = $node.properties.NextSibling
        while ($currNode) {
            AddServers -node $currNode -tags $tags -csvPath $csvPath
            $currNode = $currNode.NextSibling
        }
    } 
    else {
        # Node type isn't relevant to tagging or adding connections in WAC
    }
    return
   }

   <#
   .SYNOPSIS
   Convert an .rdg file from Remote Desktop Connection Manager into a .csv that can be imported into Windows Admin Center, maintaining groups via server tags. This will not modify the existing .rdg file and will create a new .csv file

    .DESCRIPTION
    This converts an .rdg file into a .csv that can be imported into Windows Admin Center.

    .PARAMETER RDGfilepath
    The path of the .rdg file to be converted. This file will not be modified, only read.

    .PARAMETER CSVdirectory
    Optional. The directory you wish to export the new .csv file. If not provided, the new file is created in the same directory as the .rdg file.

    .EXAMPLE
    C:\PS> RdgToWacCsv -RDGfilepath "rdcmangroup.rdg"
    #>
   function RdgToWacCsv {
    param(
        [Parameter(Mandatory = $true)]
        [String]
        $RDGfilepath,
        [Parameter(Mandatory = $false)]
        [String]
        $CSVdirectory
    )
    [xml]$RDGfile = Get-Content -Path $RDGfilepath
    $node = $RDGfile.RDCMan.file
    if (!$CSVdirectory){
        $csvPath = [System.IO.Path]::GetDirectoryName($RDGfilepath) + [System.IO.Path]::GetFileNameWithoutExtension($RDGfilepath) + "_WAC.csv"
    } else {
        $csvPath = $CSVdirectory + [System.IO.Path]::GetFileNameWithoutExtension($RDGfilepath) + "_WAC.csv"
    }
    New-item -Path $csvPath
    Add-Content -Path $csvPath -Value '"name","type","tags"'
    AddServers -node $node -csvPath $csvPath
    Write-Host "Converted $RDGfilepath `nOutput: $csvPath"
   }
   ```

2. .CSV ファイルを作成するには、次のコマンドを実行します。

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. 結果の .CSV ファイルを Windows Admin Center にインポートすると、すべての RDCMan グループ階層が接続リストのタグで表されます。 詳細については、「[PowerShell を使用して (タグを使って) 接続をインポートまたはエクスポートする](#use-powershell-to-import-or-export-your-connections-with-tags)」を参照してください。