---
ms.assetid: 22f53391-8c6a-4873-a1f4-08b4760ea621
title: 要求の役割
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 542d7a24e29b52dd3fa0d7ea6a9b2d27fb620d8d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188503"
---
# <a name="the-role-of-claims"></a>要求の役割
要求に\-ベースの id モデルでは、要求はフェデレーション プロセスで重要な役割を再生する、これによって、重要なコンポーネントはすべての Web の結果\-ベースの認証および承認要求が決定されます。 このモデルを使用することで、組織はデジタル ID とアクセス権、つまり*要求*をセキュリティや企業の境界を越えて、標準化された方法で安全に提示できるようになります。  
  
## <a name="what-are-claims"></a>要求とは  
最も単純な形式の要求は単に*ステートメント*\(名前、id、グループ\)に作成された、要求へのアクセスを認証するには、主に使用されるユーザーについて、\-ベースのアプリケーションインターネット上の任意の場所に存在します。 各ステートメントは、要求に格納される*値*に対応します。  
  
### <a name="how-claims-are-sourced"></a>要求の提供元  
Active Directory フェデレーション サービスでフェデレーション サービス\(AD FS\)要求がフェデレーション パートナー間で交換されるを定義します。 ただし、この定義を行う前に、取得または計算された値を要求に格納または提供する必要があります。 各要求の値は、ユーザー、グループ、またはエンティティの値を表し、次の 2 つのいずれかの方法で提供されます。  
  
1.  要求を構成する値が属性ストアから取得される場合。たとえば、属性値 Sales Department が Active Directory ユーザー アカウントのプロパティから取得されるような場合です。 詳細については、「[属性ストアの役割](The-Role-of-Attribute-Stores.md)」を参照してください。  
  
2.  入力方向の要求の値が、規則で表されているロジックに基づいて別の値に変換される場合。 たとえば、入力方向の要求に含まれる Domain Admins という値が、出力方向の要求として送信される前に新しい値 Administrators に変換されるような場合です。 詳細については、「[要求規則の役割](The-Role-of-Claim-Rules.md)」を参照してください。  
  
クレームは、電子メールなどの値を含めることができます\-メール アドレス、ユーザー プリンシパル名\(UPN\)、グループ メンバーシップ、およびその他のアカウントの属性。  
  
### <a name="how-claims-flow"></a>要求のフロー  
Web の承認タスクを実行するクレームの値を使用して他のパーティ\-ベースのホスト アプリケーション。 これらのパーティと呼びます*証明書利用者*AD FS 管理スナップインで\-でします。 フェデレーション サービスは多くの異なる利用者間の信頼を仲介します。 処理し、最初に、要求とも呼ばを提供する組織からのクレームの信頼されている exchange のフローに設計されています*クレーム プロバイダー* AD FS 管理スナップインで\-で、証明書利用者のパーティにします。 証明書利用者は、受け取った要求を使用して承認の判断を下します。  
  
このようなプロセスを実行する要求のフローを*要求パイプライン*と呼びます。 要求パイプラインでの要求のフローは、次の 3 つのステップから構成されます。  
  
1.  要求プロバイダーから受け取った要求は、要求プロバイダー信頼の受け入れ変換規則によって処理されます。 これらの規則は、要求プロバイダーから受け入れる要求を決定します。  
  
2.  受け入れ変換規則の出力は、発行承認規則の入力として使用されます。 これらの規則は、ユーザーが証明書利用者へのアクセスを許可されるかどうかを決定します。  
  
3.  受け入れ変換規則の出力は、発行変換規則の入力として使用されます。 これらの規則は、証明書利用者に送信される要求を決定します。  
  
詳細については、「[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)」を参照してください。  
  
### <a name="how-claims-are-issued"></a>要求の発行  
要求規則を記述する場合、要求規則の入力方向の要求のソースは、要求プロバイダー信頼または証明書利用者信頼のどちらの規則を記述するかによって異なります。 要求プロバイダー信頼の要求規則を記述する場合、入力方向の要求は、信頼される要求プロバイダーからフェデレーション サービスに送信される要求です。 証明書利用者信頼のルールを記述するときに、入力方向の要求は、該当する要求プロバイダー信頼の要求規則によって出力されるクレームを使用します。 入力方向と出力方向の要求に関する詳細については、「[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)」および「[要求エンジンの役割](The-Role-of-the-Claims-Engine.md)」を参照してください。  
  
## <a name="what-are-claim-types"></a>要求の種類とは  
要求の種類は、要求の値のコンテキストを提供します。 通常は、Uniform Resource Identifier として表される\(URI\)します。 AD FS は、あらゆる種類の要求をサポートできるし、既定では、次の表に、要求の種類によって構成されます。  
  
