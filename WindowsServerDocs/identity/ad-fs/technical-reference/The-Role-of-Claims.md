---
ms.assetid: 22f53391-8c6a-4873-a1f4-08b4760ea621
title: 要求の役割
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 851a70bbed606530ca8292f65bc4f776eae77fae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407340"
---
# <a name="the-role-of-claims"></a>要求の役割
要求 @ no__t-0based id モデルでは、要求はフェデレーションプロセスで非常に重要な役割を果たします。これは、すべての Web @ no__t ベースの認証および承認要求の結果が決定される主要なコンポーネントです。 このモデルを使用することで、組織はデジタル ID とアクセス権、つまり*要求*をセキュリティや企業の境界を越えて、標準化された方法で安全に提示できるようになります。  
  
## <a name="what-are-claims"></a>要求とは  
最も単純な形式では、要求は単に1つの*ステートメント*@no__t します。たとえば、ユーザーに関しては、ユーザーに対して作成された name、identity、group @ no__t-2 などです。これは主に、インターネット上の任意の場所にある要求 @ no__t ベースのアプリケーションへのアクセスを承認するために使用されます。 各ステートメントは、要求に格納される*値*に対応します。  
  
### <a name="how-claims-are-sourced"></a>要求の提供元  
フェデレーションサービス Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 では、フェデレーションパートナー間で交換される要求を定義します。 ただし、この定義を行う前に、取得または計算された値を要求に格納または提供する必要があります。 各要求の値は、ユーザー、グループ、またはエンティティの値を表し、次の 2 つのいずれかの方法で提供されます。  
  
1.  要求を構成する値が属性ストアから取得される場合。たとえば、属性値 Sales Department が Active Directory ユーザー アカウントのプロパティから取得されるような場合です。 詳細については、「[属性ストアの役割](The-Role-of-Attribute-Stores.md)」を参照してください。  
  
2.  入力方向の要求の値が、規則で表されているロジックに基づいて別の値に変換される場合。 たとえば、入力方向の要求に含まれる Domain Admins という値が、出力方向の要求として送信される前に新しい値 Administrators に変換されるような場合です。 詳細については、「[要求規則の役割](The-Role-of-Claim-Rules.md)」を参照してください。  
  
