---
ms.assetid: c50ecc6a-9504-4b4a-816f-e762dcf3a95e
title: フェデレーション サービス プロキシ役割サービスをインストールする
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ed66800aa6bbfdf85816a992ee8eb39799efebb6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865233"
---
# <a name="install-the-federation-service-proxy-role-service"></a>フェデレーション サービス プロキシ役割サービスをインストールする

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービスのフェデレーション サービス プロキシ役割サービスをインストールする準備が整ったら、前提条件のアプリケーションと証明書とコンピューターを構成した後\(AD FS\)します。 次の手順を使用すると、フェデレーション サービス プロキシ役割サービスをインストールします。 コンピューターで、フェデレーション サービス プロキシ役割サービスをインストールするときにそのコンピューターは、フェデレーション サーバー プロキシになります。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-install-the-federation-service-proxy-role-service-using-the-server-manager"></a>サーバー マネージャーを使用して、フェデレーション サービス プロキシ役割サービスをインストールするには
  
1.  **開始**画面で「**サーバー マネージャー**し、ENTER キーを押します。  
  
2.  をクリックして**管理**、順にクリックします**追加の役割と機能の**役割の追加と機能ウィザードを起動します。  
  
3.  **[開始する前に]** ページで、 **[次へ]** をクリックします。  
  
4.  **インストールの種類を選択します** ページで **ロール\-ベースまたは機能\-ベースのインストール**、 をクリック**次**。  
  
5.  **対象サーバーの選択**] ページで [**サーバー プールからサーバーを選択**、対象のコンピュータが強調表示されていることを確認順にクリックします**次**。  
  
6.  **サーバーの役割の選択**] ページで [**リモート アクセス**、し、[次へ] をクリックするとします。  
  
    > [!NOTE]  
    > .NET Framework または Windows プロセス アクティブ化サービスの追加機能をインストールするメッセージが表示されたら、クリックして**機能の追加**それらをインストールします。  
  
7. **役割サービスの選択**ページで、選択、**フェデレーション サービス プロキシ**チェック ボックスをオンにして **[次へ]** します。  

8. **[インストール オプションの確認]** ページの情報を確認し、 **[必要に応じて対象サーバーを自動的に再起動する]** チェック ボックスをオンにして、 **[インストール]** をクリックします。  
  
13. **[インストールの進行状況]** ページで、すべてが正常にインストールされたことを確認し、**[閉じる]** をクリックします。  

### <a name="to-install-the-federation-service-proxy-role-service-using-powershell"></a>PowerShell を使用して、フェデレーション サービス プロキシ役割サービスをインストールするには

1. Windows PowerShell (管理者として実行) を開きます

2. 次のコマンドとキーを押して入力**Enter**:

        Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools



  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーを設定します。](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト:フェデレーション サーバー プロキシを設定します。](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

