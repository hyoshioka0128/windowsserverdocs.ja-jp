---
ms.assetid: e7f9e518-2d5d-4a0d-9147-34e1304f42ac
title: AD FS からの要求を使用する AD FS の構成のチェックリスト - 1.x
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: fe99487d3a770547af36f69722b442d0e2cbb8b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828293"
---
# <a name="checklist-configuring-ad-fs--to-consume-claims-from-ad-fs-1x"></a>チェックリスト:Configuring AD FS からの要求を使用する AD FS 1.x

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-consume-claims-from-adfs1x"></a>チェックリスト:Configuring AD FS からの要求を使用する AD FS 1.x  
このチェックリストには、Active Directory フェデレーション サービスを構成するために必要なタスクが含まれた\(AD FS\) 、AD FS 1 によって送信される要求を使用する Windows Server 2012 でのフェデレーション サービス *。x*フェデレーション サービス。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![AD FS からの要求を消費する](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。Configuring AD FS からの要求を使用する AD FS 1.x**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![AD FS からの要求を使用します。](media/icon_checkboxo.gif)|Windows Server 2012 で AD FS と AD FS の以前のバージョン間の相互運用性の計画し、要求の種類の名前 ID の詳細について説明します。|![AD FS からの要求を消費する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS との相互運用の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![AD FS からの要求を使用します。](media/icon_checkboxo.gif)|AD FS の以前のバージョンと相互運用することができます、前にまず、AD FS フェデレーション サービスの要求プロバイダー信頼を作成する必要があります。 **注:** AD FS 1 で信頼を作成することはできません。*x*フェデレーション メタデータを使用してフェデレーション サービス。<br /><br />右へのリンクの手順を使用する信頼を設定するときの追加要求プロバイダー信頼ウィザードで AD FS 1 との相互運用するこの信頼を設定する、次を行う必要があります。*x*フェデレーション サービス。<br /><br />1. **データ ソースの選択**] ページで [**パーティの信頼の手動で証明書利用者に関するデータを入力**します。<br />2. **プロファイルの選択**] ページで、[ **AD FS 1.0 および 1.1 プロファイル**します。<br />3.**URL の構成**] ページ [ **WS\-フェデレーション パッシブ URL**、型、**フェデレーション サービス エンドポイントの URL** AD FS 1 で定義されている *。x*パートナーのフェデレーション サービス。<br />4。**識別子の構成**] ページ [**要求プロバイダー信頼の識別子**、型、**フェデレーション サービスの URI** AD FS 1 で定義されている *。x*パートナーのフェデレーション サービス。|![AD FS からの要求を消費する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求プロバイダー信頼を手動で作成](../../ad-fs/operations/Create-a-Claims-Provider-Trust.md)|  
|![AD FS からの要求を使用します。](media/icon_checkboxo.gif)|先ほど作成した要求プロバイダー信頼を作成する必要がある要求規則を AD FS からの入力方向の要求になります 1.x Federation Service と、パススルー フィルター処理、または名前 ID 要求の種類に変換します。<br /><br />フィルター処理または変換されるため、名前 ID 要求の種類に渡されたときに理解して Windows Server 2012 で AD FS フェデレーション サービスで使用できるように別のルールまたはルールへの入力として使用できます。|![AD FS からの要求を消費する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS を送信するルールを作成する 1.x 互換の要求](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![AD FS からの要求を使用します。](media/icon_checkboxo.gif)|AD FS 1 の管理者に問い合わせてください。*x*フェデレーション サービスと AD FS 1 の管理者を持っている *。x*フェデレーション サービスは、新しいリソース パートナーの信頼を設定します。 また、その管理者をフェデレーション サービスの URI を提供\(フェデレーション サービスのプロパティで\)、フェデレーション サービス エンドポイントの URL と、エクスポートされたトークン\-署名証明書ファイル\(で公開キーのみ\)します。 管理者は、これらの項目の信頼を設定する必要があります。|N\/A|  
  

