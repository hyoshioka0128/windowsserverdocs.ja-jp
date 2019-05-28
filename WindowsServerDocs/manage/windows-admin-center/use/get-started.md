---
title: Windows Admin Center を概要します。
description: Windows Admin Center を概要します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 02/15/2019
ms.openlocfilehash: ff1f949c764473a63eafa25346949d710699dbd1
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222720"
---
# <a name="get-started-with-windows-admin-center"></a>Windows Admin Center を概要します。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../understand/windows-admin-center.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## <a name="windows-admin-center-installed-on-windows-10"></a>Windows 10 にインストールされている Windows Admin Center

> [!IMPORTANT]
> Windows 10 で Windows Admin Center を使用するローカル管理者のグループのメンバーがあります。

### <a name="selecting-a-client-certificate"></a>クライアント証明書の選択

Windows 10、Windows Admin Center では、最初に開いた際に、ことを選択することを確認して、 *Windows Admin Center クライアント*証明書を (それ以外の場合、「このページを取得できません」という HTTP 403 エラーが表示されます)。

Microsoft edge では、このダイアログ ボックスが表示されたら。
 
1. クリックして**より多くの選択肢**

    ![](../media/launch-cert-1.png)

2. というラベルの付いた証明書を選択**Windows Admin Center クライアント**クリック**OK**

    ![](../media/launch-cert-2.png)

3. 必ず**アクセスを常に許可する**が選択されているし、をクリックして**許可します。**

    ![](../media/launch-cert-3.png)

## <a name="connecting-to-managed-nodes-and-clusters"></a>管理対象ノードとクラスターに接続します。

Windows Admin Center のインストールを完了すると後、は、サーバーまたは、メイン概要ページから管理するクラスターを追加できます。

 **管理対象ノードとして 1 台のサーバーまたはクラスターを追加します。**

 1. をクリックして **+ 追加** **すべて接続**します。

    ![](../media/launch/addserver0.png)

 2. 選択すると、サーバー、フェールオーバー クラスターまたは Hyper-Converged クラスター接続を追加します。
    
    ![](../media/launch/addserver1.png)

 3. サーバーまたは管理 をクリックしてクラスターの名前を入力**送信**します。 サーバーまたはクラスターは、[概要] ページで、接続リストに追加されます。

    ![](../media/launch/addserver2.png)

   **--または--**

**複数のサーバーを一括インポートします。**

 1. **サーバー接続の追加**ページで、選択、**インポート サーバー**タブ。

    ![](../media/launch/import-servers.png)

 2. クリックして**参照**コンマを含むテキスト ファイルを選択するか、新しい行区切りを追加するサーバーの Fqdn の一覧。

    **--または--**

**サーバーを追加するには、Active Directory の検索**

 1. **サーバー接続の追加**ページで、選択、 **Active Directory を検索**タブ。

    ![](../media/launch/search-ad.png)

 2. 検索条件を入力し、クリックして**検索**します。 ワイルドカード (*) がサポートされています。

 3. 検索が完了すると、結果の 1 つ以上選択、必要に応じてタグを追加、およびクリックして**追加**します。

## <a name="authenticate-with-the-managed-node"></a>管理対象ノードでの認証します。 ##

Windows Admin Center には、管理対象ノードを認証するためのいくつかのメカニズムがサポートされています。 シングル サインオンが既定値です。

**シングル サインオン**

現在の Windows 資格情報は、管理対象ノードでの認証に使用できます。 これは、既定値と、Windows Admin Center は、サーバーを追加するときに、サインオンしようとします。 

**シングル サインオンで Windows Server 上のサービスとしてデプロイした場合**

Windows Server に Windows Admin Center をインストールした場合は、追加の構成が必要でシングル サインオンです。  [委任用に環境を構成します。](..\configure\user-access-control.md)

**--または--**

**使用*管理に*資格情報を指定する**

**すべて接続**、一覧からサーバーを選択および選択**管理に**管理ノードへの認証に使用する資格情報を指定します。

![](../media/launch-use-6.png)

Windows Admin Center は、Windows Server でサービス モードで実行されている Kerberos 委任が構成されていない場合、Windows 資格情報を再入力する必要があります。

![](../media/launch-use-7.png)

その特定のブラウザー セッションのキャッシュのすべての接続に資格情報を適用することがあります。 再入力する必要がありますが、ブラウザーを再読み込みする場合、**管理に**資格情報。

**ローカル管理者のパスワード ソリューション (LAPS)**

