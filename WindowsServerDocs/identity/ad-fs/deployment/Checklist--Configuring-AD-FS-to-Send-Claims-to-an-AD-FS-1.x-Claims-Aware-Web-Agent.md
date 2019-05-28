---
ms.assetid: 551c1a0d-8d30-41b4-9c4a-35a3337dd3bc
title: フェデレーション サーバーの展開
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 874984b469303c0f8a40a676632c144ee6079f44
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192430"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>チェックリスト:AD FS 1.x Claims-aware Web エージェントを要求を送信する AD FS を構成します。

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-claims-aware-web-agent"></a>チェックリスト:AD FS 1.x の要求に要求を送信する AD FS を構成する\-対応する Web エージェント  
このチェックリストには、Active Directory フェデレーション サービスを構成するために必要なタスクが含まれた\(AD FS\)フェデレーション サービスによってホストされているアプリケーションによって認識できる要求を送信する Windows Server 2012 で、Web サーバーが AD FS 1 を実行します。*x*クレーム\-対応する Web エージェントです。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![要求を送信する AD FS 構成](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。AD FS 1.x の要求に要求を送信する AD FS を構成する\-対応する Web エージェント**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|Windows Server 2012 で AD FS と AD FS の以前のバージョン間の相互運用性の計画し、要求の種類の名前 ID の詳細について説明します。|![要求を送信する AD FS 構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS との相互運用の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|されていない場合は、まず Windows Server 2012 で AD FS フェデレーション サービスと AD FS 1 の間の証明書利用者信頼を作成する、右側のリンクを使用します。*x*フェデレーション サービス。|[チェックリスト:AD FS 1.x のフェデレーション サービスに要求を送信するように AD FS を構成する](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|前に、AD FS 1 によってホストされているアプリケーションとの相互運用を実現できます。*x*クレーム\-認識 Web エージェントをする必要がありますで初めて作成する証明書利用者信頼を AD FS のフェデレーション サービスで AD FS 1 に、Windows Server 2012。 *x*クレーム\-対応する Web エージェントです。 **注:** 新しいを追加するのと同じでは、AD FS フェデレーション サービスでは、この信頼を作成する**アプリケーション**を AD FS 1.x Federation Service \(**フェデレーション サービス\\信頼ポリシー\\自分の所属組織\\アプリケーション**\)します。 AD FS に相当するがあるないために、この証明書利用者の信頼が必要な**アプリケーション**独自スナップイン内のノード\-でします。 ただし、まだが必要、アプリケーションをセキュリティで保護されたチャネルです。<br /><br />右へのリンクの手順を使用する信頼を設定すると、追加証明書利用者信頼のウィザード、AD FS 1 との相互運用するこの信頼を設定するでは、次を行う必要があります。*x*クレーム\-対応する Web エージェント。<br /><br />1. **データ ソースの選択**] ページで [**パーティの信頼の手動で証明書利用者に関するデータを入力**します。<br />2. **プロファイルの選択**] ページで、[ **AD FS 1.0 および 1.1 プロファイル**します。<br />3.**URL の構成**] ページ [ **WS\-フェデレーション パッシブ URL**、型、**アプリケーションの URL** AD FS 1 で定義されている *。x*パートナーのフェデレーション サービス。<br />4。**識別子の構成**] ページ [**部分信頼の証明書利用者識別子**、型、**アプリケーションの URL** AD FS 1 で定義されている *。x*クレーム\-対応する Web エージェント|![要求を送信する AD FS 構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[証明書利用者信頼を手動で作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|AD FS 1 を実行している Web サーバーの管理者に問い合わせてください。*x*クレーム\-認識 Web エージェントとその管理者に依頼して、要求に関連付けられている web.config ファイルを編集\-対応のアプリケーション\(インターネット インフォメーションにおける既定の Web サイトの下サービス\(IIS\) \) AD FS フェデレーション サービス、Web エージェントをポイントします。<br /><br />たとえば、置換*myresourcefederationserver*タグで`<fs> https://myresourcefederationserver/adfs/fs/federationserverservice.asmx</fs>`の有効な AD FS フェデレーション サーバー名を含む web.config ファイル。<br /><br />これは、アプリケーションと AD FS 1.x の要求に必要な\-対応する Web エージェントを Windows Server 2012 で AD FS フェデレーション サービスから送信される要求を使用できるようにします。|N\/A|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|先ほど作成したパーティの証明書利用者信頼では、属性ストアから抽出された入力方向の要求の実行し通過、フィルター処理、またはによって消費され、認識が可能な名前 ID 要求の種類に変換される要求規則を作成する必要が、AD FS 1。*x*クレーム\-対応する Web エージェントです。 **注:** このルールを作成する前にこの規則を作成する要求規則セットに最初に、ライトウェイト ディレクトリ アクセス プロトコルを抽出する前に、ルールがあること確認\(LDAP\)属性ストアからの要求を属性。 この要求は、AD FS 1 を送信するために作成するルールを入力として使用されます。*x*\-互換の要求。 LDAP 属性を抽出するルールを作成する方法の詳細については、次を参照してください。[要求として LDAP 属性を送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)です。|![要求を送信する AD FS 構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS を送信するルールを作成する 1.x 互換の要求](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
  

