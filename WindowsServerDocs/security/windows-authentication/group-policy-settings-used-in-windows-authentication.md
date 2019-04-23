---
title: Windows 認証で使用されるグループ ポリシー設定
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e237f89-45b1-4a4e-9b72-11dc7d6a470b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 38df2033b57c0394b96f539f54efe6a3579500f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847933"
---
# <a name="group-policy-settings-used-in-windows-authentication"></a>Windows 認証で使用されるグループ ポリシー設定

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

IT プロフェッショナル向けのこのリファレンス トピックでは、使用し、認証プロセスでのグループ ポリシー設定の影響について説明します。

ユーザー、コンピューター、およびサービス アカウントをグループに追加することで、それらのグループに認証ポリシーを適用することでし、Windows オペレーティング システムでの認証を管理できます。 これらのポリシーは、ローカル セキュリティ ポリシーと管理用テンプレート グループ ポリシー設定とも呼ばれますとして定義されます。 両方のセットを構成およびグループ ポリシーを使用して、組織全体に分散できます。

> [!NOTE]
> Windows Server 2012 R2 で導入された機能では、対象となるサービスの認証ポリシーを構成できます。 または、保護されたアカウントのアプリケーションを使用して一般認証サイロと呼ばれます。 Active Directory でこれを行う方法については、次を参照してください。 [How to Configure Protected Accounts](how-to-configure-protected-accounts.md)します。

たとえば、組織内の関数に基づくグループに、次のポリシーを適用できます。

-   ローカルまたはドメインにログオンします。

-   ネットワーク経由でログオンします。

-   アカウントをリセットします。

-   アカウントを作成します。

次の表では、認証に関連するポリシー グループを一覧表示し、これらのポリシーを構成するのに役立つドキュメントへのリンクを提供します。

