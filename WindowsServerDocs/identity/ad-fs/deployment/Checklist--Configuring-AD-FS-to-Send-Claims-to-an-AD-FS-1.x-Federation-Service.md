---
ms.assetid: 4b81ac66-3f34-4a39-a8bf-5411131a69c2
title: チェックリスト-AD FS 1.x からの要求を使用するように AD FS を構成する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ae281640ac7e404ddf99ba10785a8828573722d9
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86959384"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>チェックリスト: AD FS 1.x のフェデレーション サービスに要求を送信するように AD FS を構成する

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-federation-service"></a>チェックリスト: AD FS 1.x フェデレーションサービスに要求を送信するように AD FS を構成する  
このチェックリストには、 \( \) AD FS 1 で認識できる要求を送信するために、Windows Server 2012 で Active Directory フェデレーションサービス (AD FS) AD FS フェデレーションサービスを構成するために必要なタスクが含まれています。*x*フェデレーションサービス。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![要求を送信するように AD FS を構成する](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: AD FS 1.x に要求を送信するための AD FS の構成フェデレーションサービス**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|Windows Server 2012 と以前のバージョンの AD FS の AD FS 間の相互運用性を計画し、Name ID 要求の種類の詳細について説明します。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1.x との相互運用性の要求計画](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678040(v=ws.11))を送信するように AD FS を構成する|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|以前のバージョンの AD FS との相互運用性を実現するには、まず AD FS 1 にフェデレーションサービス AD FS で証明書利用者の信頼を作成する必要があります。*x*フェデレーションサービス。 **注:** AD FS 1 を持つ信頼を作成することはできません。*x*フェデレーションサービスフェデレーションメタデータを使用します。<p>右側のリンクにある手順を使用して信頼を設定する場合は、証明書利用者信頼の追加ウィザードで次の操作を行って、AD FS 1 と相互運用するようにこの信頼を設定する必要があります。*x*フェデレーションサービス:<p>1. [**データソースの選択**] ページで、[**証明書利用者の信頼に関するデータを手動で入力**する] を選択します。<br />2. [**プロファイルの選択**] ページで、[ **AD FS 1.0 および1.1 プロファイル**] を選択します。<br />3. [ **URL の構成**] ページの [ **ws-federation \- パッシブ URL**] に、AD FS 1 **Federation Service endpoint URL** *で定義されているフェデレーションサービスエンドポイント URL を入力します。* パートナーの x フェデレーションサービス。<br />4. [**識別子の構成**] ページの [**証明書パーツ信頼識別子**] に、AD FS 1 で定義されている**フェデレーションサービス URI**を入力します。パートナーの*x*フェデレーションサービス。|![要求を送信するように AD FS を構成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[証明書利用者信頼を手動で作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)する|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|前の手順で作成した証明書利用者の信頼では、属性ストアから抽出された入力方向の要求を受け取り、それをパススルー、フィルター処理、または名前 ID 要求の種類に変換する要求規則を作成する必要があります。これは、AD FS 1 で理解して使用することができます。*x*フェデレーションサービス。 **注:** この規則を作成する前に、この規則を作成する要求規則セットに、最初に、ライトウェイトディレクトリアクセスプロトコル \( LDAP \) 属性要求を属性ストアから抽出する前の規則があることを確認してください。 この要求は、AD FS 1 を送信するために作成するルールへの入力として使用されます。*x* \-互換性のある要求。 LDAP 属性を抽出するルールを作成する方法の詳細については、「 [Ldap 属性を要求として送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)する」を参照してください。|![要求を送信するように AD FS を構成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1. x 互換の要求を送信する規則を作成](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)する|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|AD FS 1 の管理者に連絡してください。*x*フェデレーションサービス、AD FS 1 の管理者がいます。*x*フェデレーションサービス新しいアカウントパートナー信頼を設定します。 また、フェデレーションサービスプロパティのフェデレーションサービス URI、 \( \) WS \- フェデレーションパッシブエンドポイント url \( フェデレーションサービスエンドポイント url、 \) および \- \( 公開キーのみを含むエクスポートされたトークン署名証明書ファイル \) を管理者に提供します。 この管理者は、信頼を設定するためにこれらの項目を必要とします。|N\/A|  
  
