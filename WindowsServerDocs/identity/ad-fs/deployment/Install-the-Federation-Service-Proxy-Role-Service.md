---
ms.assetid: c50ecc6a-9504-4b4a-816f-e762dcf3a95e
title: フェデレーション サービス プロキシ役割サービスをインストールする
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8d2ff177c821baf31bb5453b7c50e3eadca2aab7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855385"
---
# <a name="install-the-federation-service-proxy-role-service"></a>フェデレーション サービス プロキシ役割サービスをインストールする

前提条件のアプリケーションと証明書を使用してコンピューターを構成した後、Active Directory フェデレーションサービス (AD FS) \(AD FS\)のフェデレーションサービスプロキシの役割サービスをインストールすることができます。 フェデレーションサービスプロキシの役割サービスをインストールするには、次の手順を実行します。 コンピューターにフェデレーションサービスプロキシの役割サービスをインストールすると、そのコンピューターがフェデレーションサーバープロキシになります。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-install-the-federation-service-proxy-role-service-using-the-server-manager"></a>サーバーマネージャーを使用してフェデレーションサービスプロキシの役割サービスをインストールするには
  
1.  **スタート**画面で、「**サーバーマネージャー**」と入力し、enter キーを押します。  
  
2.  **[管理]** をクリックし、次に **[役割と機能の追加]** をクリックして、役割と機能の追加ウィザードを起動します。  
  
3.  **[開始する前に]** ページで、 **[次へ]** をクリックします。  
  
4.  **[インストールの種類の選択]** ページで、[**役割\-ベース] または [機能\-ベースのインストール**] をクリックし、 **[次へ]** をクリックします。  
  
5.  **[宛先サーバーの選択]** ページで、 **[サーバー プールからサーバーを選択]** をクリックし、ターゲット コンピューターが選択されていることを確認して、 **[次へ]** をクリックします。  
  
6.  **サーバーの役割の選択** ページで、**リモートアクセス** をクリックし、次へ をクリックします。  
  
    > [!NOTE]  
    > .NET Framework または Windows プロセス アクティブ化サービスの追加機能をインストールするよう求められたら、 **[機能の追加]** をクリックしてそれらをインストールします。  
  
7. **[役割サービスの選択]** ページで、 **[フェデレーション サービス プロキシ]** チェック ボックスをオンにして **[次へ]** をクリックします。  

8. **[インストール オプションの確認]** ページの情報を確認し、 **[必要に応じて対象サーバーを自動的に再起動する]** チェック ボックスをオンにして、 **[インストール]** をクリックします。  
  
13. **[インストールの進行状況]** ページで、すべてが正常にインストールされたことを確認し、 **[閉じる]** をクリックします。  

### <a name="to-install-the-federation-service-proxy-role-service-using-powershell"></a>PowerShell を使用してフェデレーションサービスプロキシの役割サービスをインストールするには

1. Windows PowerShell を開く (管理者として実行)

2. 次のコマンドを入力し、 **enter キーを**押します。

        Install-WindowsFeature Web-Application-Proxy -IncludeManagementTools



  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

