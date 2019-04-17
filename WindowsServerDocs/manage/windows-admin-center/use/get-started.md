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
ms.openlocfilehash: f4fd9f69e75ed80bbdb345b4041c2337c65ec2e6
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296654"
---
# Windows Admin Center を概要します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../understand/windows-admin-center.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## Windows 10 にインストールされている Windows Admin Center

> [!IMPORTANT]
> Windows 10 で Windows Admin Center を使用するローカル管理者のグループのメンバーである必要があります。

### クライアント証明書の選択

初めての Windows 10 で Windows Admin Center を開くことを確認 (それ以外の場合「このページに取得することはできません」という HTTP 403 エラーを取得します)、 *Windows Admin Center のクライアント*証明書を選択します。

Microsoft Edge の場合、このダイアログ ボックスが表示されたら: で
 
1. **多くの選択肢**をクリックします。

    ![](../media/launch-cert-1.png)

2. というラベルの付いた**Windows Admin Center のクライアント**証明書を選択し、 **[ok]** をクリックしてください

    ![](../media/launch-cert-2.png)

3. **常に許可するアクセス**が選択されているかどうかを確認し、**許可する**] をクリックしてください

    ![](../media/launch-cert-3.png)

## 管理対象のノードとクラスターへの接続

Windows Admin Center のインストールを完了すると後、は、サーバーまたはクラスターをメインの概要ページから管理を追加できます。

 **1 台のサーバーまたはクラスター管理ノードとして追加します。**

 1. **すべての接続**[ **+ 追加]** をクリックします。

    ![](../media/launch/addserver0.png)

 2. 選択すると、サーバー、フェールオーバー クラスターまたはハイパーコンバージド クラスターの接続を追加します。
    
    ![](../media/launch/addserver1.png)

 3. サーバーまたはクラスターを管理し、**送信**] をクリックしての名前を入力します。 サーバーまたはクラスターは、概要ページで、接続の一覧に追加されます。

    ![](../media/launch/addserver2.png)

   **-- または --**

**一括インポートの複数のサーバー**

 1. **サーバー接続の追加**] ページで、**インポート サーバー** ] タブを選択します。

    ![](../media/launch/import-servers.png)

 2. [**参照**] をクリックし、コンマ、または新しい行の区切りを追加するサーバーの Fqdn の一覧を含むテキスト ファイルを選択します。

    **-- または --**

**Active Directory を検索してサーバーを追加する.**

 1. **サーバー接続の追加**] ページで、 **Active Directory を検索**] タブを選択します。

    ![](../media/launch/search-ad.png)

 2. 検索条件を入力し、[**検索**] をクリックします。 ワイルドカード (*) がサポートされています。

 3. 検索が完了すると、結果の 1 つ以上選択、必要に応じてタグを追加し、**追加**] をクリックします。

## 管理ノードを使用して認証します。 ##

Windows Admin Center は、管理ノードで認証するためのいくつかのメカニズムをサポートします。 シングル サインオンの既定値です。

**シングル サインオン**

現在の Windows 資格情報を使用すると、管理ノードを使用して認証します。 これは、既定のし、Windows Admin Center は、サーバーを追加する場合、サインオンしようとします。 

**シングル サインオン展開されると Windows Server 上のサービスとして**

Windows Server に Windows Admin Center をインストールしている場合は、追加の構成がシングル サインオンが必要です。  [委任用の環境を構成します。](..\configure\user-access-control.md)

**-- または --**

**指定の資格情報を*管理に*使用します。**

[**すべての接続**] リストからサーバーを選択し、**管理に**管理ノードへの認証に使用する資格情報を指定する選択します。

![](../media/launch-use-6.png)

Windows Admin Center は Windows Server でサービス モードで実行されている場合は、Kerberos 委任を構成する必要はありませんは、Windows 資格情報を再入力する必要があります。

![](../media/launch-use-7.png)

その特定のブラウザー セッションでキャッシュのすべての接続には、資格情報を適用することがあります。 お使いのブラウザーを再読み込みする場合は、**管理に**資格情報を再入力する必要があります。

**ローカル管理者のパスワード ソリューション (LAPS)**

お客様の環境では、 [LAPS](https://technet.microsoft.com/mt227395.aspx)を使用する場合は、管理ノードを使用して認証を LAPS 資格情報を使用できます。 **このシナリオをください使用する場合**[フィードバックを提供](http://aka.ms/WACFeedback)します。

## タグを使用して、接続を整理するには

タグを使用して、識別し、接続の一覧に関連するサーバーをフィルター処理することができます。  これにより、接続の一覧で、サーバーのサブセットを表示できます。  これは、多数の接続がある場合に特に便利です。

### タグを編集します。

* すべての接続の一覧で、サーバーまたは複数のサーバーを選択します。
* **すべての接続**] の下の [**タグの編集**] をクリックします

