---
ms.assetid: 460792e4-9f1d-4e7b-b6b2-53e057f839df
title: AD FS 展開トポロジに関する考慮事項
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3086de9dc34f555d5f6056716ab9572b980f1962
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858755"
---
# <a name="using-ad-ds-claims-with-ad-fs"></a>AD DS の要求を AD FS と共に使用する
  
  
Active Directory Domain Services \(\)AD DS を使用することにより、フェデレーションアプリケーションのより高度なアクセス制御を有効にすることができます。 \-Active Directory フェデレーションサービス (AD FS) \(AD FS と共にユーザーとデバイスの信頼性情報を発行\)ます。  
  
## <a name="about-dynamic-access-control"></a>ダイナミック アクセス制御について  
Windows Server&reg; 2012 では、動的 Access Control 機能を使用して、ユーザーアカウント属性\) およびデバイスの信頼性情報によって供給されるユーザー要求 \(に基づいてファイルへのアクセス権を付与することができます。これは \(\) Active Directory Domain Services \(によって発行された AD DS コンピューターアカウントの属性によって供給されます。\) 要求を発行する AD DS は、Kerberos 認証プロトコルを使って Windows 統合認証に統合されます。  
  
ダイナミック アクセス制御の詳細については、次を参照してください。 [ダイナミック アクセス制御: コンテンツ ロードマップ](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP)します。  
  
### <a name="whats-new-in-ad-fs"></a>AD FS の新機能  
ダイナミック アクセス制御シナリオの拡張として Windows Server 2012 の AD FS を実行できます。  
  
-   コンピューター アカウントの属性から AD DS 内のユーザー アカウント属性だけでなくにアクセスします。 AD FS の以前のバージョンで、フェデレーション サービスからアクセスできませんでしたコンピューター アカウントの属性すべての AD DS です。  
  
-   AD DS の認証で Kerberos チケット内に存在するユーザーまたはデバイスの要求を発行を使用します。 要求エンジンのユーザーとグループのセキュリティ Id を読み込むことが AD FS の以前のバージョンで \(Sid\) から Kerberos でしたへ Kerberos チケットに含まれる情報を要求します。  
  
-   AD DS のユーザーまたはデバイスの信頼性情報を発行した証明書利用者アプリケーションを使用して高度なアクセス制御を実行する SAML トークンに変換します。  
  
## <a name="benefits-of-using-ad-ds-claims-with-ad-fs"></a>AD DS を使用する利点と AD FS の要求  
クレームを発行したこれらの AD DS を Kerberos 認証チケットに挿入され、次の利点を提供する AD FS と共に使用します。  
  
-   高度なアクセス制御ポリシーを必要とする組織には、クレームが有効にすることができます\-アプリケーションや AD DS を使用してリソースにベースのアクセスは、特定のユーザーまたはコンピューター アカウント用の AD DS に格納されている属性値に基づく要求を発行します。 これを作成および管理に関連するオーバーヘッドを減らすために管理者に役立ちます。  
  
    -   AD DS セキュリティ グループをアプリケーションと統合 Windows 認証を介してアクセス可能なリソースへのアクセスを制御するそれ以外の場合に使用されます。  
  
    -   ビジネス\-へのアクセスを制御するために使用されるフォレストの信頼は、インターネットにアクセス可能なアプリケーションとリソース \/ のビジネス \(B2B\)\-ます。  
  
-   \(AD DS に格納されている特定のコンピューターアカウントの属性値 (たとえば、コンピューターの DNS\) 名が \(リソースのアクセス制御ポリシーと一致しているかどうかなどに基づいて、クライアントコンピューターからのネットワークリソースへの不正アクセスを防ぐことができるようになりました。たとえば、要求\) を含むファイルサーバーや、証明書利用者ポリシー \(たとえば、要求\-\) これにより管理者はリソースやアプリケーションをさらに細かくアクセス制御ポリシーを設定できます。  
  
    -   Windows 統合認証を使用してのみアクセスできます。  
  
    -   インターネットの AD FS の認証メカニズムを使用してアクセスできます。 AD FS を使用して、デバイスの信頼性情報を発行したインターネット アクセス可能なリソースまたは証明書利用者アプリケーションで使用できる SAML トークンにカプセル化されることができます、AD FS の要求に AD DS を変換することができます。  
  
## <a name="differences-between-ad-ds-and-ad-fs-issued-claims"></a>AD DS および AD FS の違いは、要求を発行  
AD DS と AD FS から発行される要求について理解するために重要な2つの差別化要因があります。 これらの相違点は次のとおりです。  
  
-   AD DS では、Kerberos チケット、SAML トークンではないでカプセル化されたクレームを発行できるのみです。 AD DS での要求を発行する方法の詳細については、次を参照してください。 [ダイナミック アクセス制御: コンテンツ ロードマップ](../../solution-guides/Dynamic-Access-Control--Scenario-Overview.md#BKMK_APP)します。  
  
-   AD FS では、SAML トークン、Kerberos チケットではないでカプセル化されたクレームを発行できるのみです。 AD FS での要求を発行する方法の詳細については、次を参照してください。 [要求エンジンの役割](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)します。  
  
## <a name="how-ad-ds-issued-claims-work-with-ad-fs"></a>AD DS 発行の要求が AD FS と連携するしくみ  
AD DS 発行された要求は、AD FS と共に使用して、ユーザーとデバイスの両方の信頼性情報にユーザーの認証コンテキストから直接アクセスすることができます。このとき、Active Directory に対して個別の LDAP 呼び出しを行う必要はありません。 次の図と対応する手順は、このプロセスが要求を有効にするより詳細でどのように動作するかについて説明します\-ベースのダイナミック アクセス制御シナリオでは、アクセス制御します。  
  
![要求を使用します。](media/UsingADDSClaimswithADFS.gif)  
  
1.  AD DS 管理者は、AD DS スキーマ内の Active Directory 管理センター コンソールまたは特定のクレーム タイプのオブジェクトを有効にする PowerShell コマンドレットを使用します。  
  
2.  AD FS 管理者では、AD FS 管理コンソールを使用して作成し、要求プロバイダーと証明書利用者を構成を渡すかとの信頼関係\-を通じて変換要求規則またはです。  
  
3.  Windows クライアントがネットワークにアクセスしようとするとします。 Kerberos 認証プロセスの一環として、クライアントは、ユーザーとコンピューターのチケットを提示\-保証チケット \(TGT\) がまだ含まれていない、要求には、ドメイン コント ローラーをします。 ドメイン コント ローラー AD DS で有効になっているクレームの種類が検索され、返された Kerberos チケットの結果として得られるクレームが含まれています。  
  
4.  ときに、ユーザー\/クライアントが、クレームを要求するように ACLd であるファイル リソースにアクセスしようとした場合、Kerberos から表示されました複合の ID にこれらの要求があるため、リソースにアクセスすることができます。  
  
5.  同じクライアントが AD FS の認証用に構成されている Web サイトまたは Web アプリケーションにアクセスしようとした場合は、ユーザーが Windows 統合認証用に構成されている AD FS フェデレーション サーバーにリダイレクトされます。 クライアントは、Kerberos を使用してドメイン コント ローラーに要求を送信します。 ドメイン コント ローラーは、クライアントがフェデレーション サーバーに提供できる、要求されたクレームを格納している Kerberos チケットを発行します。  
  
6.  要求のルールは、要求プロバイダーで構成されている方法に基づいており、証明書利用者の信頼ことで構成した管理者は、AD FS、Kerberos チケットから身元証明データを読み取るし、クライアントに発行する SAML トークンに含めます。  
  
7.  クライアントは正しい要求を含む SAML トークンを受信し、web サイトにリダイレクトされています。  
  
AD DS が発行されたクレームの AD FS と連動するために必要なクレーム ルールを作成する方法の詳細については、次を参照してください。 [入力方向の要求を変換するルールを作成する](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)です。  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