|ポリシー グループ|Location|説明|
|--------|------|--------|
|**パスワード ポリシー**|ローカル コンピューター ポリシー \windows 設定 \ セキュリティ アカウント ポリシー|パスワード ポリシーは、パスワードの動作と特性に影響します。 ドメイン アカウントまたはローカル ユーザー アカウントのパスワード ポリシーが使用されます。 強制の有効期間などのパスワードの設定を決定します。<br /><br />特定の設定については、次を参照してください。[パスワード ポリシー](https://technet.microsoft.com/itpro/windows/keep-secure/password-policy)します。|
|**アカウント ロックアウトのポリシー**|ローカル コンピューター ポリシー \windows 設定 \ セキュリティ アカウント ポリシー|アカウント ロックアウトのポリシー オプションは、設定された数のログオン試行の失敗後にアカウントを無効にします。 これらのオプションを使用すると、検出し、パスワードを中断する試行をブロックすることができます。<br /><br />アカウント ロックアウトのポリシーのオプションについては、次を参照してください。[アカウント ロックアウトのポリシー](https://technet.microsoft.com/itpro/windows/keep-secure/account-lockout-policy)します。|
|**Kerberos ポリシー**|ローカル コンピューター ポリシー \windows 設定 \ セキュリティ アカウント ポリシー|Kerberos 関連の設定には、チケットの有効期間と適用規則が含まれます。 ローカル アカウントの認証に Kerberos 認証プロトコルが使用されていないために、Kerberos のポリシーはローカル アカウント データベースには適用されません。 そのため、Kerberos のポリシー設定は、既定のドメイン グループ ポリシー オブジェクト (GPO)、ドメインへのログオンに影響をによってのみ構成できます。<br /><br />ドメイン コント ローラー用の Kerberos のポリシー オプションについては、次を参照してください。 [Kerberos ポリシー](https://technet.microsoft.com/itpro/windows/keep-secure/kerberos-policy)します。|
|**監査ポリシー**|Local Computer Policy\Computer Configuration\Windows Settings\Security Settings\Local Policies\Audit Policy|監査ポリシーを制御し、ファイルやフォルダーなど、ユーザーおよびグループ アカウントとユーザーのログオンとログオフを管理するオブジェクトへのアクセスを理解することができます。 監査ポリシーは、監査、サイズとセキュリティ ログの動作を設定およびオブジェクトのアクセスを監視して、監視するアクセスの種類を決定するイベントのカテゴリを指定できます。<br /><br />|
|**ユーザー権利の割り当て**|Local Computer Policy\Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment|通常、ユーザーの権利は、ユーザーが所属するなど、管理者、パワー ユーザーまたはユーザー セキュリティ グループに基づいて割り当てられます。 このカテゴリのポリシー設定は通常のアクセスとセキュリティ グループのメンバーシップのメソッドに基づくコンピューターへのアクセス許可または拒否に使用されます。|
|**セキュリティ オプション**|Local Computer Policy\Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options|認証に関連するポリシーは次のとおりです。<br /><br />-デバイス<br />ドメイン コント ローラー<br />ドメイン メンバー<br />対話型ログオン<br />Microsoft ネットワーク サーバー<br />-ネットワーク アクセス<br />-ネットワーク セキュリティ<br />-回復コンソール<br />シャット ダウン<br /><br />|
|**資格情報の委任**|コンピューターの構成 \ 管理用システム \ の委任|資格情報の委任は、ローカルの資格情報を他のシステムでは、最も顕著なメンバー サーバーとドメイン内のドメイン コント ローラーで使用できるメカニズムです。 これらの設定は、Credential Security Support Provider (Cred SSP) を使用してアプリケーションに適用されます。 リモート デスクトップ接続では、例を示します。|
|**KDC**|Computer Configuration\Administrative Templates\System\KDC|これらのポリシー設定では、キー配布センター (KDC) ドメイン コント ローラー サービスであるが Kerberos 認証要求を処理する方法に影響します。|
|**Kerberos**|Computer Configuration\Administrative Templates\System\Kerberos|これらのポリシー設定では、信頼性情報、Kerberos 防御、複合認証、プロキシ サーバーの識別、およびその他の構成のサポートを処理するために Kerberos を構成する方法に影響します。|
|**ログオン**|コンピューターの構成\管理用テンプレート\システム\ログオン|これらのポリシー設定では、システムがユーザーのログオン エクスペリエンスを表示する方法を制御します。|
|**Net Logon**|Computer Configuration\Administrative Templates\System\Net Logon|これらのポリシー設定では、ドメイン コントローラ ロケータが動作する方法を含むネットワーク ログオン要求を処理する方法を制御します。<br /><br />ドメイン コントローラ ロケータがレプリケーション プロセスに適合する方法の詳細については、次を参照してください。 [Understanding Replication Between Sites](https://technet.microsoft.com/library/cc771251.aspx)します。|
|**生体認証**|コンピューターの構成 \ 管理用テンプレート \windows コンポーネント \ Components\Biometrics|これらのポリシー設定は、一般に許可または認証方法として生体認証の使用を拒否します。<br /><br />生体認証の Windows 実装の詳細については、Windows 生体認証フレームワークの概要を参照してください。|
|**資格情報ユーザー インターフェイス**|コンピューターの構成 \ 管理用テンプレート \windows コンポーネント \ 資格情報ユーザー インターフェイス|これらのポリシー設定では、エントリの時点での資格情報を管理する方法を制御します。|
|**パスワード同期**|コンピューターの構成 \ 管理用テンプレート \windows コンポーネント \ Components\Password の同期|これらのポリシー設定では、システムが Windows と UNIX ベースのオペレーティング システム間でパスワードの同期を管理する方法を決定します。<br /><br />詳細については、次を参照してください。[パスワード同期](https://technet.microsoft.com/library/cc732609.aspx)します。|
|**スマート カード**|コンピューターの構成 \ 管理用テンプレート \windows コンポーネント \ Components\Smart カード|これらのポリシー設定では、システムによるスマート カードによるログオンの管理方法を制御します。<br /><br />|
|**Windows のログオン オプション**|コンピューターの構成 \ 管理用テンプレート \windows コンポーネント \windows ログオン オプション|これらのポリシー設定では、ログオンの機会を利用できる時期と方法を制御します。|
|**Ctrl + Alt + Del オプション**|コンピューターの構成 \ 管理用テンプレート \windows コンポーネント \ Components\Ctrl + Alt + Del オプション|これらのポリシー設定は、UI (セキュリティで保護されたデスクトップ) のログオン時に、タスク マネージャーやコンピューターのキーボード ロックなどの機能へのアクセシビリティとの外観に影響します。|
|**ログオン**|Computer Configuration\Administrative Templates\Windows Components\Logon|これらのポリシー設定を決定場合またはのどのプロセスは、ユーザーがログオンしたときに実行できます。|

## <a name="see-also"></a>関連項目
[Windows 認証の技術概要](windows-authentication-technical-overview.md)