要求には、e @ no__t-0mail アドレス、ユーザープリンシパル名 \( UPN @ no__t-2、グループメンバーシップ、およびその他のアカウント属性などの値を含めることができます。  
  
### <a name="how-claims-flow"></a>要求のフロー  
他の当事者は、要求の値に基づいて、ホストする Web @ no__t ベースのアプリケーションの承認タスクを実行します。 これらのパーティは、*証明書利用者*と呼ばれ、AD FS 管理スナップ @ no__t から参照されます。 フェデレーションサービスは、多数の異なるパーティ間で信頼を仲介する役割を担います。 これは、要求を最初に送信する組織 (AD FS 管理スナップ @ no__t-1 で要求*プロバイダー*とも呼ばれます) から証明書利用者への信頼性のある要求の交換を処理およびフローするように設計されています。 証明書利用者は、受け取った要求を使用して承認の判断を下します。  
  
このようなプロセスを実行する要求のフローを*要求パイプライン*と呼びます。 要求パイプラインでの要求のフローは、次の 3 つのステップから構成されます。  
  
1.  要求プロバイダーから受け取った要求は、要求プロバイダー信頼の受け入れ変換規則によって処理されます。 これらの規則は、要求プロバイダーから受け入れる要求を決定します。  
  
2.  受け入れ変換規則の出力は、発行承認規則の入力として使用されます。 これらの規則は、ユーザーが証明書利用者へのアクセスを許可されるかどうかを決定します。  
  
3.  受け入れ変換規則の出力は、発行変換規則の入力として使用されます。 これらの規則は、証明書利用者に送信される要求を決定します。  
  
詳細については、「[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)」を参照してください。  
  
### <a name="how-claims-are-issued"></a>要求の発行  
要求規則を記述する場合、要求規則の入力方向の要求のソースは、要求プロバイダー信頼または証明書利用者信頼のどちらの規則を記述するかによって異なります。 要求プロバイダー信頼の要求規則を記述する場合、入力方向の要求は、信頼される要求プロバイダーからフェデレーション サービスに送信される要求です。 証明書利用者信頼の規則を記述する場合、入力方向の要求は、該当する要求プロバイダー信頼の要求規則によって出力される要求です。 入力方向と出力方向の要求に関する詳細については、「[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)」および「[要求エンジンの役割](The-Role-of-the-Claims-Engine.md)」を参照してください。  
  
## <a name="what-are-claim-types"></a>要求の種類とは  
要求の種類は、要求の値のコンテキストを提供します。 通常は、Uniform Resource Identifier \(URI @ no__t-1 として表されます。 AD FS は任意の要求の種類をサポートでき、既定では次の表の要求の種類で構成されます。  
  
|名前|説明|URI|  
|--------|---------------|-------|  
|E @ no__t-0Mail アドレス|ユーザーの e @ no__t-0mail アドレス|http: \/\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7emailaddress|  
|名|ユーザーの姓名の名|http: \/\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7givenname|  
|名前|ユーザーの一意の名前|http: \/\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7name|  
|UPN|ユーザーのユーザープリンシパル名 \(UPN @ no__t-1|http: \/\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7upn|  
|共通名|ユーザーの共通名|http: \/\/schemas.xmlsoap.org @ no__t-2claims @ no__t-3CommonName|  
|AD FS 1.x E @ no__t-0Mail アドレス|AD FS 1.1 または ADFS 1.0 と相互運用するときのユーザーの e @ no__t-0mail アドレス|http: \/\/schemas.xmlsoap.org @ no__t-2claims @ no__t-3EmailAddress|  
|グループ|ユーザーが属するグループ|http: \/\/schemas.xmlsoap.org @ no__t-2claims @ no__t-3Group|  
|AD FS 1.x UPN|AD FS 1.1 または AD FS 1.0 と相互運用するときのユーザーの UPN|http: \/\/schemas.xmlsoap.org @ no__t-2claims @ no__t-3UPN|  
|ロール|ユーザーの役割|http: \/\/schemas.microsoft.com @ no__t-2ws @ 32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7role|  
|姓|ユーザーの姓名の姓|http: \/\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7surname|  
|PPID|ユーザーの個人識別子|http: \/\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7privatepersonalidentifier|  
|名前識別子|ユーザーの SAML 名前識別子|http: \/\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7nameidentifier|  
|認証方法|ユーザー認証に使用される方法|http: \/\/schemas.microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7authenticationmethod|  
|拒否専用グループ SID|ユーザーの deny @ no__t-0only グループ SID|http: \/\/schemas.xmlsoap.org @ no__t-2ws @ no__t-32005 @ no__t-405 @ no__t-5identity @ no__t-6claims @ no__t-7denyonlysid|  
|拒否専用プライマリ SID|ユーザーの deny @ no__t-0only プライマリ SID|http: \/\/schemas.microsoft.com @ no__t-2ws @ 32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7denyonlyprimarysid|  
|拒否専用プライマリ グループ SID|ユーザーの deny @ no__t-0only プライマリグループ SID|http: \/\/schemas.microsoft.com @ no__t-2ws @ 32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7denyonlyprimarygroupsid|  
|グループ SID|ユーザーのグループ SID|http: \/\/schemas.microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7groupsid|  
|プライマリ グループ SID|ユーザーのプライマリ グループ SID|http: \/\/schemas.microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7primarygroupsid|  
|プライマリ SID|ユーザーのプライマリ SID|http: \/\/schemas.microsoft.com @ no__t-2ws @ 32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7primarysid|  
|Windows アカウント名|ユーザーのドメインアカウント名を \<domain @ no__t の形式で指定します。 @ no__t @ no__t @ no__t-4|http: \/\/schemas.microsoft.com @ no__t-2ws @ no__t-32008 @ no__t-406 @ no__t-5identity @ no__t-6claims @ no__t-7windowsaccountname|  
  
## <a name="what-are-claim-descriptions"></a>要求記述とは  
要求の説明は、AD FS がサポートしていて、フェデレーションメタデータで公開できる要求の種類の一覧を表します。 前の表に記載されている要求の種類は、AD FS 管理スナップインの @ no__t-0in 要求の説明として構成されています。  
  
フェデレーション メタデータに公開される要求記述のコレクションは、AD FS 構成データベースに格納されます。 これらの要求記述は、フェデレーション サービスのさまざまなコンポーネントで使用されます。  
  
各要求記述には、要求の種類の URI、名前、公開状態、および説明が含まれています。 要求記述のコレクションを管理するには、AD FS Management snap @ no__t の **[要求の説明]** ノードを使用します。 のスナップ @ no__t を使用して、要求の説明の発行状態を変更できます。 次の設定を使用できます。  
  
-   この**フェデレーションサービス @no__t が受け入れ可能な要求の種類としてフェデレーションメタデータにこの要求を発行**します。 @ no__t-2-このフェデレーションサービスによって他の要求プロバイダーから受け入れられる要求の種類を示します。  
  
-   この**フェデレーションサービスが送信できる要求の種類として、この要求をフェデレーションメタデータに発行**します。送信された \( は、このフェデレーションサービスによって提供される要求の種類を示します。 これらは、フェデレーション サービスが送信できる要求として公開する要求の種類です。 要求プロバイダーによって送信される実際の要求の種類は、多くの場合、このリストのサブセットとなります。  
  
要求の種類の公開状態を設定する方法の詳細については、AD FS デプロイガイドの「[要求の説明を追加](https://technet.microsoft.com/library/dd807051.aspx)する」を参照してください。  
  
### <a name="when-generating-federation-metadata"></a>フェデレーション メタデータの生成  
フェデレーション メタデータには、公開対象としてマークされているすべての要求記述が含まれます。  
  
### <a name="when-claims-rules-are-processed"></a>要求規則の処理  
要求記述に関する構成情報を保持しておくと、要求に関する規則を簡単に構成できます。 要求プロバイダー組織で使用できる要求規則の詳細については、「[要求規則の役割](The-Role-of-Claim-Rules.md)」を参照してください。  
  

