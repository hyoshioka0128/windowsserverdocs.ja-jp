---
title: Windows 管理センターを使ってみる
description: Windows 管理センターを使ってみる
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 02/15/2019
ms.openlocfilehash: 68b5c7b2c5bc8e93d653514b2664d96b97b07a9e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406848"
---
# <a name="get-started-with-windows-admin-center"></a>Windows 管理センターを使ってみる

>適用先:Windows Admin Center、Windows Admin Center Preview

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../understand/windows-admin-center.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## <a name="windows-admin-center-installed-on-windows-10"></a>Windows 10 にインストールされた windows 管理センター

> [!IMPORTANT]
> Windows 10 で Windows 管理センターを使用するには、ローカル管理者のグループのメンバーである必要があります。

### <a name="selecting-a-client-certificate"></a>クライアント証明書の選択

Windows 10 で windows 管理センターを初めて開くときは、必ず*Windows 管理センタークライアント*証明書を選択してください (そうしないと、"このページにアクセスできません" という HTTP 403 エラーが表示されます)。

Microsoft Edge で、このダイアログボックスが表示されたら、次のように入力します。
 
1. **その他の選択肢**をクリック

    ![](../media/launch-cert-1.png)

2. **Windows 管理センタークライアント**という名前の証明書を選択し、[ **OK]** をクリックします。

    ![](../media/launch-cert-2.png)

3. **常にアクセスを許可する**ことを確認し、 **[許可]** をクリックします。

    ![](../media/launch-cert-3.png)

## <a name="connecting-to-managed-nodes-and-clusters"></a>管理対象ノードとクラスターへの接続

Windows 管理センターのインストールが完了したら、メインの [概要] ページから、管理するサーバーまたはクラスターを追加できます。

 **単一のサーバーまたはクラスターを管理ノードとして追加する**

1. をクリックして **+ 追加** **すべて接続**します。

   ![](../media/launch/addserver0.png)

2. サーバー、フェールオーバークラスター、またはハイパー集約されるクラスター接続を追加することを選択します。
    
   ![](../media/launch/addserver1.png)

3. 管理するサーバーまたはクラスターの名前を入力し、 **[送信]** をクリックします。 サーバーまたはクラスターが [概要] ページの接続リストに追加されます。

   ![](../media/launch/addserver2.png)

   **--または--**

**複数のサーバーの一括インポート**

 1. **[サーバー接続の追加]** ページで、 **[サーバーのインポート]** タブを選択します。

    ![](../media/launch/import-servers.png)

 2. **[参照]** をクリックし、追加するサーバーの fqdn のコンマまたは改行を含むテキストファイルを選択します。

