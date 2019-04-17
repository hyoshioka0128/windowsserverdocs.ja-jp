---
ms.assetid: 22f53391-8c6a-4873-a1f4-08b4760ea621
title: "要求の役割"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 98765deaba67ffdc0ee18b6d8ef573e531d739cc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="the-role-of-claims"></a>要求の役割
Claims\ ベースの ID モデルで要求はフェデレーション プロセスで重要な役割を再生するが、すべて Web ベースの認証および承認要求の結果を決定する際の主要コンポーネントです。 このモデルにより、安全に提示デジタル ID とアクセス権、または*クレーム*、セキュリティおよび標準化された方法で、エンタープライズの境界を越えてします。  
  
## <a name="what-are-claims"></a>信頼性情報とは何ですか。  
最もシンプルな形式の要求は*ステートメント*\ (たとえば、名前、id group\)、インターネット上の任意の場所にある claims\ ベースのアプリケーションへのアクセスを承認するためには、主に使用される、ユーザーに関して作成されました。 各ステートメントに対応する、*値*、要求に格納されています。  
  
### <a name="how-claims-are-sourced"></a>信頼性情報を供給する方法  
Active Directory フェデレーション サービス \(AD FS\) 内のフェデレーション サービスでは、フェデレーション パートナー間でやり取りされる要求を定義します。 ただし、これを行う前に、必要があります最初の設定または取得した値または計算された値のいずれかで信頼性情報をソースします。 各要求の値は、ユーザー、グループ、またはエンティティの値を表し、2 つの方法で提供されます。  
  
1.  ときに要求を構成している値とから取得されます属性ストアでは、たとえば、属性値 Sales Department が Active Directory ユーザー アカウントのプロパティから取得されます。 詳細については、次を参照してください。[属性ストアの役割を、](The-Role-of-Attribute-Stores.md)します。  
  
2.  ときに、入力方向の要求の値は、規則で表されているロジックに基づいて別の値に変換されます。 たとえば、Domain Admins という値を持つ入力方向の要求時に変換する新しい値 Administrators 出力方向の要求として送信される前にします。 詳細については、次を参照してください。[The Role of Claim Rules](The-Role-of-Claim-Rules.md)します。  
  
信頼性情報には、e\ メール アドレス、ユーザー プリンシパル名 \(UPN\)、グループ メンバーシップ、およびその他のアカウント属性などの値を含めることができます。  
  
### <a name="how-claims-flow"></a>信頼性情報のフロー  
その他の者は、それらがホストする Web ベース アプリケーションの承認タスクを実行する信頼性情報の値に依存します。 これらの利用者と呼びます*証明書利用者*の AD FS 管理スナップインでします。 フェデレーション サービスは多くの異なる利用者間の信頼を仲介します。 目的として処理し、最初にとも呼ばれ、信頼性情報を提供する組織からのクレームの信頼されている exchange のフロー*要求プロバイダー*で、AD FS の管理スナップイン、証明書利用者にします。 証明書利用者は、これらの要求を使用して承認を決定します。  
  
このプロセスを使用する要求のフローと呼ばれる、*要求パイプライン*します。 要求パイプラインを通過する要求のフローには、3 つの手順があります。  
  
1.  要求プロバイダーから受信した信頼性情報は、要求プロバイダー信頼の受付変換規則によって処理されます。 これらのルールは、要求プロバイダーから要求が受け付けられますを決定します。  
  
2.  受け入れ変換規則の出力は、発行承認規則の入力として使用されます。 これらのルールは、ユーザーは、証明書利用者にアクセスを許可するかどうかを決定します。  
  
3.  受け入れ変換規則の出力は、発行変換規則の入力として使用されます。 これらのルールでは、証明書利用者に送信される要求を決定します。  
  
詳細については、次を参照してください[要求パイプラインの役割。](The-Role-of-the-Claims-Pipeline.md)  
  
### <a name="how-claims-are-issued"></a>信頼性情報を発行する方法  
要求規則を記述するときに、要求規則の入力方向の要求のソースは、要求プロバイダー信頼または証明書利用者信頼の規則を作成するかどうかに基づいては異なります。 要求プロバイダー信頼の要求規則を記述する場合、入力方向の要求は、信頼される要求プロバイダーからフェデレーション サービスに送信される要求を使用します。 証明書利用者信頼の規則を記述する場合、入力方向の要求は、該当する要求プロバイダー信頼の要求規則によって出力される要求です。 入力方向の要求と出力方向の要求の詳細については、次を参照してください。[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)と[The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md)します。  
  