環境内で使用する場合[LAPS](https://technet.microsoft.com/mt227395.aspx)、Windows Admin Center の Windows 10 PC にインストールされている必要があるとは、管理ノードでの認証に LAPS 資格情報を使用することができます。 **このシナリオを使用する場合は、次のようにしてください。** [フィードバック](http://aka.ms/WACFeedback)します。

## <a name="using-tags-to-organize-your-connections"></a>タグを使用して、接続を整理するには

特定し、接続の一覧で関連するサーバーをフィルター処理、タグを使用することができます。  これにより、接続の一覧で、サーバーのサブセットを表示できます。  これは、多くの接続がある場合に特に便利です。

### <a name="edit-tags"></a>タグを編集します。

* すべての接続の一覧で、サーバーまたは複数のサーバーを選択します。
* [**すべて接続**、] をクリックして**タグの編集**

![](../media/launch/tags-5.png)

**接続タグの編集**ウィンドウでは、変更、追加、または、選択した接続からタグを削除することができます。

* 新しいタグを選択した接続を追加するには、選択**タグを追加**を使用したいタグ名を入力します。

* 既存のタグ名との接続を選択したタグを適用するタグ名の横にあるボックスを確認します。

* 選択したすべての接続からタグを削除するには、削除するタグの横にあるボックスをオフにします。

* 選択した接続のサブセットにタグを適用する場合は、チェック ボックスが中間の状態で表示されます。 チェックし、選択したすべての接続にタグを適用またはそれをオフにし、選択したすべての接続から、タグの削除をもう一度クリックするボックスをクリックすることができます。

![](../media/launch/tags-6.png)

### <a name="filter-connections-by-tag"></a>タグを使用して接続をフィルター処理します。

タグを 1 つまたは複数のサーバー接続を追加すると、接続の一覧で、タグを表示し、タグを使用して接続の一覧をフィルター処理できます。

* タグでフィルターするには、検索ボックスの横にあるフィルター アイコンを選択します。
![](../media/launch/tags-7.png)
* 選択することができます「または」、"and"、または、選択されたタグのフィルターの動作を変更するには、"not"。
![](../media/launch/tags-8.png)

## <a name="use-powershell-to-import-or-export-your-connections-with-tags"></a>PowerShell を使用して、インポートまたはエクスポート (タグ) で接続する

> 適用先:Windows Admin Center Preview

Windows Admin Center Preview には、インポートまたは接続一覧をエクスポートする PowerShell モジュールが含まれています。

```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to .csv files
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
```

### <a name="csv-file-format-for-importing-connections"></a>接続をインポートするための CSV ファイルの形式

CSV ファイルの形式は次の 4 つの見出しで始まる```"name","type","tags","groupId"```、その後に新しい行に各接続します。

**名前**は、接続の FQDN です

**型**は、接続の種類。 、Windows Admin Center に付属の既定の接続には、次のいずれかを使用します。

| 接続の種類 | 接続文字列 |
|------|-------------------------------|
| Windows Server | msft.sme.connection-type.server |
| Windows 10 PC | msft.sme.connection-type.windows-client |
| フェールオーバー クラスター | msft.sme.connection-type.cluster |
| ハイパー コンバージド クラスター | msft.sme.connection-type.hyper-converged-cluster |

**タグ**はパイプで区切られました。

**groupId**共有接続のために使用します。 値を使用して```global```接続を共有するには、この列にします。

### <a name="example-csv-file-for-importing-connections"></a>接続のインポートの CSV ファイルの例

```
"name","type","tags","groupId"
"myServer.contoso.com","msft.sme.connection-type.server","hyperv"
"myDesktop.contoso.com","msft.sme.connection-type.windows-client","hyperv"
"teamcluster.contoso.com","msft.sme.connection-type.cluster","legacyCluster|WS2016","global"
"myHCIcluster.contoso.com,"msft.sme.connection-type.hyper-converged-cluster","myHCIcluster|hyperv|JIT|WS2019"
"teamclusterNode.contoso.com","msft.sme.connection-type.server","legacyCluster|WS2016","global"
"myHCIclusterNode.contoso.com","msft.sme.connection-type.server","myHCIcluster|hyperv|JIT|WS2019"
```

## <a name="import-rdcman-connections"></a>インポートの RDCman 接続

保存された接続をエクスポートする次のスクリプトを使用して[RDCman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/)ファイル。 ことができますし、ファイルをインポート、Windows Admin Center では、タグを使用して、RDCMan グループ階層を維持します。 試してみましょう。

1. コピーして PowerShell セッションに次のコードを貼り付けます。

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

2. 作成します。CSV ファイル、次のコマンドを実行します。

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. 結果をインポートします。内の CSV ファイルには、Windows Admin Center と、すべての RDCMan グループ階層は、接続の一覧でタグを使用して表されます。 詳細については、次を参照してください。 [PowerShell インポートまたはエクスポート (タグ) で接続を使用して](#use-powershell-to-import-or-export-your-connections-with-tags)します。

## <a name="view-powershell-scripts-used-in-windows-admin-center"></a>Windows Admin Center で使用される PowerShell スクリプトを表示します。

をサーバー、クラスター、または PC に接続した後に確認できる PowerShell スクリプトは、その電源 UI アクションを使用できます Windows Admin Center。 ツールで、上部アプリケーション バーの PowerShell アイコンをクリックします。 ドロップダウン リストで、対応する PowerShell スクリプトに移動するには、関心のあるコマンドを選択します。

![](../media/launch/showscript.png)