> [!Note]
> [PowerShell を使用した接続のエクスポート](#use-powershell-to-import-or-export-your-connections-with-tags)によって作成される .csv ファイルには、サーバー名以外の追加情報が含まれており、このインポート方法との互換性がありません。

  **--または--**

**Active Directory を検索してサーバーを追加する**

 1. **[サーバー接続の追加]** ページで、 **[検索 Active Directory]** タブを選択します。

    ![](../media/launch/search-ad.png)

 2. 検索条件を入力し、 **[検索]** をクリックします。 ワイルドカード (*) がサポートされています。

 3. 検索が完了したら、1つまたは複数の結果を選択し、必要に応じてタグを追加して、 **[追加]** をクリックします。

## <a name="authenticate-with-the-managed-node"></a>管理ノードで認証する ##

Windows 管理センターでは、管理対象ノードで認証を行うためのメカニズムがいくつかサポートされています。 シングルサインオンが既定値です。

**シングルサインオン**

現在の Windows 資格情報を使用して、管理対象ノードで認証を行うことができます。 これは既定の設定であり、Windows 管理センターはサーバーを追加するときにサインオンを試行します。 

**Windows Server にサービスとして展開された場合のシングルサインオン**

Windows Server に Windows 管理センターがインストールされている場合は、シングルサインオンのために追加の構成が必要になります。  [委任のために環境を構成する](../configure/user-access-control.md)

**--または--**

**管理アカウントを使用し*て*資格情報を指定する**

**すべての接続** で、一覧からサーバーを選択し、管理に使用する資格情報 を選択し**て**、管理ノードへの認証に使用する資格情報を指定します。

![](../media/launch-use-6.png)

Windows 管理センターが Windows Server でサービスモードで実行されているが、Kerberos 委任が構成されていない場合は、Windows 資格情報を再入力する必要があります。

![](../media/launch-use-7.png)

すべての接続に資格情報を適用することができます。これにより、その特定のブラウザーセッションに対して資格情報がキャッシュされます。 ブラウザーを再読み込みする場合は、**管理**者の資格情報を再入力する必要があります。

**ローカル管理者パスワードソリューション (LAPS)**

お使いの環境で[LAPS](https://technet.microsoft.com/mt227395.aspx)を使用していて、Windows 管理センターが WINDOWS 10 PC にインストールされている場合は、LAPS の資格情報を使用して、管理対象ノードで認証を行うことができます。 **このシナリオを使用する場合は、** [フィードバックを提供](http://aka.ms/WACFeedback)します。

## <a name="using-tags-to-organize-your-connections"></a>タグを使用した接続の整理

タグを使用して、接続リスト内の関連するサーバーを識別し、フィルター処理することができます。  これにより、サーバーのサブセットを接続リストに表示できます。  これは、多数の接続がある場合に特に便利です。

### <a name="edit-tags"></a>タグの編集

* [すべての接続] の一覧で1つまたは複数のサーバーを選択します。
* **[すべての接続]** の **[タグの編集]** をクリックします。

![](../media/launch/tags-5.png)

**[接続タグの編集]** ウィンドウでは、選択した接続のタグを変更、追加、または削除できます。

* 選択した接続に新しいタグを追加するには、 **[タグの追加]** を選択し、使用するタグ名を入力します。

* 既存のタグ名を使用して選択した接続にタグを付けるには、適用するタグ名の横にあるチェックボックスをオンにします。

* 選択したすべての接続からタグを削除するには、削除するタグの横にあるチェックボックスをオフにします。

* 選択した接続のサブセットにタグが適用されている場合、このチェックボックスは中間状態として表示されます。 チェックボックスをオンにして確認し、選択したすべての接続にタグを適用するか、もう一度クリックして選択を解除し、選択したすべての接続からタグを削除することができます。

![](../media/launch/tags-6.png)

### <a name="filter-connections-by-tag"></a>タグによる接続のフィルター

1つまたは複数のサーバー接続にタグを追加すると、接続リストでタグを表示し、タグで接続リストをフィルター処理できます。

* タグでフィルター処理するには、検索ボックスの横にあるフィルターアイコンを選択します。
![](../media/launch/tags-7.png)
* 選択したタグのフィルター動作を変更するには、"or"、"and"、または "not" を選択します。
![](../media/launch/tags-8.png)

## <a name="use-powershell-to-import-or-export-your-connections-with-tags"></a>PowerShell を使用した接続のインポートまたはエクスポート (タグあり)

```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to .csv files
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
```

### <a name="csv-file-format-for-importing-connections"></a>接続をインポートするための CSV ファイル形式

CSV ファイルの形式は、4つの見出し```"name","type","tags","groupId"```で始まり、その後に新しい行に各接続が続きます。

**name**は接続の FQDN です。

**種類**は接続の種類です。 Windows 管理センターに含まれる既定の接続については、次のいずれかを使用します。

| 接続の種類 | 接続文字列 |
|------|-------------------------------|
| Windows Server | msft. 接続の種類。サーバー |
| Windows 10 PC | msft. 接続の種類。 windows-クライアント |
| フェールオーバー クラスター | msft. 接続の種類. クラスター |
| ハイパー収束クラスター | msft. 接続の種類. ハイパー収束-クラスター |

**タグ**は、パイプで区切られます。

**groupId**は共有接続に使用されます。 この列の```global```値を使用して、共有接続を作成します。

### <a name="example-csv-file-for-importing-connections"></a>接続をインポートするための CSV ファイルの例

```
"name","type","tags","groupId"
"myServer.contoso.com","msft.sme.connection-type.server","hyperv"
"myDesktop.contoso.com","msft.sme.connection-type.windows-client","hyperv"
"teamcluster.contoso.com","msft.sme.connection-type.cluster","legacyCluster|WS2016","global"
"myHCIcluster.contoso.com,"msft.sme.connection-type.hyper-converged-cluster","myHCIcluster|hyperv|JIT|WS2019"
"teamclusterNode.contoso.com","msft.sme.connection-type.server","legacyCluster|WS2016","global"
"myHCIclusterNode.contoso.com","msft.sme.connection-type.server","myHCIcluster|hyperv|JIT|WS2019"
```

## <a name="import-rdcman-connections"></a>RDCman 接続のインポート

次のスクリプトを使用して、保存されている接続を[RDCman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/)内のファイルにエクスポートします。 その後、Windows 管理センターにファイルをインポートし、タグを使用して RDCMan グループ化階層を維持することができます。 試してみてください。

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

2. を作成する場合は。CSV ファイルで、次のコマンドを実行します。

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. 生成されたをインポートします。Windows 管理センターに CSV ファイルを配置すると、すべての RDCMan grouping 階層が接続リストのタグによって表されます。 詳細については、「 [PowerShell を使用した接続のインポートまたはエクスポート (タグあり)」を](#use-powershell-to-import-or-export-your-connections-with-tags)参照してください。

## <a name="view-powershell-scripts-used-in-windows-admin-center"></a>Windows 管理センターで使用される PowerShell スクリプトを表示する

サーバー、クラスター、または PC に接続したら、Windows 管理センターで使用可能な UI 操作を強化する PowerShell スクリプトを確認できます。 ツール内から、上部のアプリケーションバーにある PowerShell アイコンをクリックします。 ドロップダウンから目的のコマンドを選択して、対応する PowerShell スクリプトに移動します。

![](../media/launch/showscript.png)