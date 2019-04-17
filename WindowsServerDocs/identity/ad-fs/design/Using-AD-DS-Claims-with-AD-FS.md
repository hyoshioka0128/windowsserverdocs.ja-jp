---
ms.assetid: 460792e4-9f1d-4e7b-b6b2-53e057f839df
title: "AD FS 展開トポロジに関する考慮事項"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 46692653ba10558a9236bd321127591bc7c8a275
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="using-ad-ds-claims-with-ad-fs"></a>AD FS と AD DS を使用して信頼性情報
  
>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
  
Active Directory Domain Services \(AD DS\)\-issued ユーザーと Active Directory フェデレーション サービス \(AD FS\) とデバイスの信頼性情報を使用してフェデレーション アプリケーションの高度なアクセス制御を有効にすることができます。  
  
## <a name="about-dynamic-access-control"></a>ダイナミック アクセス制御について  
「Windows Server® 2012 では、ダイナミック アクセス制御の機能によって、組織はユーザーの信頼性情報に基づいてファイルへのアクセス許可を \ (によって供給されるユーザー アカウントの attributes\) とデバイスの信頼性情報 \ (によって供給されるコンピューター アカウント attributes\) Active Directory Domain Services \(AD DS\) によって発行されます。 信頼性情報を発行する AD DS は、Kerberos 認証プロトコルを使って Windows 統合認証に統合されます。  
  
ダイナミック アクセス制御の詳細については、次を参照してください。[ダイナミック アクセス制御: コンテンツ ロードマップ](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP)します。  
  
### <a name="whats-new-in-ad-fs"></a>AD FS の新機能ですか。  
ダイナミック アクセス制御シナリオの拡張として Windows Server 2012 で AD FS を実行できます。  
  
-   コンピューター アカウントの属性から AD DS 内のユーザー アカウント属性だけでなくにアクセスします。 AD FS の以前のバージョンで、フェデレーション サービスにアクセスできませんでしたコンピューター アカウントの属性すべての AD DS からです。  
  
-   AD DS を Kerberos 認証チケット内に存在するユーザーまたはデバイスの信頼性情報の発行を使用します。 AD FS の以前のバージョンで、要求エンジンがユーザーを読み込むことが、Kerberos からグループ セキュリティ Id \(SIDs\) ができませんでしたへ Kerberos チケットに含まれる情報を要求します。  
  
-   AD DS のユーザーまたはデバイスの信頼性情報を発行した証明書利用者アプリケーションを使用して高度なアクセス制御を実行する SAML トークンに変換します。  
  
## <a name="benefits-of-using-ad-ds-claims-with-ad-fs"></a>AD DS を使用する利点と AD FS のクレーム  
信頼性情報を発行したこれらの AD DS を Kerberos 認証チケットに挿入し、次の利点を提供する AD FS と共に使用できます。  
  
-   高度なアクセス制御ポリシーを必要とする組織では、特定のユーザーまたはコンピューター アカウントを AD DS に格納されている属性値に基づいて要求を発行する AD DS を使用してアプリケーションとリソースを claims\ ベースのアクセスを有効にできます。 管理者を作成および管理に関連するオーバーヘッドを減らすためにこのことができます。  
  
    -   AD DS セキュリティ グループをアプリケーションと統合 Windows 認証を介してアクセス可能なリソースへのアクセスを制御するそれ以外の場合に使用されます。  
  
    -   フォレストの Business\ 商取引へ記述 \(B2B\) へのアクセスを制御するそれ以外の場合に使用される信頼 \/インターネット アクセス可能なアプリケーションとリソースです。  
  
