---
title: AD FS 2.0 フェデレーション サーバーを Windows Server 2012 R2 で AD FS に移行を準備します。
description: Windows Server 2012 R2 に AD FS サーバーの移行の準備について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4d0ff53b9118db1dd6ba5af94b3e627bf1597e0c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889023"
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>AD FS 2.0 フェデレーション サーバーを Windows Server 2012 R2 で AD FS に移行を準備します。

このドキュメントでは、Windows Server 2012 R2 AD FS ファーム、AD FS 2.0 または Windows Server 2012 のフェデレーション サーバー ファームを移行する方法について説明します。  手順は、基になるデータベースとして WID または SQL Server のいずれかを使用して AD FS ファームで使用できます。  
  
-   [移行プロセスの概要](prepare-migrate-ad-fs-server-r2.md#migrate-process-outline)  
  
-   [Windows Server 2012 R2 AD FS の新機能](prepare-migrate-ad-fs-server-r2.md#new-ad-fs-functionality-in-windows-server-2012-r2)  
  
-   [Windows Server 2012 R2 で AD FS の要件](prepare-migrate-ad-fs-server-r2.md#ad-fs-requirements-in-windows-server-2012-r2)  
  
-   [Windows PowerShell の制限を増やす](prepare-migrate-ad-fs-server-r2.md#increasing-your-windows-powershell-limits)  
  
-   [その他の移行タスクおよび考慮事項](prepare-migrate-ad-fs-server-r2.md#other-migration-tasks-and-considerations)  
  
##  <a name="migration-process-outline"></a>移行プロセスの概要  
 AD FS フェデレーション サーバー ファームから Windows Server 2012 R2 への移行を完了するには、ここで示しているタスクを完了する必要があります。  
  
1.  既存の AD FS ファームで以下の構成データをエクスポート、記録、バックアップします。 これらのタスクの完了方法の詳細については、「[AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)」を参照してください。  
  
次の設定は、Windows Server 2012 R2 のインストール CD の \support\adfs フォルダーにあるスクリプトを使用に移行されます。  
  
-   要求プロバイダー信頼。ただし、Active Directory 要求プロバイダー信頼のカスタム要求規則は除きます。 詳細については、「[AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)」を参照してください。  
  
-   証明書利用者信頼。  
  
-   AD FS 内部で生成された自己署名トークン署名証明書とトークン暗号化解除証明書。  
  
次のカスタム設定はすべて手動で移行する必要があります。  
  
 -   サービスの設定:  
  
     -   企業やパブリック証明機関から発行された既定以外のトークン署名証明書とトークン暗号化解除証明書。  
  
     -   AD FS によって使用される SSL サーバー認証証明書。  
  
     -   AD FS によって使用されるサービス通信証明書 (既定では SSL 証明書と同じ証明書)。  
  
      -   任意のフェデレーション サービス プロパティの既定以外の値 (AutoCertificateRollover や SSO 有効期間など)。  
  
      -   既定以外の AD FS エンドポイントの設定と要求記述します。  
  
-   Active Directory 要求プロバイダー信頼のカスタム要求規則。  
  
    -   AD FS サインイン ページのカスタマイズ内容。  
  
詳細については、「[AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)」を参照してください。  
  
2.  Windows Server 2012 R2 フェデレーション サーバー ファームを作成します。  
  
3.  元の構成データをこの新しい Windows Server 2012 R2 AD FS ファームにインポートします。  
  
4.  AD FS サインイン ページを構成およびカスタマイズします。  
  
##  <a name="new-ad-fs-functionality-in-windows-server-2012-r2"></a>Windows Server 2012 R2 の AD FS の新機能  
 次の AD FS 機能 Windows Server 2012 R2 への影響で、移行から変更 AD FS 2.0 または Windows Server 2012 で AD FS:  
  
**IIS の依存関係**  
   - Windows Server 2012 R2 の AD FS は自己ホスト型になり、IIS のインストールは不要になりました。 この変更の結果として次の点に注意してください。  
   -   AD FS ファーム内のフェデレーション サーバーとプロキシ コンピューターの両方の SSL 証明書は、Windows PowerShell を使用して管理する必要があります。  
  
**AD FS サインイン ページの設定とカスタマイズの変更**  
-   Windows Server 2012 R2 で AD FS で管理者とユーザーのサインイン エクスペリエンスを向上させるためのいくつかの変更があります。 AD FS の以前のバージョンにあった IIS ホスト型の Web ページは削除されました。 AD FS サインイン Web ページのルック アンド フィールは AD FS での自己ホスト型になり、ユーザー エクスペリエンスに合わせてカスタマイズできるようになりました。 それらの変更を次に示します。  
    -   AD FS のサインイン エクスペリエンスのカスタマイズ (会社名、ロゴ、イラスト、サインインの説明などのカスタマイズ)  
    -   エラー メッセージのカスタマイズ  
    -   ADFS のホーム領域の検出エクスペリエンスのカスタマイズ  
        -   特定の電子メール サフィックスを使用するための ID プロバイダーの構成  
        -   証明書利用者ごとの ID プロバイダーの一覧の構成  
        -   イントラネットのホーム領域の検出のバイパス  
        -   カスタム Web テーマの作成  
  
AD FS サインイン ページのルック アンド フィールを構成する詳細については、次を参照してください。 [AD FS サインイン ページのカスタマイズ](../operations/AD-FS-Customization-in-Windows-Server-2016.md)します。  
  
Windows Server 2012 R2 に移行したい既存の AD FS ファームに web ページのカスタマイズがあれば、Windows Server 2012 R2 で新しいカスタマイズ機能を使用して、移行プロセスの一部としてを再作成できます。  
  
-   **その他の変更**  
  
    -   Windows Server 2012 R2 で AD FS は、Windows Identity Foundation (WIF) 3.5 では、WIF 4.5 ではないに基づいています。 したがって、WIF 4.5 (Kerberos 要求やダイナミック アクセス制御など) の一部の機能は、Windows Server 2012 R2 で AD FS ではサポートされません。  
  
    -   Windows Server 2012 R2 でデバイス登録サービス (DRS) はポート 443 で動作します。ユーザー証明書認証用の ClientTLS はポート 49443 で動作します。  
  
        -   ブラウザー以外のアクティブ クライアントで、ポート 443 を参照するように特別にハードコードされている証明書トランスポート モード認証を使用する場合、ユーザー証明書認証をポート 49443 で使用し続けるには、そのコードの変更が必要です。  
  
        -   パッシブ アプリケーションの場合、変更は不要です。AD FS によりユーザー証明書認証が適切なポートにリダイレクトされるためです。  
  
        -   クライアントとプロキシとの間のファイアウォール ポートでは、ユーザー証明書認証のトラフィックがポート 49443 を通過できるようにする必要があります。  
  
##  <a name="ad-fs-requirements-in-windows-server-2012-r2"></a>Windows Server 2012 R2 の AD FS の要件  
 Windows Server 2012 R2 に AD FS ファームを適切に移行するには、するには、次の要件を満たす必要があります。  
  
 AD fs が機能する、フェデレーションする各コンピューターをドメインに参加する必要があります。  
  
 関数には、Windows Server 2012 R2 で実行されている AD fs では、Active Directory ドメインは、次のいずれかを実行する必要があります。  
  
-   Windows Server 2012 R2  
  
-   Windows Server 2012  
  
-   Windows Server 2008 R2  
  
-   Windows Server 2008  
  
 AD FS のサービス アカウントとしてグループ管理サービス アカウント (gMSA) を使用する場合は、Windows Server 2012 または Windows Server 2012 R2 のオペレーティング システムで実行されている環境で少なくとも 1 つのドメイン コント ローラーが必要です。  
  
 AD ワークプ レース ジョイン用に AD FS 展開の一部としてデバイス登録サービス (DRS) をデプロイする場合は、AD DS スキーマを Windows Server 2012 R2 のレベルを更新する必要があります。 スキーマを更新するには 3 種類の方法があります。  
  
1.  既存の Active Directory フォレスト内には、2008 またはそれ以降、Windows Server を実行する任意の 64 ビット サーバーで Windows Server 2012 R2 オペレーティング システム DVD の \support\adprep フォルダーから adprep/forestprep を実行します。 この場合は、追加のドメイン コントローラーをインストールする必要はなく、既存のドメイン コントローラーのアップグレードも必要ありません。  
  
adprep/forestprep を実行するには、Schema Admins グループ、Enterprise Admins グループ、およびスキーマ マスターをホストするドメインの Domain Admins グループのメンバーである必要があります。  
  
2.  既存の Active Directory フォレストでは、Windows Server 2012 R2 を実行するドメイン コント ローラーをインストールします。 この場合は、adprep/forestprep がドメイン コント ローラーのインストールの一部として自動的に実行されます。  
  
ドメイン コントローラーのインストール時に、adprep /forestprep を実行するための追加の資格情報の入力が必要になる場合があります。  
  
3.  新しい Active Directory フォレストを作成するには、Windows Server 2012 R2 を実行しているサーバーに AD DS をインストールします。 この場合は、adprep/forestprep がスキーマは最初にすべての必要なコンテナーと DRS をサポートするためにオブジェクトを作成するために実行する必要はありません。  
  
### <a name="sql-server-support-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2 の AD FS のための SQL Server のサポート  
 AD FS ファームを作成し、SQL Server を使用して構成データを保存する場合は、SQL Server 2012 など、SQL Server 2008 以降のバージョンを使用できます。  
  
##  <a name="increasing-your-windows-powershell-limits"></a>Windows PowerShell の制限の増加  
 AD FS ファームに 1,000 以上の要求プロバイダー信頼と証明書利用者信頼がある場合、または AD FS の移行エクスポート/インポート ツールを実行しようとして次のエラーが表示された場合は、Windows PowerShell の制限を増やす必要があります。  
  
```  
'Exception of type 'System.OutOfMemoryException' was thrown. At E:\dev\ds\security\ADFSv2\Product\Migration\Export-FederationConfiguration.ps1:176 char:21 + $configData = Invoke-Command -ScriptBlock $GetConfig -Argume ...  
```  
  
 Windows PowerShell セッションの既定のメモリの制限が少なすぎるため、このエラーがスローされます。 Windows PowerShell 2.0 では、セッションの既定のメモリは 150 MB です。 Windows PowerShell 3.0 では、セッションの既定のメモリは 1,024 MB です。 Windows PowerShell リモート セッションのメモリの制限を確認には、`Get-Item wsman:localhost\Shell\MaxMemoryPerShellMB` コマンドを使用します。 制限を増やすには、`Set-Item wsman:localhost\Shell\MaxMemoryPerShellMB 512` コマンドを実行します。  
  
## <a name="other-migration-tasks-and-considerations"></a>その他の移行作業と考慮事項  
 レガシ AD FS ファームを Windows Server 2012 R2 に移行するには、次のことに注意してください。  
  
-   Windows Server 2012 R2 のインストール CD の \support\adfs フォルダーにある移行スクリプトでは、同じフェデレーション サーバー ファーム名および Windows に移行するときに、レガシ AD FS ファームで使用したサービス アカウント識別名を保持することが必要です。Server 2012 R2。  
  
-   SQL Server の AD FS ファームを移行する場合は、移行プロセスに新しい SQL データベース インスタンスの作成が含まれ、そのインスタンスに元の構成データをインポートする必要があることに注意してください。  
  
## <a name="next-steps"></a>次の手順
 [Windows Server 2012 R2 への Active Directory フェデレーション サービス役割サービスを移行します。](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)   
 [AD FS フェデレーション サーバー プロキシの移行](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 R2 への AD FS の移行の検証](verify-ad-fs-migration.md)