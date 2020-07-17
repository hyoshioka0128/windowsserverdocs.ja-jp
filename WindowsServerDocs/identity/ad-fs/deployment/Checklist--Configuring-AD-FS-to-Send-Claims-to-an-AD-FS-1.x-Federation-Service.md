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
ms.openlocfilehash: d522dddf99d71d8921db511af6f00488e424736e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854125"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>チェックリスト: AD FS 1.x のフェデレーション サービスに要求を送信するように AD FS を構成する

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-federation-service"></a>チェックリスト: AD FS 1.x フェデレーションサービスに要求を送信するように AD FS を構成する  
このチェックリストには、Active Directory フェデレーションサービス (AD FS) \(を構成するために必要なタスクが含まれています。このタスクは、Windows Server 2012 の\) フェデレーションサービス AD FS AD FS 1 で認識できる要求を送信するために使用します。*x*フェデレーションサービス。  
  
> [!NOTE]  
> このチェックリストに記載されているタスクを順番どおりに実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
要求を送信するための AD FS を構成する ![](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: AD FS 1.x に要求を送信するための AD FS の構成フェデレーションサービス**  
  
||タスク|参照|  
|-|--------|-------------|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|Windows Server 2012 と以前のバージョンの AD FS の AD FS 間の相互運用性を計画し、Name ID 要求の種類の詳細について説明します。|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1.x との相互運用性の要求の計画](https://technet.microsoft.com/library/ff678040.aspx)を送信するように AD FS を構成 ![には|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|以前のバージョンの AD FS との相互運用性を実現するには、まず AD FS 1 にフェデレーションサービス AD FS で証明書利用者の信頼を作成する必要があります。*x*フェデレーションサービス。 **注:** AD FS 1 を持つ信頼を作成することはできません。*x*フェデレーションサービスフェデレーションメタデータを使用します。<p>右側のリンクにある手順を使用して信頼を設定する場合は、証明書利用者信頼の追加ウィザードで次の操作を行って、AD FS 1 と相互運用するようにこの信頼を設定する必要があります。*x*フェデレーションサービス:<p>1. **[データソースの選択]** ページで、 **[証明書利用者の信頼に関するデータを手動で入力]** する を選択します。<br />2. **[プロファイルの選択]** ページで、 **[AD FS 1.0 および1.1 プロファイル]** を選択します。<br />3. **[URL の構成]** ページで、[ **WS\-フェデレーションパッシブ URL**] に、AD FS 1 で定義されている**フェデレーションサービスエンドポイント url**を入力します。パートナーの*x*フェデレーションサービス。<br />4. **[識別子の構成]** ページの **[証明書パーツ信頼識別子]** に、AD FS 1 で定義されている**フェデレーションサービス URI**を入力します。パートナーの*x*フェデレーションサービス。|要求を送信するように AD FS を構成 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[証明書利用者信頼を手動で作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)する|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|前の手順で作成した証明書利用者の信頼では、属性ストアから抽出された入力方向の要求を受け取り、それをパススルー、フィルター処理、または名前 ID 要求の種類に変換する要求規則を作成する必要があります。これは、AD FS 1 で理解して使用することができます。*x*フェデレーションサービス。 **注:** この規則を作成する前に、この規則を作成する要求規則セットに、まず、ライトウェイトディレクトリアクセスプロトコル \(LDAP\) 属性要求を属性ストアから抽出する規則が含まれていることを確認します。 この要求は、AD FS 1 を送信するために作成するルールへの入力として使用されます。*x*\-互換性のある要求です。 LDAP 属性を抽出するルールを作成する方法の詳細については、「 [Ldap 属性を要求として送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)する」を参照してください。|要求を送信するための AD FS を構成 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1. x 互換の要求を送信する規則を作成](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)する|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|AD FS 1 の管理者に連絡してください。*x*フェデレーションサービス、AD FS 1 の管理者がいます。*x*フェデレーションサービス新しいアカウントパートナー信頼を設定します。 また、管理者には、フェデレーションサービスプロパティ\)内のフェデレーションサービス URI \(、WS\-フェデレーションパッシブエンドポイント URL \(フェデレーションサービスエンドポイント URL\)、および公開キーのみ\-署名証明書ファイル \(署名証明書ファイル\)を指定します。 この管理者は、信頼を設定するためにこれらの項目を必要とします。|N\/A|  
  

