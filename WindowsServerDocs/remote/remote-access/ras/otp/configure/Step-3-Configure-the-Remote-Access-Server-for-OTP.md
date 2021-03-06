---
title: 手順 3 OTP 用のリモート アクセス サーバーを構成します。
description: このトピックでは、ガイド Windows Server 2016 での OTP 認証を使用したリモート アクセスの展開の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df1e87f2-6a0f-433b-8e42-816ae75395f9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 093877657f19006bba2b80c10b92db1fb3b40fde
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280864"
---
# <a name="step-3-configure-the-remote-access-server-for-otp"></a>手順 3 OTP 用のリモート アクセス サーバーを構成します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

ソフトウェア配布のトークンを RADIUS サーバーを構成すると、通信のポートが開いて、共有シークレットが作成された、Active Directory に対応するユーザー アカウントが、RADIUS サーバーで作成された、リモート アクセス サーバーにリモート アクセス サーバーは OTP をサポートするように構成する必要があり、RADIUS 認証エージェントと構成されました。  
  
|タスク|説明|  
|----|--------|  
|[3.1 除外ユーザーが OTP 認証 (省略可能)](#BKMK_Exempt)|特定のユーザーは、OTP 認証を使用した DirectAccess から除外されます場合、次の準備手順。|  
|[3.2 OTP をサポートするためにリモート アクセス サーバーを構成します。](#BKMK_Config)|リモート アクセス サーバーでは、OTP 2 要素認証をサポートするためにリモート アクセスの構成を更新します。|  
|[3.3 追加の承認のスマート カードの](#BKMK_Smartcard)|スマート カードの使用に関する追加情報。|  
  
> [!NOTE]  
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="BKMK_Exempt"></a>3.1 除外ユーザーが OTP 認証 (省略可能)  
特定のユーザーが OTP 認証から除外する場合は、次の手順は、リモート アクセス構成の前に実行する必要があります。  
  
> [!NOTE]  
> OTP の除外グループを構成するときに完了するドメイン間のレプリケーションを待つ必要があります。  
  
#### <a name="create-user-exemption-security-group"></a>ユーザーの除外セキュリティ グループを作成します。  
  
1.  Active Directory での目的は、OTP 除外セキュリティ グループを作成します。  
  
2.  OTP 認証から除外するセキュリティ グループのすべてのユーザーを追加します。  
  
    > [!NOTE]  
    > OTP 除外セキュリティ グループにユーザー アカウント、およびコンピューター アカウントではなくのみを含めるに確認します。  
  
## <a name="BKMK_Config"></a>3.2 OTP をサポートするためにリモート アクセス サーバーを構成します。  
2 要素認証を使用するリモート アクセスと OTP RADIUS サーバーと、前のセクションから証明書の展開を構成するには、次の手順を使用します。  
  
#### <a name="configure-remote-access-for-otp"></a>OTP 用のリモート アクセスを構成します。  
  
1.  開いている**リモート アクセス管理** をクリック**構成**します。  
  
2.  **DirectAccess のセットアップ**ウィンドウで、**手順 2 - リモート アクセス サーバー**、 をクリックして**編集**します。  
  
3.  をクリックして**次**3 回と、**認証**両方のセクションを選択します**2 要素認証**と**OTP を使用**を確認してください**コンピューター証明書を使用して、** がチェックされます。  
  
    > [!NOTE]  
    > OTP が選択を解除して OTP を無効にした場合、リモート アクセス サーバーで有効にされた後**OTP を使用**サーバーで、ISAPI および CGI 拡張機能がアンインストールされます。  
  
4.  Windows 7 のサポートが必要な場合は、選択、**を有効にする Windows 7 クライアント コンピューターを DirectAccess 経由で接続を**チェック ボックスをオンします。 注:前述の計画セクションでは、Windows 7 クライアントに DirectAccess otp をサポートするためにインストールされている DCA 2.0 は必要です。  
  
5.  **[次へ]** をクリックします。  
  
6.  **OTP RADIUS サーバー**セクションで、空白をダブルクリックして**サーバー名**フィールド。  
  
7.  **RADIUS サーバーの追加**ダイアログ ボックスで、RADIUS サーバーの名前を入力、**サーバー名**フィールド。 クリックして**変更**横に、**共有シークレット**フィールドし、RADIUS サーバーを構成するときに使用したのと同じパスワードを入力、**新しいシークレット**と**新しいシークレットの確認入力**フィールド。 をクリックして**OK** 2 回、 をクリック**次へ**します。  
  
    > [!NOTE]  
    > RADIUS サーバーが、リモート アクセス サーバーとは異なるドメインの場合、**サーバー名**フィールドは、RADIUS サーバーの FQDN を指定する必要があります。  
  
8.  **OTP CA サーバー**セクションは、OTP クライアント認証証明書の登録を使用し、をクリックするには、CA サーバーを選択して**追加**します。 **[次へ]** をクリックします。  
  
9. **OTP 証明書テンプレート**セクション**参照**OTP 認証用に発行される証明書の登録を使用する証明書テンプレートを選択します。  
  
    > [!NOTE]  
    > 「失効情報に含めない発行された証明書」オプションを指定せず、OTP 証明書が社内の CA によって発行された証明書テンプレートを構成する必要があります。 証明書テンプレートの作成中にこのオプションがオンの場合は、OTP クライアント コンピューターを正しくログオン失敗します。  
  
    クリックして**参照**OTP 証明書の登録要求の署名に、リモート アクセス サーバーによって使用される証明書の登録に使用される証明書テンプレートを選択します。 **[OK]** をクリックします。 **[次へ]** をクリックします。  
  
10. DirectAccess OTP とから特定のユーザーを除外することが必要場合、次に、 **OTP 除外**セクションを選択**2 要素認証を使用して認証を指定したセキュリティ グループのユーザーが必要としません。** . クリックして**セキュリティ グループ**OTP の除外を作成したセキュリティ グループを選択します。  
  
11. **リモート アクセス サーバーのセットアップ**ページ クリック**完了**します。  
  
12. **DirectAccess のセットアップ**ウィンドウで、**手順 3 - インフラストラクチャ サーバー**、 をクリックして**編集**します。  
  
13. をクリックして**次へ** 、2 回し、**管理**セクション をダブルクリック、**管理サーバー**フィールド。  
  
14. 入力、**コンピューター名**または**アドレス**OTP 証明書を発行し、をクリックして構成されている CA サーバーの**OK**します。  
  
15. **リモート アクセスのセットアップ**windows クリックして**完了**します。  
  
16. をクリックして**完了**上、 **DirectAccess エキスパート ウィザード**。  
  
17. **リモート アクセスの確認** ダイアログ ボックスをクリックして**適用**DirectAccess ポリシーを更新するには、待機し、クリックして**閉じる**します。  
  
18. **開始**画面で「**powershell.exe**、を右クリックして**powershell** をクリック**詳細**、 をクリック**として実行管理者**します。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、 **[はい]** をクリックします。  
  
19. Windows PowerShell ウィンドウで、入力**gpupdate/force** ENTER キーを押します。  
  
リモート アクセスの PowerShell コマンドを使用して OTP を構成するには  
  
![Windows PowerShell](../../../../media/Step-3-Configure-the-Remote-Access-Server-for-OTP/PowerShellLogoSmall.gif)**Windows PowerShell の同等のコマンド**  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
現在コンピューター証明書認証を使用する展開で 2 要素認証を使用するリモート アクセスを構成するには。  
  
```  
Set-DAServer -UserAuthentication TwoFactor  
```  
  
次の設定を使用して、OTP 認証を使用するリモート アクセスを構成するには。  
  
-   という名前の OTP.corp.contoso.com OTP サーバー。  
  
-   CA サーバーでは、APP1.corp.contoso.com\corp-APP1-CA1 という名前です。  
  
-   証明書テンプレートをという名前の DAOTPLogon OTP 認証用に発行される証明書の登録を使用します。  
  
-   OTP 証明書の登録要求の署名にリモート アクセス サーバーによって使用される登録機関の証明書を登録する DAOTPRA をという名前の証明書テンプレートを使用します。  
  
```  
Enable-DAOtpAuthentication -CertificateTemplateName 'DAOTPLogon' -SigningCertificateTemplateName 'DAOTPRA' -CAServer @('APP1.corp.contoso.com\corp-APP1-CA1') -RadiusServer OTP.corp.contoso.com -SharedSecret Abcd123$  
```  
  
PowerShell コマンドを実行した後は、OTP をサポートするためにリモート アクセス サーバーを構成する前の手順から手順 12-19 を完了します。  
  
> [!NOTE]  
> エントリ ポイントを追加する前にリモート アクセス サーバーで OTP 設定を設定することを確認してください。  
  
## <a name="BKMK_Smartcard"></a>3.3 追加の承認のスマート カードの  
手順 2 リモート アクセス セットアップ ウィザードの [認証] ページで、内部ネットワークへのアクセスにスマート カードの使用を要求できます。 このオプションを選択すると、リモート アクセスのセットアップ ウィザードは、スマート カードとトンネル モードの承認を要求するように DirectAccess サーバーのイントラネット トンネルの IPsec 接続セキュリティ規則を構成します。 トンネル モードの承認は、ことを指定することのみ承認されたコンピューターまたはユーザーが、受信トンネルを確立できます。  
  
イントラネット トンネルで IPsec トンネル モードの承認をスマート カードを使用するには、スマート カード インフラストラクチャと公開キー基盤 (PKI) を展開する必要があります。  
  
ファイル、フォルダー、およびかどうかに基づいて、プリンターなどのリソースへのアクセスを制御する認証メカニズム保証、Windows Server 2008 R2 の機能を使用できますも、DirectAccess クライアントは、イントラネットへのアクセスにスマート カードを使用している、ため、ユーザーがスマート カード ベースの証明書を使ってログオンします。 認証メカニズム保証では、Windows Server 2008 R2 のドメインの機能レベルが必要です。  
  
### <a name="allowing-access-for-users-with-unusable-smart-cards"></a>使用不可のスマート カードを持つユーザーのアクセスを許可します。  
を使用できるスマート カードを持つユーザーの一時的なアクセスを許可するのには、次の操作を行います。  
  
1.  Active Directory セキュリティ グループを含めることはできませんが、スマート カードを使用して一時的にユーザーのユーザー アカウントを作成します。  
  
2.  DirectAccess サーバーのグループ ポリシー オブジェクトには、IPsec トンネルの承認にグローバル IPsec 設定を構成し、承認されたユーザーの一覧を Active Directory セキュリティ グループを追加します。  
  
ユーザーのスマート カードを使用できないユーザーにアクセスを許可するには、Active Directory セキュリティ グループに、ユーザー アカウントを一時的に追加します。 スマート カードが使用可能な場合は、グループからユーザー アカウントを削除します。  
  
### <a name="under-the-covers-smart-card-authorization"></a>実際には。スマート カードの承認  
スマート カード認証は、特定の Kerberos ベースのセキュリティ識別子 (SID) の DirectAccess サーバーのイントラネット トンネルの接続セキュリティ規則でトンネル モードの承認を有効にして動作します。 スマート カード認証、スマート カード ベースのログオンにマップする既知の SID (S-1-5-65-1)、これです。 この SID は、DirectAccess クライアントの Kerberos トークンに存在し、"この組織の証明書として"グローバル IPsec で構成されている場合にトンネル モード承認の設定と呼びます。  
  
DirectAccess のセットアップ ウィザードの手順 2. でスマート カード認証を有効にすると、DirectAccess のセットアップ ウィザードは、DirectAccess サーバーのグループ ポリシー オブジェクトのこの SID を持つグローバル IPsec トンネル モードの承認設定を構成します。 高度なセキュリティ スナップインの DirectAccess サーバーのグループ ポリシー オブジェクトで Windows ファイアウォールでこの設定を表示するには、次の操作を行います。  
  
1.  セキュリティが強化された Windows ファイアウォールを右クリックし、し、[プロパティ] をクリックします。  
  
2.  IPsec の設定 タブで、IPsec トンネルの承認では、カスタマイズ をクリックします。  
  
3.  [ユーザー] タブをクリックします。権限を持つユーザーとして、"NT AUTHORITY\This 組織 Certificate"が表示されます。  
  


