---
title: Windows Server 2008/2008 R2 に特化されたイメージの Azure へのアップロード
description: Windows Server 2008 と Windows Server 2008 R2 は、サービス終了が近づいています。 クラウド内で Windows Server をホストすることで Azure に移行する方法について説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: mikeblodge
ms.author: mikeblodge
ms.date: 07/11/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.localizationpriority: high
ms.openlocfilehash: af98a219a4a5aa708df9c648f1b245a21e95f016
ms.sourcegitcommit: f7113ccc8b664494f664cd4b100dcac06eef5654
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "7012076"
---
# Windows Server 2008/2008 R2 に特化されたイメージの Azure へのアップロード 

![WS08 イメージ トピックを導入するバナー](media/WS08-image-banner-large.png)

Azure によりクラウド内で Windows Server 2008/2008 R2 VM を実行できるようになりました。 

## Windows Server 2008/2008 R2 に特化されたイメージの準備
画像をアップロードする前に、次の変更を行います。

- Windows Server 2008 Service Pack 2 (SP2) をイメージにまだインストールしていない場合は、ダウンロードしてインストールします。

- リモート デスクトップ (RDP) の設定を構成します。
   1. **[コントロール パネル]** > **[システム設定]** の順に移動します。   
   2. 左側のメニューで、**[リモートの設定]** を選択します。

   ![[リモートの設定] を強調表示したシステム設定のスクリーンショット。](media/1a_remote_settings.png)

   3. [システムのプロパティ] で **[リモート]** タブを選択します。   

   ![[システムのプロパティ] の [リモート] タブのスクリーンショット。](media/2c_sysprops.png)

   4. [リモート デスクトップを実行しているコンピュータからの接続を許可する (セキュリティのレベルは低くなります)] を選択します。   
   5. **[適用]**、**[OK]** をクリックします。
- Windows ファイアウォールの設定を構成します。   
   1. 管理モードのコマンド プロンプトで、「**wf.msc**」と入力して Windows ファイアウォールとセキュリティの詳細設定を表示します。   
   2. 検出結果を **[ポート]** で並べ替え、**[ポート 3389]** を選択します。   
     ![Windows ファイアウォール設定の受信ルールのスクリーンショット。](media/3b_inboundrules.png)   
   3. **[ドメイン]**、**[プライベート]**、**[パブリック]** (上記を参照) のプロパティについてリモート デスクトップ (TCP-IN) を有効にします。

- すべての設定を保存して、イメージをシャットダウンします。   
- Hyper-V を使用している場合は、変更を維持するために子 AVHD が親 VHD にマージされていることを確認します。

現在の既知のバグでは、アップロードしたイメージで管理者パスワードが 24 時間以内に期限切れになります。 この問題を回避するには、次の手順に従います。 

1. **[スタート]** > **[ファイル名を指定して実行]** の順に移動します。
2. 「**lusrmgr.msc**」と入力します。
3. [ローカル ユーザーとグループ] で **[ユーザー]** を選択します
4. **[管理者]** を右クリックし、**[プロパティ]** を選択します
5. **[パスワードを無期限にする]** を選択し、**[OK]** を選択します
![管理者プロパティのスクリーンショット。](media/6_adminprops.png)

## イメージ VHD のアップロード
以下のスクリプトを使用して、VHD をアップロードできます。 これを行う前に、Azure アカウントの公開設定ファイルが必要になります。 [Azure ファイル設定](https://azure.microsoft.com/downloads/)を取得します。

スクリプトは次のとおりです。

```powershell
Get-AzurePublishSettingsFile 

Login-AzureRmAccount
 
      # Import publishsettings
      Import-AzurePublishSettingsFile -PublishSettingsFile <LocationOfPublishingFile>
      $subscriptionId = 'xxxx-xxxx-xxxx-xxxx-xxxxx'
 
      # Set NodeFlight subscription as default subscription
      Select-AzureRmSubscription -SubscriptionId $subscriptionId
      Set-AzureRmContext -SubscriptionId $subscriptionId
      $rgName = "<resourcegroupname>"
    
      $urlOfUploadedImageVhd = "<BlobUrl>/<NameForVHD>.vhd"
      Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd -LocalFilePath "<FilePath>"  
```
## Azure でのイメージの展開
このセクションでは、Azure でイメージ VHD を展開します。 

> [!IMPORTANT]
> Azure で定義済みのユーザー イメージを使用しないでください。

1.  新しい[リソース グループ](https://docs.microsoft.com/rest/api/resources/resourcegroups/createorupdate)を作成します。 
2.  リソース グループ内に新しい[ストレージ BLOB](https://docs.microsoft.com/rest/api/storageservices/put-blob) を作成します。
3.  ストレージ BLOB 内に[コンテナー](https://docs.microsoft.com/rest/api/storageservices/create-container)を作成します。
4.  プロパティから BLOB ストレージの URL をコピーします。
5.  上で指定されたスクリプトを使用して新しいストレージ BLOB にイメージをアップロードします。
6.  VHD の[ディスク](https://docs.microsoft.com/azure/virtual-machines/windows/prepare-for-upload-vhd-image)を作成します。   
     a. [ディスク] に移動し、**[追加]** をクリックします。  
     b. ディスクの名前を入力します。 使用するサブスクリプションを選択し、地域を設定して、アカウントの種類を選択します。   
     c. [ソースの種類] で、ストレージを選択します。 スクリプトを使用して作成した BLOB VHD の場所を参照します。  
     d. Windows OS の種類とサイズを選択します (既定: 1023)。   
     e. **[作成]** をクリックします。   

7.  [Disk Created] (作成されたディスク) に移動し、**[VM の作成]** をクリックします。   
     a. VM に名前を付けます。   
     b. ディスクをアップロードした 手順 5 で作成した既存のグループを選択します。   
     c. VM のサイズと SKU 計画を選びます。   
     d. 設定ページで、ネットワーク インターフェイスを選択します。 ネットワーク インターフェイスに次の規則が指定されていることを確認します。
 
        PORT:3389 Protocol: TCP Action: Allow Priority: 1000 Name: ‘RDP-Rule’.   
     e. **[作成]** をクリックします。