## <a name="what-are-claim-types"></a>要求の種類とは何ですか。  
要求の種類は、要求の値のコンテキストを提供します。 これは通常、Uniform Resource Identifier \(URI\) として表されます。 AD FS が、あらゆる種類の要求をサポートし、既定では、次の表に、要求の種類が構成します。  
  
|名|説明|URI|  
|--------|---------------|-------|  
|E\ メール アドレス|ユーザーの e\ メール アドレス|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/emailaddress|  
|指定された名前|ユーザーの姓名の名|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/givenname|  
|名|ユーザーの一意の名前|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/name|  
|UPN|ユーザー プリンシパル名、ユーザーの \(UPN\)|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/upn|  
|共通名|ユーザーの共通名|http:///\/schemas.xmlsoap.org\/claims\/CommonName|  
|AD FS 1.x E\ メール アドレス|AD FS 1.1 または ad FS 1.0 と相互運用するときのユーザーの e\ メール アドレス|http:///\/schemas.xmlsoap.org\/claims\/EmailAddress|  
|グループ|メンバーであるユーザーのグループ|http:///\/schemas.xmlsoap.org\/claims\/Group|  
|AD FS 1.x の UPN|AD FS 1.1 または ad FS 1.0 と相互運用する場合のユーザーの UPN|http:///\/schemas.xmlsoap.org\/claims\/UPN|  
|ロール|ユーザーが持っているロール|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/role|  
|姓|ユーザーの姓|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/surname|  
|PPID|ユーザーの個人識別子|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/privatepersonalidentifier|  
|名前識別子|ユーザーの SAML 名前識別子|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/nameidentifier|  
|認証方法|ユーザーの認証に使用する方法|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/authenticationmethod|  
|拒否専用グループ SID|ユーザーの deny\ 専用グループ SID|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/denyonlysid|  
|拒否専用プライマリ SID|ユーザーの deny\ 専用プライマリ SID|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/denyonlyprimarysid|  
|拒否専用プライマリ グループ SID|Deny\ 専用のプライマリ グループ SID ユーザー|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/denyonlyprimarygroupsid|  
|グループ SID|ユーザーのグループ SID|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/groupsid|  
|プライマリ グループ SID|ユーザーのプライマリ グループ SID|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/primarygroupsid|  
|プライマリ SID|ユーザーのプライマリ SID|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/primarysid|  
|Windows アカウント名|形式でユーザーのドメイン アカウント名<domain>\\<user>|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/windowsaccountname|  
  
## <a name="what-are-claim-descriptions"></a>要求記述とは何ですか。  
要求記述は、フェデレーション メタデータに公開が AD FS によってサポートされ、信頼性情報の種類の一覧を表します。 前の表に記載されている要求の種類は、AD FS 管理スナップインで要求記述として構成されます。  
  
フェデレーション メタデータに公開される要求記述のコレクションは、AD FS 構成データベースに格納されます。 これは、要求の説明は、フェデレーション サービスのさまざまなコンポーネントで使用します。  
  
各要求記述には、要求の種類の URI、名前、公開状態、および説明が含まれています。 使用して要求記述のコレクションを管理することができます、**要求記述**の AD FS 管理スナップイン内のノード。 スナップインを使用して、要求記述の公開状態を変更することができます。 次の設定を使用できます。  
  
-   **このフェデレーション サービスが受け付けることができる要求の種類としてこの要求をフェデレーション メタデータで公開**\(Publish as Accepted\) — このフェデレーション サービスで他の要求プロバイダーから受け付ける要求の種類を示します。  
  
-   **このフェデレーション サービスに送信できる要求の種類としてこの要求をフェデレーション メタデータで公開**\(Publish as Sent\) — このフェデレーション サービスによって提供される要求の種類を示します。 これらは、フェデレーション サービスがそれで送信するものとして公開する要求の種類です。 要求プロバイダーによって送信される実際の要求の種類は、多くの場合、このリストのサブセットです。  
  
詳細については、要求の種類の公開状態を設定する方法について、次を参照してください。[要求記述の追加](https://technet.microsoft.com/library/dd807051.aspx)AD FS 展開ガイドにします。  
  
### <a name="when-generating-federation-metadata"></a>フェデレーション メタデータの生成時  
フェデレーション メタデータには、発行用にマークされているすべての要求記述が含まれています。  
  
### <a name="when-claims-rules-are-processed"></a>要求規則が処理されます。  
要求記述に関する構成情報を保持するおくと、要求に関する規則を構成するための簡単です。 要求プロバイダー組織で使用できる要求規則の詳細については、次を参照してください。[、要求規則の役割](The-Role-of-Claim-Rules.md)します。  
  

