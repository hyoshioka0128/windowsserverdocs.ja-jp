---
title: "Windows Server 2012 R2 での AD FS への AD FS 2.0 フェデレーション サーバーの移行を準備します。"
description: "Windows Server 2012 R2 への AD FS サーバーの移行の準備について説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4d0ff53b9118db1dd6ba5af94b3e627bf1597e0c
ms.sourcegitcommit: 03ce78a1624dbd7f4e6abf2ec1ef185b55de29a1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2017
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Windows Server 2012 R2 での AD FS への AD FS 2.0 フェデレーション サーバーの移行を準備します。

このドキュメントでは、Windows Server 2012 R2 AD FS ファームに、AD FS 2.0 または Windows Server 2012 のフェデレーション サーバー ファームを移行する方法について説明します。  手順は、基になるデータベースとして WID または SQL Server のいずれかを使用している AD FS ファームで使用できます。  
  
-   [移行プロセスの概要](prepare-migrate-ad-fs-server-r2.md#migrate-process-outline)  
  
-   [Windows Server 2012 R2 で新しい AD FS 機能](prepare-migrate-ad-fs-server-r2.md#new-ad-fs-functionality-in-windows-server-2012-r2)  
  
-   [Windows Server 2012 R2 で AD FS の要件](prepare-migrate-ad-fs-server-r2.md#ad-fs-requirements-in-windows-server-2012-r2)  
  
-   [Windows PowerShell の制限を増やす](prepare-migrate-ad-fs-server-r2.md#increasing-your-windows-powershell-limits)  
  
-   [その他の移行作業と考慮事項](prepare-migrate-ad-fs-server-r2.md#other-migration-tasks-and-considerations)  
  
##  <a name="migration-process-outline"></a>移行プロセスの概要  
 Windows Server 2012 R2 には、AD FS フェデレーション サーバー ファームの移行を完了するには、次のタスクを行う必要があります。  
  
1.  エクスポート、記録、し、既存の AD FS ファーム内の次の構成データをバックアップします。 これらのタスクを完了する方法の詳細については、次を参照してください。[AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)します。  
  
Windows Server 2012 R2 のインストール CD の \support\adfs フォルダーにあるスクリプトで、次の設定が移行されます。  
  
-   Active Directory 要求プロバイダー信頼のカスタム要求規則を除いて、プロバイダーの信頼関係を要求します。 詳細については、次を参照してください。[AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)します。  
  
-   証明書利用者の信頼します。  
  
-   内部生成された AD FS 自己署名トークン署名やトークン暗号化解除証明書。  
  
次のカスタム設定のいずれかを手動で移行する必要があります。  
  
 -   サービスの設定。  
  
     -   既定以外のトークンの署名と企業やパブリック証明機関から発行されたトークン暗号化解除証明書。  
  
     -   SSL サーバー認証証明書 AD FS によって使用されます。  
  
     -   AD FS によって使用されるサービス通信証明書 (既定では、これは、SSL 証明書と同じ証明書です。  
  
      -   AutoCertificateRollover や SSO 有効期間など、フェデレーション サービスのプロパティの既定以外の値。  
  
      -   既定以外の AD FS エンドポイントの設定と要求記述します。  
  
-   カスタム要求規則は Active Directory 要求プロバイダー信頼します。  
  
    -   AD FS サインイン ページのカスタマイズ  
  
詳細については、次を参照してください。[AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)します。  
  
2.  Windows Server 2012 R2 フェデレーション サーバー ファームを作成します。  
  
3.  この新しい Windows Server 2012 R2 AD FS ファームに元の構成データをインポートします。  
  
4.  構成して、AD FS サインイン ページをカスタマイズします。  
  
##  <a name="new-ad-fs-functionality-in-windows-server-2012-r2"></a>Windows Server 2012 R2 で新しい AD FS 機能  
 次の AD FS 機能では、Windows Server 2012 R2 への影響、移行から変更 AD FS 2.0 または Windows Server 2012 で AD FS します。  
  
**IIS の依存関係**  
   - Windows Server 2012 R2 の AD FS は自己ホスト型し、IIS のインストールは不要です。 この変更の結果として、次をメモしたことを確認します。  
   -   Windows PowerShell を使用して、フェデレーション サーバーと、AD FS ファーム内のコンピューターのプロキシの両方の SSL 証明書の管理を実行できるようになりました必要があります。  
  
**AD FS サインイン ページの設定とカスタマイズの変更**  
-   Windows Server 2012 R2 で AD FS では、管理者とユーザーのサインイン エクスペリエンスを向上させるためのいくつかの変更があります。 AD FS の以前のバージョンにあった IIS ホスト型 Web ページは削除されました。 AD FS サインイン Web ページのルック アンド フィールは AD FS でホストされる自己およびに、ユーザー エクスペリエンスをカスタマイズするカスタマイズできるようになりました。 変更は次のとおりです。  
    -   AD FS サインイン エクスペリエンス、会社名、ロゴ、図、およびサインインの説明のカスタマイズを含むをカスタマイズします。  
    -   エラー メッセージをカスタマイズします。  
    -   ADFS のホーム領域検出エクスペリエンスのカスタマイズ、これを次に示します。  
        -   特定の電子メール サフィックスを使用する ID プロバイダーの構成。  
        -   証明書利用者ごとの ID プロバイダーの一覧を構成するパーティします。  
        -   イントラネットのホーム領域検出をバイパスできるようにします。  
        -   カスタム Web テーマを作成します。  
  
AD FS サインイン ページのルック アンド フィールの構成の詳細な手順については、次を参照してください。[AD FS サインイン ページのカスタマイズ](../operations/AD-FS-Customization-in-Windows-Server-2016.md)します。  
  
Windows Server 2012 R2 へ移行する場合、既存の AD FS ファームに Web ページのカスタマイズがあれば、Windows Server 2012 R2 の新しいカスタマイズ機能を使用して、移行プロセスの一部としてそのを作成し直すことができます。  
  
-   **その他の変更**  
  
    -   Windows Server 2012 R2 の AD FS は、[Windows Identity Foundation (WIF) 3.5 では、WIF 4.5 ではないに基づいています。 したがって、WIF 4.5 (Kerberos 要求やダイナミック アクセス制御など) の一部の機能は、Windows Server 2012 R2 で AD FS ではサポートされません。  
  
    -   Windows Server 2012 R2 でデバイス登録サービス (DRS) は、ポート 443 で動作します。用ユーザー証明書認証の ClientTLS はポート 49443 で動作します。  
  
        -   ブラウザー以外のアクティブなクライアントの証明書トランスポート モード認証を使用して具体的には、ハードコードされたポート 443、] をポイントするコードの変更が必要をポート 49443 でユーザー証明書認証を使用して引き続きです。  
  
        -   パッシブ アプリケーションの変更は必要ありませんので、AD FS がユーザー証明書認証用の正しいポートにリダイレクトします。  
  
        -   クライアントとプロキシの間のファイアウォールのポートは、ユーザー証明書認証を通過するポート 49443 のトラフィックを有効にする必要があります。  
  
##  <a name="ad-fs-requirements-in-windows-server-2012-r2"></a>Windows Server 2012 R2 で AD FS の要件  
 Windows Server 2012 R2 への AD FS ファームを移行する、するために、次の要件を満たす必要があります。  
  
 関数に、AD FS のフェデレーションにする各コンピューターをドメインに参加する必要があります。  
  
 関数には、Windows Server 2012 R2 で実行されている、AD FS の次のいずれかの Active Directory ドメインが実行する必要があります。  
  
-   Windows Server 2012 R2  
  
-   Windows Server 2012  
  
-   Windows Server 2008 R2  
  
-   Windows Server 2008  
  
 AD FS のサービス アカウントとしてグループの管理されたサービス アカウント (gMSA) を使用する場合は、Windows Server 2012 または Windows Server 2012 R2 のオペレーティング システムで実行されている環境で、少なくとも 1 つのドメイン コントローラーが必要です。  
  
 AD ワークプ レース ジョイン用の AD FS 展開の一部としてデバイス登録サービス (DRS) を展開する場合は、AD DS スキーマを Windows Server 2012 R2 のレベルを更新する必要があります。 スキーマの更新に次の 3 つの方法はあります。  
  
1.  既存の Active Directory フォレスト内には、adprep を実行 /forestprep 2008 またはそれ以降は、Windows Server を実行している任意の 64 ビット サーバー上の Windows Server 2012 R2 オペレーティング システム DVD の \support\adprep フォルダーからです。 ここでは、追加のドメイン コントローラーをインストールする必要はありませんし、既存のドメイン コントローラーをアップグレードする必要はありません。  
  
Adprep/forestprep を実行するには、Schema Admins グループ、Enterprise Admins グループ、およびスキーマ マスターをホストするドメインの Domain Admins グループのメンバーがあります。  
  
2.  既存の Active Directory フォレスト内には、Windows Server 2012 R2 を実行するドメイン コントローラーをインストールします。 この場合、adprep /forestprep ドメイン コントローラーのインストールの一部として自動的に実行します。  
  
ドメイン コントローラーのインストール中には、adprep を実行するために追加の資格情報を指定する必要があります /forestprep します。  
  
3.  Windows Server 2012 R2 を実行しているサーバーに AD DS をインストールして、新しい Active Directory フォレストを作成します。 この場合、adprep /forestprep のすべての必要なコンテナーおよびオブジェクト DRS のサポートを使用、スキーマが最初に作成するために実行する必要はありません。  
  
### <a name="sql-server-support-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2 の AD FS での SQL Server のサポート  
 AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012 などの新しいバージョンを使用することができます。  
  
##  <a name="increasing-your-windows-powershell-limits"></a>Windows PowerShell の制限を増やす  
 1,000 以上の要求プロバイダー信頼がある場合と、AD FS ファーム内の証明書利用者の信頼または AD FS の移行エクスポート/インポート ツールを実行しているときに、次のエラーが表示された場合は、Windows PowerShell の制限を増やす必要があります。  
  
```  
'Exception of type 'System.OutOfMemoryException' was thrown. At E:\dev\ds\security\ADFSv2\Product\Migration\Export-FederationConfiguration.ps1:176 char:21 + $configData = Invoke-Command -ScriptBlock $GetConfig -Argume ...  
```  
  
 Windows PowerShell セッションの既定のメモリ制限が少なすぎるために、このエラーがスローされます。 Windows PowerShell 2.0 では、セッションの既定のメモリは 150 MB です。 Windows PowerShell 3.0 では、セッションの既定のメモリには 1024 MB です。 次のコマンドを使用して Windows PowerShell リモート セッションのメモリ制限を確認することができます:`Get-Item wsman:localhost\Shell\MaxMemoryPerShellMB`します。 次のコマンドを実行して、制限を増やすことができます:`Set-Item wsman:localhost\Shell\MaxMemoryPerShellMB 512`します。  
  
## <a name="other-migration-tasks-and-considerations"></a>その他の移行作業と考慮事項  
 Windows Server 2012 R2 への AD FS ファームを移行する、するために、次の把握するになっていることを確認します。  
  
-   Windows Server 2012 R2 のインストール CD の \support\adfs フォルダーにある移行スクリプトは、同じフェデレーション サーバー ファーム名と Windows Server 2012 R2 に移行する場合に、レガシ AD FS ファームで使用しているサービス アカウント識別名を保持する必要があります。  
  
-   SQL Server の AD FS ファームを移行する場合は、移行プロセスが元の構成データをインポートする必要があります、新しい SQL データベース インスタンスを作成するには注意してください。  
  
## <a name="next-steps"></a>次の手順
 [Windows Server 2012 R2 への Active Directory フェデレーション サービスの役割サービスを移行します。](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)   
 [AD FS フェデレーション サーバー プロキシの移行](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 R2 への AD FS の移行の検証](verify-ad-fs-migration.md)