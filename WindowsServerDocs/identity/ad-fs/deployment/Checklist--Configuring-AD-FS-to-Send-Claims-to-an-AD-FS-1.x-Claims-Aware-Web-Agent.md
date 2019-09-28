---
ms.assetid: 551c1a0d-8d30-41b4-9c4a-35a3337dd3bc
title: フェデレーション サーバーの展開
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 689bd33bc95c2b142dfbe6d0448a604b2971979e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359980"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>チェックリスト:AD FS 1. x 要求に対応する Web エージェントに要求を送信するように AD FS を構成する

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-claims-aware-web-agent"></a>チェックリスト:AD FS 1.x クレーム @ no__t に対応する Web エージェントに要求を送信するように AD FS を構成する  
このチェックリストには、Windows Server 2012 の Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 フェデレーションサービスを構成するために必要なタスクが含まれています。このタスクは、Web サーバーでホストされているアプリケーションによって認識される要求を送信します。AD FS 1 を実行しています。*x*要求 @ no__t-3Aware Web エージェント。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![configure 要求を送信するように構成する @ no__t-1Checklist リスト:AD FS 1.x のクレームに要求を送信するように AD FS を構成する @ no__t-0aware Web エージェント @ no__t-1  
  
||タスク|参照|  
|-|--------|-------------|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|Windows Server 2012 と以前のバージョンの AD FS の AD FS 間の相互運用性を計画し、Name ID 要求の種類の詳細について説明します。|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0configure 1.x との相互運用性の要求の計画](https://technet.microsoft.com/library/ff678040.aspx)を送信するように AD FS を構成します。|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|この操作をまだ行っていない場合は、右側のリンクを使用して、最初に Windows Server 2012 の AD FS フェデレーションサービスと AD FS 1 の間に証明書利用者の信頼を作成します。*x*フェデレーションサービス。|[チェックリスト:AD FS 1.x のフェデレーション サービスに要求を送信するように AD FS を構成する](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|AD FS 1 でホストされているアプリケーションとの相互運用を実現する前に。*x*要求 @ no__t-1 対応の Web エージェントでは、最初に Windows Server 2012 の AD FS フェデレーションサービスで AD FS 1 に証明書利用者信頼を作成する必要があります。 *x*要求 @ no__t-1 対応 Web エージェント。 **注:** AD FS フェデレーションサービスでこの信頼を作成することは、AD FS 1.x フェデレーションサービス \(**フェデレーションサービス @ no__t-3Trust ポリシー @ no__t-4My Organization @ no__t-5Application**\) に新しい**アプリケーション**を追加することに相当します。 この証明書利用者の信頼は、AD FS が独自のスナップ @ no__t に同等の**アプリケーション**ノードを持っていないために必要です。 ただし、アプリケーションにはセキュリティで保護されたチャネルが必要です。<br /><br />右側のリンクにある手順を使用して信頼を設定する場合は、証明書利用者信頼の追加ウィザードで次の操作を行って、AD FS 1 と相互運用するようにこの信頼を設定する必要があります。*x*要求 @ no__t-1 対応 Web エージェント:<br /><br />1. **[データソースの選択]** ページで、 **[証明書利用者の信頼に関するデータを手動で入力]** する を選択します。<br />2. **[プロファイルの選択]** ページで、 **[AD FS 1.0 および1.1 プロファイル]** を選択します。<br />3. **[URL の構成]** ページの **[WS @ No__t-2FEDERATION パッシブ URL]** に、AD FS 1 で定義されているアプリケーションの**URL**を入力します。パートナーの*x*フェデレーションサービス。<br />4。 **[識別子の構成]** ページの **[証明書パーツ信頼識別子]** に、AD FS 1 で定義されている**アプリケーションの URL**を入力します。*x*要求 @ no__t-4Aware Web エージェント|@no__t は、要求を送信するように AD FS を構成し、](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[証明書利用者信頼を手動で作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)します。|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|AD FS 1 を実行している Web サーバーの管理者に問い合わせてください。*x*要求 @ no__t-1 を認識する web エージェントで、no__t インターネットインフォメーションサービスの既定の web サイトの下にある要求 @-2aware @no__t アプリケーションに関連付けられている web.config ファイルを編集するには \(iis @ no__t-5 @ no__t-6AD FS フェデレーションサービスで Web エージェントをポイントします。<br /><br />たとえば、web.config ファイルのタグ `<fs> https://myresourcefederationserver/adfs/fs/federationserverservice.asmx</fs>` の*myresourcefederationserver*を、有効な AD FS フェデレーションサーバー名に置き換えます。<br /><br />これは、アプリケーションと AD FS 1.x の要求 @ no__t に対応する Web エージェントが、Windows Server 2012 の AD FS フェデレーションサービスから送信された要求を使用できるようにするために必要です。|N\/A|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|前の手順で作成した証明書利用者の信頼では、属性ストアから抽出された入力方向の要求を受け取る要求規則を作成する必要があります。これにより、これらの要求は、AD FS 1 です。*x*要求 @ no__t-1 対応 Web エージェント。 **注:** この規則を作成する前に、この規則を作成する要求規則セットに、まず、ライトウェイトディレクトリアクセスプロトコル \(LDAP @ no__t 属性の要求を属性ストアから抽出する前の規則が含まれていることを確認します。 この要求は、AD FS 1 を送信するために作成するルールへの入力として使用されます。*x*\- 互換要求。 LDAP 属性を抽出するルールを作成する方法の詳細については、「 [Ldap 属性を要求として送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)する」を参照してください。|![configure を構成して要求を送信する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1. x 互換の要求を送信する規則を作成](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)する|  
  