-   組織は特定のコンピューター アカウントが AD DS に格納されている値を属性かどうかに基づいて、クライアント コンピューターからネットワーク リソースに、不正アクセスを防止できるようになりましたことができます \ (たとえば、コンピューターの DNS 名前 \/)、リソースのアクセス制御ポリシーと一致する \ (claims\ のように ACLd をされているファイル サーバーなど) または証明書利用者のパーティ ポリシー \ (たとえば、claims\ 対応 Web できるアプリケーション)。 管理者のリソースやアプリケーションをさらに細かくアクセス制御ポリシーを設定してこのことができます。  
  
    -   統合 Windows 認証を介してのみアクセスできます。  
  
    -   インターネットの AD FS の認証メカニズムを使用してアクセスします。 AD FS を使用して、デバイスの信頼性情報をインターネット アクセス可能なリソースまたは証明書利用者のパーティ アプリケーションで使用できる SAML トークンにカプセル化することができます、AD FS の要求に発行する AD DS を変換することができます。  
  
## <a name="differences-between-ad-ds-and-ad-fs-issued-claims"></a>要求を発行する AD DS および AD FS の違い  
AD DS と AD FS から発行されるクレームを理解するために重要な 2 つの差別化要因があります。 これらの相違点は次のとおりです。  
  
-   AD DS では、Kerberos チケット、SAML トークンいないにカプセル化されたクレームを発行できるのみです。 AD DS の要求を発行する方法の詳細については、次を参照してください。[ダイナミック アクセス制御: コンテンツ ロードマップ](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP)します。  
  
-   AD FS では、いない Kerberos チケット、SAML トークンにカプセル化されたクレームを発行できるのみです。 AD FS の要求を発行する方法の詳細については、次を参照してください。 [The Role of the Claims Engine](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)します。  
  
## <a name="how-ad-ds-issued-claims-work-with-ad-fs"></a>AD DS が AD FS による信頼性情報の作業を発行する方法  
信頼性情報を発行する AD DS は、ユーザーとデバイスの両方の要求から直接アクセスするユーザーの認証コンテキストではなく、Active Directory に別個の LDAP 呼び出しを行う AD FS で使用できます。 次の図と対応する手順は、このプロセスが、ダイナミック アクセス制御のシナリオの claims\ ベースのアクセス制御を有効にさらに詳しく動作方法について説明します。  
  
![信頼性情報の使用](media/UsingADDSClaimswithADFS.gif)  
  
1.  AD DS 管理者は、AD DS スキーマで、Active Directory 管理センター コンソールまたは特定のクレーム タイプのオブジェクトを有効にする PowerShell コマンドレットを使用します。  
  
2.  AD FS 管理者では、AD FS 管理コンソールを使用して作成し、要求プロバイダーと証明書利用者を構成するかとの信頼関係 pass\ を通じて変換要求規則またはです。  
  
3.  Windows クライアントがネットワークにアクセスしようとするとします。 Kerberos 認証プロセスの一環として、クライアントがそのユーザーに提示し、コンピューター ticket\ 保証チケットがサポートしていない \(TGT\) まだ、要求には、ドメイン コント ローラーが含まれています。 ドメイン コント ローラー AD DS で有効になっているクレームの種類が検索され、返された Kerberos チケット内の任意の結果として得られるクレームが含まれています。  
  
4.  ユーザー/クライアントが、信頼性情報を必要とするように ACLd であるファイル リソースにアクセスしようとすると、Kerberos から表示されました複合の ID にこれらの要求があるため、リソースにアクセスすることができます。  
  
5.  同じクライアントが AD FS の認証用に構成されている Web サイトまたは Web アプリケーションにアクセスしようとすると、ユーザーが Windows 統合認証用に構成されている AD FS フェデレーション サーバーにリダイレクトします。 クライアントは、Kerberos を使用して、ドメイン コント ローラーに要求を送信します。 ドメイン コント ローラーは、フェデレーション サーバーにクライアントを表示できますし、要求されたクレームが含まれる Kerberos チケットを発行します。  
  
6.  要求規則は、要求プロバイダーで構成されている方法に基づいており、証明書利用者の信頼を構成した管理者は、AD FS、Kerberos チケットからの信頼性情報を読み取るし、クライアントに発行する SAML トークンに含めます。  
  
7.  クライアントは正しい要求を含む SAML トークンを受信しが、web サイトにリダイレクトし、します。  
  
AD FS と連動する信頼性情報を発行する AD DS に必要な要求規則を作成する方法の詳細については、次を参照してください。[入力方向の要求を変換する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
