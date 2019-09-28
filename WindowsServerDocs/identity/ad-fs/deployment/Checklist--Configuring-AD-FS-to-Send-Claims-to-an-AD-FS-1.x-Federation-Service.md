---
ms.assetid: 4b81ac66-3f34-4a39-a8bf-5411131a69c2
title: チェックリスト-AD FS 1.x からの要求を使用するように AD FS を構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: f91944333da9ce4c1d78bbbf7b3652f1118e1f08
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408497"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>チェックリスト:AD FS 1.x フェデレーションサービスに要求を送信するように AD FS を構成する

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-federation-service"></a>チェックリスト:AD FS 1.x フェデレーションサービスに要求を送信するように AD FS を構成する  
このチェックリストには、Windows Server 2012 の Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 フェデレーションサービスを構成するために必要なタスクが含まれており、AD FS 1 で認識できる要求を送信します。*x*フェデレーションサービス。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![configure 要求を送信するように構成する @ no__t-1Checklist リスト:AD FS 1.x フェデレーションサービス @ no__t に要求を送信するように AD FS を構成する  
  
||タスク|参照|  
|-|--------|-------------|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|Windows Server 2012 と以前のバージョンの AD FS の AD FS 間の相互運用性を計画し、Name ID 要求の種類の詳細について説明します。|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0configure 1.x との相互運用性の要求の計画](https://technet.microsoft.com/library/ff678040.aspx)を送信するように AD FS を構成します。|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|以前のバージョンの AD FS との相互運用性を実現するには、まず AD FS 1 にフェデレーションサービス AD FS で証明書利用者の信頼を作成する必要があります。*x*フェデレーションサービス。 **注:** AD FS 1 を持つ信頼を作成することはできません。*x*フェデレーションサービスフェデレーションメタデータを使用します。<br /><br />右側のリンクにある手順を使用して信頼を設定する場合は、証明書利用者信頼の追加ウィザードで次の操作を行って、AD FS 1 と相互運用するようにこの信頼を設定する必要があります。*x*フェデレーションサービス:<br /><br />1. **[データソースの選択]** ページで、 **[証明書利用者の信頼に関するデータを手動で入力]** する を選択します。<br />2. **[プロファイルの選択]** ページで、 **[AD FS 1.0 および1.1 プロファイル]** を選択します。<br />3. **[URL の構成]** ページの **[WS @ No__t-2FEDERATION パッシブ URL]** に、AD FS 1 で定義されている**フェデレーションサービスエンドポイント URL**を入力します。パートナーの*x*フェデレーションサービス。<br />4。 **[識別子の構成]** ページの **[証明書パーツ信頼識別子]** に、AD FS 1 で定義されている**フェデレーションサービス URI**を入力します。パートナーの*x*フェデレーションサービス。|@no__t は、要求を送信するように AD FS を構成し、](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[証明書利用者信頼を手動で作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)します。|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|前の手順で作成した証明書利用者の信頼では、属性ストアから抽出された入力方向の要求を受け取る要求規則を作成し、AD によって認識および使用できる名前 ID 要求の種類にパススルー、フィルター処理、または変換します。FS 1.*x*フェデレーションサービス。 **注:** この規則を作成する前に、この規則を作成する要求規則セットに、まず、ライトウェイトディレクトリアクセスプロトコル \(LDAP @ no__t 属性の要求を属性ストアから抽出する前の規則が含まれていることを確認します。 この要求は、AD FS 1 を送信するために作成するルールへの入力として使用されます。*x*\- 互換要求。 LDAP 属性を抽出するルールを作成する方法の詳細については、「 [Ldap 属性を要求として送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)する」を参照してください。|![configure を構成して要求を送信する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1. x 互換の要求を送信する規則を作成](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)する|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|AD FS 1 の管理者に連絡してください。*x*フェデレーションサービス、AD FS 1 の管理者がいます。*x*フェデレーションサービス新しいアカウントパートナー信頼を設定します。 また、管理者にフェデレーションサービスプロパティ @ no__t で \(in WS @ no__t-2Federation パッシブエンドポイントの URL \(the エンドポイント URL @ no__t、およびエクスポートされたトークン @ no__ を使用して、フェデレーションサービス URI を指定します。\(with 証明書ファイル (公開キーのみ @ no__t-7)。 この管理者は、信頼を設定するためにこれらの項目を必要とします。|N\/A|  
  

