---
title: Windows Server 2012 R2 で AD FS に AD FS 2.0 フェデレーションサーバーを移行する準備をする
description: AD FS サーバーを Windows Server 2012 R2 に移行するための準備について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 149e3d3fc4d4eee22fa9330475f0eed9d945f8b9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359311"
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Windows Server 2012 R2 で AD FS に AD FS 2.0 フェデレーションサーバーを移行する準備をする

このドキュメントでは、AD FS 2.0 または Windows Server 2012 のフェデレーションサーバーファームを Windows Server 2012 R2 AD FS ファームに移行する方法について説明します。  これらの手順は、基になるデータベースとして WID または SQL Server を使用する AD FS ファームで使用できます。  
  
-   [移行プロセスの概要](prepare-migrate-ad-fs-server-r2.md#migration-process-outline)  
  
-   [Windows Server 2012 R2 の新しい AD FS 機能](prepare-migrate-ad-fs-server-r2.md#new-ad-fs-functionality-in-windows-server-2012-r2)  
  
-   [Windows Server 2012 R2 での AD FS の要件](prepare-migrate-ad-fs-server-r2.md#ad-fs-requirements-in-windows-server-2012-r2)  
  
-   [Windows PowerShell の制限を増やす](prepare-migrate-ad-fs-server-r2.md#increasing-your-windows-powershell-limits)  
  
-   [その他の移行タスクと考慮事項](prepare-migrate-ad-fs-server-r2.md#other-migration-tasks-and-considerations)  
  
##  <a name="migration-process-outline"></a>移行プロセスの概要

 AD FS フェデレーション サーバー ファームから Windows Server 2012 R2 への移行を完了するには、ここで示しているタスクを完了する必要があります。  
  
1.  既存の AD FS ファームで以下の構成データをエクスポート、記録、バックアップします。 これらのタスクの完了方法の詳細については、「[AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)」を参照してください。  
  
次の設定は、Windows Server 2012 R2 のインストール CD の \support\adfs フォルダーにあるスクリプトと共に移行されます。  
  
-   要求プロバイダー信頼。ただし、Active Directory 要求プロバイダー信頼のカスタム要求規則は除きます。 詳細については、「[AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)」を参照してください。  
  
-   証明書利用者信頼。  
  
-   AD FS 内部で生成された自己署名トークン署名証明書とトークン暗号化解除証明書。  
  
次のカスタム設定はすべて手動で移行する必要があります。  
  
- サービスの設定:  
  
  - 企業やパブリック証明機関から発行された既定以外のトークン署名証明書とトークン暗号化解除証明書。  
  
  - AD FS によって使用される SSL サーバー認証証明書。  
  
  - AD FS によって使用されるサービス通信証明書 (既定では SSL 証明書と同じ証明書)。  
  
    -   任意のフェデレーション サービス プロパティの既定以外の値 (AutoCertificateRollover や SSO 有効期間など)。  
  
    -   既定以外の AD FS エンドポイント設定と要求の説明。  
  
-   Active Directory 要求プロバイダー信頼のカスタム要求規則。  
  
    -   AD FS サインイン ページのカスタマイズ内容。  
  
詳細については、「[AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)」を参照してください。  
  
2. Windows Server 2012 R2 フェデレーション サーバー ファームを作成します。  
  
3. 元の構成データをこの新しい Windows Server 2012 R2 AD FS ファームにインポートします。  
  
4. AD FS サインイン ページを構成およびカスタマイズします。  
  
##  <a name="new-ad-fs-functionality-in-windows-server-2012-r2"></a>Windows Server 2012 R2 の AD FS の新機能  
 Windows Server 2012 R2 の次の AD FS 機能の変更は、Windows Server 2012 の AD FS 2.0 または AD FS からの移行に影響します。  
  
**IIS の依存関係**  
   - Windows Server 2012 R2 の AD FS は自己ホスト型になり、IIS のインストールは不要になりました。 この変更の結果として次の点に注意してください。  
   -   AD FS ファーム内のフェデレーション サーバーとプロキシ コンピューターの両方の SSL 証明書は、Windows PowerShell を使用して管理する必要があります。  
  
**AD FS サインインページの設定とカスタマイズに対する変更**  
-   Windows Server 2012 R2 の AD FS では、管理者とユーザーの両方のサインインエクスペリエンスを向上させるためにいくつかの変更が加えられています。 AD FS の以前のバージョンにあった IIS ホスト型の Web ページは削除されました。 AD FS サインイン Web ページのルック アンド フィールは AD FS での自己ホスト型になり、ユーザー エクスペリエンスに合わせてカスタマイズできるようになりました。 それらの変更を次に示します。  
    -   AD FS のサインイン エクスペリエンスのカスタマイズ (会社名、ロゴ、イラスト、サインインの説明などのカスタマイズ)  
    -   エラー メッセージのカスタマイズ  
    -   ADFS のホーム領域の検出エクスペリエンスのカスタマイズ  
        -   特定の電子メール サフィックスを使用するための ID プロバイダーの構成  
        -   証明書利用者ごとの ID プロバイダーの一覧の構成  
        -   イントラネットのホーム領域の検出のバイパス  
        -   カスタム Web テーマの作成  
  
AD FS サインインページのルックアンドフィールを構成する手順の詳細については、「 [AD FS サインインページのカスタマイズ](../operations/AD-FS-Customization-in-Windows-Server-2016.md)」を参照してください。  
  
既存の AD FS ファームに Windows Server 2012 R2 に移行する web ページのカスタマイズがある場合は、Windows Server 2012 R2 の新しいカスタマイズ機能を使用して、移行プロセスの一部として web ページを再作成することができます。  
  
-   **その他の変更**  
  
    -   Windows Server 2012 R2 の AD FS は、WIF 4.5 ではなく、Windows Identity Foundation (WIF) 3.5 に基づいています。 そのため、Windows Server 2012 R2 の AD FS では、WIF 4.5 (Kerberos 信頼性情報やダイナミックアクセス制御など) の一部の機能はサポートされていません。  
  
    -   Windows Server 2012 R2 のデバイス登録サービス (DRS) は、ポート443で動作します。ユーザー証明書認証用の ClientTLS はポート49443で動作します  
  
        -   ブラウザー以外のアクティブ クライアントで、ポート 443 を参照するように特別にハードコードされている証明書トランスポート モード認証を使用する場合、ユーザー証明書認証をポート 49443 で使用し続けるには、そのコードの変更が必要です。  
  
        -   パッシブ アプリケーションの場合、変更は不要です。AD FS によりユーザー証明書認証が適切なポートにリダイレクトされるためです。  
  
        -   クライアントとプロキシとの間のファイアウォール ポートでは、ユーザー証明書認証のトラフィックがポート 49443 を通過できるようにする必要があります。  
  
##  <a name="ad-fs-requirements-in-windows-server-2012-r2"></a>Windows Server 2012 R2 の AD FS の要件  
 AD FS ファームを Windows Server 2012 R2 に正常に移行するには、次の要件を満たしている必要があります。  
  
 AD FS を機能させるには、フェデレーションを行う各コンピューターがドメインに参加している必要があります。  
  
 Windows Server 2012 R2 で実行されている AD FS を機能させるには、Active Directory ドメインが次のいずれかを実行している必要があります。  
  
- Windows Server 2012 R2  
  
- Windows Server 2012  
  
- Windows Server 2008 R2  
  
- Windows Server 2008  
  
  AD FS のサービスアカウントとしてグループの管理されたサービスアカウント (gMSA) を使用する場合は、Windows Server 2012 または Windows Server 2012 R2 オペレーティングシステムで実行されている環境内に少なくとも1つのドメインコントローラーが必要です。  
  
  AD FS の展開の一部として AD Workplace Join 用のデバイス登録サービス (DRS) を展開する予定がある場合は、AD DS スキーマを Windows Server 2012 R2 レベルに更新する必要があります。 スキーマを更新するには 3 種類の方法があります。  
  
1.  既存の Active Directory フォレストで、windows Server 2012 R2 オペレーティングシステム DVD の \support\adprep フォルダーから、Windows Server 2008 以降を実行している任意の64ビットサーバーの adprep/forestprep を実行します。 この場合は、追加のドメイン コントローラーをインストールする必要はなく、既存のドメイン コントローラーのアップグレードも必要ありません。  
  
adprep/forestprep を実行するには、Schema Admins グループ、Enterprise Admins グループ、およびスキーマ マスターをホストするドメインの Domain Admins グループのメンバーである必要があります。  
  
2. 既存の Active Directory フォレストに、Windows Server 2012 R2 を実行するドメインコントローラーをインストールします。 この場合、adprep/forestprep は、ドメインコントローラーのインストールの一部として自動的に実行されます。  
  
ドメイン コントローラーのインストール時に、adprep /forestprep を実行するための追加の資格情報の入力が必要になる場合があります。  
  
3. Windows Server 2012 R2 を実行しているサーバーに AD DS をインストールして、新しい Active Directory フォレストを作成します。 この場合、DRS をサポートするために必要なすべてのコンテナーとオブジェクトを使用してスキーマが最初に作成されるため、adprep/forestprep を実行する必要はありません。  
  
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
  
-   Windows Server 2012 R2 のインストール CD の \support\adfs フォルダーにある移行スクリプトでは、Windows に移行するときに、従来の AD FS ファームで使用していたものと同じフェデレーションサーバーファーム名とサービスアカウント id 名を保持する必要があります。サーバー 2012 R2。  
  
-   SQL Server の AD FS ファームを移行する場合は、移行プロセスに新しい SQL データベース インスタンスの作成が含まれ、そのインスタンスに元の構成データをインポートする必要があることに注意してください。  
  
## <a name="next-steps"></a>次の手順
 [Active Directory フェデレーションサービス (AD FS) の役割サービスを Windows Server 2012 R2 に移行する](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [AD FS フェデレーションサーバーの移行](migrate-ad-fs-fed-server-r2.md)   
 [AD FS フェデレーションサーバープロキシの移行](migrate-fed-server-proxy-r2.md)   
 [Windows Server 2012 R2 への AD FS 移行の検証](verify-ad-fs-migration.md)