---
ms.assetid: c50ecc6a-9504-4b4a-816f-e762dcf3a95e
title: フェデレーション サービス プロキシ役割サービスをインストールする
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1f66e863c28aea7c9214c8363328a103b0a92f06
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359570"
---
# <a name="install-the-federation-service-proxy-role-service"></a>フェデレーション サービス プロキシ役割サービスをインストールする

前提条件のアプリケーションと証明書を使用してコンピューターを構成した後、Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 のフェデレーションサービスプロキシの役割サービスをインストールする準備が整いました。 フェデレーションサービスプロキシの役割サービスをインストールするには、次の手順を実行します。 コンピューターにフェデレーションサービスプロキシの役割サービスをインストールすると、そのコンピューターがフェデレーションサーバープロキシになります。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-install-the-federation-service-proxy-role-service-using-the-server-manager"></a>サーバーマネージャーを使用してフェデレーションサービスプロキシの役割サービスをインストールするには
  
1.  **スタート**画面で、「**サーバーマネージャー**」と入力し、enter キーを押します。  
  
2.  **[管理]** をクリックし、 **[役割と機能の追加]** をクリックして、役割と機能の追加ウィザードを開始します。  
  
3.  **[開始する前に]** ページで、 **[次へ]** をクリックします。  
  
4.  **[インストールの種類の選択]** ページで、[**ロール @ no__t-2based] または [機能 @ no__t ベースのインストール**] をクリックし、 **[次へ]** をクリックします。  
  
5.  **[対象サーバーの選択]** ページで、 **[サーバープールからサーバーを選択]** をクリックし、対象のコンピューターが強調表示されていることを確認して、 **[次へ]** をクリックします。  
  
6.  **サーバーの役割の選択** ページで、**リモートアクセス** をクリックし、次へ をクリックします。  
  
    > [!NOTE]  
    > 追加の .NET Framework または Windows プロセスアクティブ化サービスの機能をインストールするように求めるメッセージが表示されたら、 **[機能の追加]** をクリックしてインストールします。  
  
7. **[役割サービスの選択]** ページで、 **[フェデレーションサービスプロキシ]** チェックボックスをオンにし、 **[次へ]** をクリックします。  

8. **[インストール オプションの確認]** ページの情報を確認し、 **[必要に応じて対象サーバーを自動的に再起動する]** チェック ボックスをオンにして、 **[インストール]** をクリックします。  
  
13. **[インストールの進行状況]** ページで、すべてが正常にインストールされたことを確認し、 **[閉じる]** をクリックします。  

### <a name="to-install-the-federation-service-proxy-role-service-using-powershell"></a>PowerShell を使用してフェデレーションサービスプロキシの役割サービスをインストールするには

1. Windows PowerShell を開く (管理者として実行)

2. 次のコマンドを入力し、 **enter キーを**押します。

        Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools



  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