|名前|説明|URI|  
|--------|---------------|-------|  
|E\-メール アドレス|E\-ユーザーのメール アドレス|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/クレーム\/emailaddress|  
|名|ユーザーの姓名の名|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/givenname|  
|名前|ユーザーの一意の名前|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/name|  
|UPN|ユーザー プリンシパル名\(UPN\)ユーザーの|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/upn|  
|共通名|ユーザーの共通名|http:\/\/schemas.xmlsoap.org\/クレーム\/CommonName|  
|AD FS 1.x 電子メール\-メール アドレス|E\-AD FS 1.1 または ad FS 1.0 と相互運用するときに、ユーザーのアドレスをメール|http:\/\/schemas.xmlsoap.org\/クレーム\/EmailAddress|  
|グループ|ユーザーが属するグループ|http:\/\/schemas.xmlsoap.org\/クレーム\/グループ|  
|AD FS 1.x UPN|AD FS 1.1 または AD FS 1.0 と相互運用するときのユーザーの UPN|http:\/\/schemas.xmlsoap.org\/クレーム\/UPN|  
|ロール|ユーザーの役割|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/クレーム\/ロール|  
|姓|ユーザーの姓名の姓|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/クレーム\/surname|  
|PPID|ユーザーの個人識別子|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/privatepersonalidentifier|  
|名前識別子|ユーザーの SAML 名前識別子|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/クレーム\/nameidentifier|  
|認証方法|ユーザー認証に使用される方法|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/クレーム\/authenticationmethod|  
|拒否専用グループ SID|Deny\-のみユーザーの SID のグループ|http:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/denyonlysid|  
|拒否専用プライマリ SID|Deny\-ユーザーのプライマリ SID のみ|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/クレーム\/denyonlyprimarysid|  
|拒否専用プライマリ グループ SID|Deny\-ユーザーの専用プライマリ グループ SID|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/クレーム\/denyonlyprimarygroupsid|  
|グループ SID|ユーザーのグループ SID|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/クレーム\/groupsid|  
|プライマリ グループ SID|ユーザーのプライマリ グループ SID|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/クレーム\/primarygroupsid|  
|プライマリ SID|ユーザーのプライマリ SID|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/クレーム\/primarysid|  
|Windows アカウント名|ドメイン アカウント名の形式でユーザーの\<ドメイン\>\\\<ユーザー\>|http:\/\/schemas.microsoft.com\/ws\/2008\/06\/identity\/クレーム\/windowsaccountname|  
  
## <a name="what-are-claim-descriptions"></a>要求記述とは  
要求記述は、フェデレーション メタデータに公開が AD FS サポートされ、クレームの種類の一覧を表します。 AD FS 管理スナップインで要求記述として、前の表で説明されている要求の種類が構成されて\-でします。  
  
フェデレーション メタデータに公開される要求記述のコレクションは、AD FS 構成データベースに格納されます。 これらの要求記述は、フェデレーション サービスのさまざまなコンポーネントで使用されます。  
  
各要求記述には、要求の種類の URI、名前、公開状態、および説明が含まれています。 使用して要求記述のコレクションを管理することができます、**要求記述**ノード AD FS 管理スナップインで\-でします。 スナップを使用して、要求記述の公開状態を変更する\-でします。 次の設定を使用できます。  
  
-   **このフェデレーション サービスが受け入れることができる要求の種類としてこの要求をフェデレーション メタデータで公開**\(受け付け済みとして公開\)-は、このフェデレーションで他の要求プロバイダーから受信する要求の種類を示しますサービス。  
  
-   **このフェデレーション サービスを送信できる要求の種類としてこの要求をフェデレーション メタデータで公開**\(送信済みとして公開\): このフェデレーション サービスによって提供されるクレームの種類を示します。 これらは、フェデレーション サービスが送信できる要求として公開する要求の種類です。 要求プロバイダーによって送信される実際の要求の種類は、多くの場合、このリストのサブセットとなります。  
  
要求の種類の公開状態を設定する方法の詳細については、次を参照してください。 [Add a Claim Description](https://technet.microsoft.com/library/dd807051.aspx) AD FS Deployment guide の「します。  
  
### <a name="when-generating-federation-metadata"></a>フェデレーション メタデータの生成  
フェデレーション メタデータには、公開対象としてマークされているすべての要求記述が含まれます。  
  
### <a name="when-claims-rules-are-processed"></a>要求規則の処理  
要求記述に関する構成情報を保持しておくと、要求に関する規則を簡単に構成できます。 要求プロバイダー組織で使用できる要求規則の詳細については、「[要求規則の役割](The-Role-of-Claim-Rules.md)」を参照してください。  
  