![](../media/launch/tags-5.png)

**接続のタグを編集**ウィンドウでは、変更、追加、または、選択した接続からタグを削除できます。

* 選択した接続には、新しいタグを追加するには、**タグの追加**を選択し、使用するには、タグ名を入力します。

* 既存のタグの名前を選択した接続のタグを付けるためには、適用するタグ名の横のボックスを確認します。

* タグを削除する、選択したすべての接続から、削除するタグの横にあるチェック ボックスをオフにします。

* 選択した接続のサブセットにタグを適用する場合は、中間の状態にチェック ボックスが表示されます。 確認して、オフにし、選択したすべての接続から、タグの削除をもう一度クリックして、または選択したすべての接続にタグを適用するボックスをオンにすることができます。

![](../media/launch/tags-6.png)

### タグで接続をフィルター処理します。

タグは、1 つまたは複数のサーバー接続を追加したら、接続の一覧にタグを表示し、タグを使用して接続の一覧をフィルター処理できます。

* タグをでフィルター処理するには、検索ボックスの横にあるフィルター アイコンを選択します。
![](../media/launch/tags-7.png)
* 選択することができます「または」、「と」、または選択したタグのフィルターの動作を変更するには、「いない」です。
![](../media/launch/tags-8.png)

## PowerShell を使用してインポートまたはエクスポート タグの接続

> 適用対象: Windows Admin Center Preview

Windows Admin Center Preview には、PowerShell モジュール インポートまたはエクスポート、接続の一覧にはが含まれます。

```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to .csv files
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
```

### 接続のインポートの CSV ファイルの形式

CSV ファイルの形式は次の 4 つの見出しで始まる```"name","type","tags","groupId"```、その後に新しい行には、各接続します。

**名前**は、接続の FQDN

**型**は、接続の種類です。 Windows Admin Center に含まれている既定の接続で、次のいずれかを使用します。

| 接続の種類 | 接続文字列 |
|------|-------------------------------|
| Windows Server | msft.sme.connection type.server |
| Windows 10 PC | msft.sme.connection から type.windows クライアント |
| フェールオーバー クラスター | msft.sme.connection type.cluster |
| ハイパーコンバージド クラスター | msft.sme.connection-type.hyper 集約型のクラスター |

**タグ**は、パイプ文字で区切られました。

**groupId**は、共有の接続に使用されます。 値を使用して```global```接続を共有するには、この列にします。

### 接続のインポートの CSV ファイルの例

```
"name","type","tags","groupId"
"myServer.contoso.com","msft.sme.connection-type.server","hyperv"
"myDesktop.contoso.com","msft.sme.connection-type.windows-client","hyperv"
"teamcluster.contoso.com","msft.sme.connection-type.cluster","legacyCluster|WS2016","global"
"myHCIcluster.contoso.com,"msft.sme.connection-type.hyper-converged-cluster","myHCIcluster|hyperv|JIT|WS2019"
"teamclusterNode.contoso.com","msft.sme.connection-type.server","legacyCluster|WS2016","global"
"myHCIclusterNode.contoso.com","msft.sme.connection-type.server","myHCIcluster|hyperv|JIT|WS2019"
```

## インポート RDCman 接続

[RDCman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/)で保存された接続をファイルにエクスポートするのには、次のスクリプトを使用します。 ファイルにインポート Windows Admin Center では、タグを使って、RDCMan グループ階層を維持します。 試してみましょう。

1. コピーし、PowerShell セッションに以下のコードを貼り付けます。

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

3. その結果をインポートします。Windows Admin Center を CSV ファイルと、すべての RDCMan グループ化階層は、接続の一覧にタグを使用して表されます。 詳細については、 [PowerShell をインポートまたはエクスポート タグの接続を使って](#use-powershell-to-import-or-export-your-connections-with-tags)を参照してください。

## Windows Admin Center で使用されている PowerShell スクリプトを表示します。

サーバー、クラスター、または PC に接続したら後を見ることができます PowerShell スクリプトその電源 UI の操作を利用可能な Windows Admin Center でします。 ツール内で最上位のアプリケーション バーの PowerShell のアイコンをクリックします。 関心のあるコマンドを対応する PowerShell スクリプトへの移動にドロップダウン リストから選択します。

![](../media/launch/showscript.png)