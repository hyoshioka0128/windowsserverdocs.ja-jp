---
ms.assetid: 551c1a0d-8d30-41b4-9c4a-35a3337dd3bc
title: フェデレーション サーバーの展開
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 9f5b67c15c367121998f940d428a997af9ae13d5
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955594"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>チェックリスト: AD FS 1.x の要求に対応する Web エージェントに要求を送信するように AD FS を構成する

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-claims-aware-web-agent"></a>チェックリスト: AD FS 1. x 要求に \- 対応する Web エージェントに要求を送信するように AD FS を構成する  
このチェックリストには、AD FS 1 を実行して \( いる \) Web サーバーでホストされているアプリケーションで認識できる要求を送信するために、Windows Server 2012 でフェデレーションサービス AD FS Active Directory フェデレーションサービス (AD FS) を構成するために必要なタスクが含まれています。*x*要求に \- 対応する Web エージェント。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![要求を送信するように AD FS を構成する](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: AD FS 1.x 要求に対応する \- Web エージェントに要求を送信するための AD FS の構成**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|Windows Server 2012 と以前のバージョンの AD FS の AD FS 間の相互運用性を計画し、Name ID 要求の種類の詳細について説明します。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1.x との相互運用性の要求計画](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678040(v=ws.11))を送信するように AD FS を構成する|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|この操作をまだ行っていない場合は、右側のリンクを使用して、最初に Windows Server 2012 の AD FS フェデレーションサービスと AD FS 1 の間に証明書利用者の信頼を作成します。*x*フェデレーションサービス。|[チェックリスト:AD FS 1.x のフェデレーション サービスに要求を送信するように AD FS を構成する](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|AD FS 1 でホストされているアプリケーションとの相互運用を実現する前に。*x*要求に \- 対応する Web エージェントでは、最初に Windows Server 2012 の AD FS フェデレーションサービスで AD FS 1 に証明書利用者信頼を作成する必要があります。 *x*要求に \- 対応する Web エージェント。 **注:** AD FS フェデレーションサービスでこの信頼を作成することは、AD FS 1.x フェデレーションサービス**Application** \( **フェデレーションサービス \\ 信頼ポリシーの \\ 組織 \\ アプリケーション**に新しいアプリケーションを追加することに相当し \) ます。 この証明書利用者信頼が必要になるのは、AD FS がそれ自体のスナップインに同等の**アプリケーション**ノードを持っていないためです \- 。 ただし、アプリケーションにはセキュリティで保護されたチャネルが必要です。<p>右側のリンクにある手順を使用して信頼を設定する場合は、証明書利用者信頼の追加ウィザードで次の操作を行って、AD FS 1 と相互運用するようにこの信頼を設定する必要があります。*x*要求に \- 対応する Web エージェント:<p>1. [**データソースの選択**] ページで、[**証明書利用者の信頼に関するデータを手動で入力**する] を選択します。<br />2. [**プロファイルの選択**] ページで、[ **AD FS 1.0 および1.1 プロファイル**] を選択します。<br />3. [ **URL の構成**] ページの [ **ws-federation \- パッシブ URL**] に、AD FS 1 **Application URL** *で定義されているアプリケーションの URL を入力します。* パートナーの x フェデレーションサービス。<br />4. [**識別子の構成**] ページの [**証明書パーツ信頼識別子**] に、AD FS 1 で定義されている**アプリケーションの URL**を入力します。*x*要求に \- 対応する Web エージェント|![要求を送信するように AD FS を構成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[証明書利用者信頼を手動で作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)する|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|AD FS 1 を実行している Web サーバーの管理者に問い合わせてください。*x*要求 \- に対応する web エージェント。管理者は、インターネットインフォメーションサービス IIS の既定の web サイトにある要求対応アプリケーションに関連付けられている web.config ファイルを編集して、 \- \( \( \) \) AD FS フェデレーションサービスで Web エージェントをポイントするようにします。<p>たとえば、web.config ファイルのタグの*myresourcefederationserver*を、 `<fs>https://myresourcefederationserver/adfs/fs/federationserverservice.asmx</fs>` 有効な AD FS フェデレーションサーバー名に置き換えます。<p>これは、アプリケーションと AD FS 1. x 要求に \- 対応する Web エージェントが、Windows Server 2012 の AD FS フェデレーションサービスから送信された要求を使用できるようにするために必要です。|N\/A|  
|![要求を送信するように AD FS を構成する](media/icon_checkboxo.gif)|前の手順で作成した証明書利用者の信頼では、属性ストアから抽出された入力方向の要求を受け取る要求規則を作成し、AD FS 1 で認識および使用できる名前 ID 要求の種類にパススルー、フィルター処理、または変換します。*x*要求に \- 対応する Web エージェント。 **注:** この規則を作成する前に、この規則を作成する要求規則セットに、最初に、ライトウェイトディレクトリアクセスプロトコル \( LDAP \) 属性要求を属性ストアから抽出する前の規則があることを確認してください。 この要求は、AD FS 1 を送信するために作成するルールへの入力として使用されます。*x* \-互換性のある要求。 LDAP 属性を抽出するルールを作成する方法の詳細については、「 [Ldap 属性を要求として送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)する」を参照してください。|![要求を送信するように AD FS を構成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1. x 互換の要求を送信する規則を作成](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)する|  
  
