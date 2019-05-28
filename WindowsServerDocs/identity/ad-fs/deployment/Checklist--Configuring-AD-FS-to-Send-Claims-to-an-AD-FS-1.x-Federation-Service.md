---
ms.assetid: 4b81ac66-3f34-4a39-a8bf-5411131a69c2
title: AD FS からの要求を使用する AD FS の構成のチェックリスト - 1.x
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: bd4c436c806074f63bf51f497429532d7be32f75
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192407"
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-federation-service"></a>チェックリスト:AD FS 1.x のフェデレーション サービスに対するクレームを送信する AD FS を構成します。

  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-adfs1x-federation-service"></a>チェックリスト:AD FS の要求を送信する AD FS を構成する 1.x Federation Service  
このチェックリストには、Active Directory フェデレーション サービスを構成するために必要なタスクが含まれた\(AD FS\) 、AD FS 1 によって認識できる要求を送信する Windows Server 2012 でのフェデレーション サービス *。x*フェデレーション サービス。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![要求を送信する AD FS 構成](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。AD FS の要求を送信する AD FS を構成する 1.x Federation Service**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|Windows Server 2012 で AD FS と AD FS の以前のバージョン間の相互運用性の計画し、要求の種類の名前 ID の詳細について説明します。|![要求を送信する AD FS 構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS との相互運用の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|AD FS の以前のバージョンとの相互運用を行う前に、まず証明書利用者信頼を AD FS 1 に AD FS フェデレーション サービスを作成する必要があります。*x*フェデレーション サービス。 **注:** AD FS 1 で信頼を作成することはできません。*x*フェデレーション メタデータを使用してフェデレーション サービス。<br /><br />右へのリンクの手順を使用する信頼を設定すると、追加証明書利用者信頼のウィザード、AD FS 1 との相互運用するこの信頼を設定するでは、次を行う必要があります。*x*フェデレーション サービス。<br /><br />1. **データ ソースの選択**] ページで [**パーティの信頼の手動で証明書利用者に関するデータを入力**します。<br />2. **プロファイルの選択**] ページで、[ **AD FS 1.0 および 1.1 プロファイル**します。<br />3.**URL の構成**] ページ [ **WS\-フェデレーション パッシブ URL**、型、**フェデレーション サービス エンドポイントの URL** AD FS 1 で定義されている *。x*パートナーのフェデレーション サービス。<br />4。**識別子の構成**] ページ [**部分信頼の証明書利用者識別子**、型、**フェデレーション サービスの URI** AD FS 1 で定義されている *。x*パートナーのフェデレーション サービス。|![要求を送信する AD FS 構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[証明書利用者信頼を手動で作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|先ほど作成した証明書利用者のパーティ信頼に要求が属性ストアから抽出された入力方向の要求を実行しを通過、フィルター処理、または名前 ID に変換される規則の要求の種類を理解し、AD によって消費されることができますを作成する必要があります。FS 1。*x*フェデレーション サービス。 **注:** このルールを作成する前にこの規則を作成する要求規則セットに最初に、ライトウェイト ディレクトリ アクセス プロトコルを抽出する前に、ルールがあること確認\(LDAP\)属性ストアからの要求を属性。 この要求は、AD FS 1 を送信するために作成するルールを入力として使用されます。*x*\-互換の要求。 LDAP 属性を抽出するルールを作成する方法の詳細については、次を参照してください。[要求として LDAP 属性を送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)です。|![要求を送信する AD FS 構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS を送信するルールを作成する 1.x 互換の要求](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|AD FS 1 の管理者に問い合わせてください。*x*フェデレーション サービスと AD FS 1 の管理者を持っている *。x*フェデレーション サービスは、新しいアカウント パートナーの信頼を設定します。 また、その管理者をフェデレーション サービスの URI を提供\(フェデレーション サービスのプロパティで\)、WS\-フェデレーション パッシブ エンドポイント URL\(フェデレーション サービス エンドポイントの URL\)、エクスポートされたトークン\-署名証明書ファイル\(公開キーのみで\)します。 その管理者は、これらの項目の信頼を設定する必要があります。|N\/A|  
  

