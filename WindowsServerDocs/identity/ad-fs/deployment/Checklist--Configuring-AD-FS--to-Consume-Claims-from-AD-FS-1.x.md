---
ms.assetid: e7f9e518-2d5d-4a0d-9147-34e1304f42ac
title: チェックリスト-AD FS 1.x からの要求を使用するように AD FS を構成する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 0b3b58b158e6443cf4f0e2b9e09960f46d57ebbc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854165"
---
# <a name="checklist-configuring-ad-fs--to-consume-claims-from-ad-fs-1x"></a>チェックリスト: AD FS 1.x からの要求を使用するように AD FS を構成する

  
## <a name="checklist-configuring-ad-fs-to-consume-claims-from-adfs1x"></a>チェックリスト: AD FS 1.x からの要求を使用するように AD FS を構成する  
このチェックリストには、Active Directory フェデレーションサービス (AD FS)\) AD FS \(を構成するために必要なタスクが含まれています。このタスクは、Windows Server 2012 でフェデレーションサービス1によって送信された要求を処理するために使用します。*x*フェデレーションサービス。  
  
> [!NOTE]  
> このチェックリストに記載されているタスクを順番どおりに実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
AD FS チェックリストからの要求の使用 ![](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**: AD FS 1.x からの要求を使用するように AD FS を構成**する  
  
||タスク|参照|  
|-|--------|-------------|  
|![AD FS からの要求を使用する](media/icon_checkboxo.gif)|Windows Server 2012 と以前のバージョンの AD FS の AD FS 間の相互運用性を計画し、Name ID 要求の種類の詳細について説明します。|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1.x との相互運用性のために AD FS 計画](https://technet.microsoft.com/library/ff678040.aspx)の要求を使用 ![|  
|![AD FS からの要求を使用する](media/icon_checkboxo.gif)|以前のバージョンの AD FS と相互運用するには、まず AD FS フェデレーションサービスで要求プロバイダー信頼を作成する必要があります。 **注:** AD FS 1 を持つ信頼を作成することはできません。*x*フェデレーションサービスフェデレーションメタデータを使用します。<p>右側のリンクにある手順を使用して信頼を設定する場合は、要求プロバイダー信頼の追加ウィザードで次の操作を行って、AD FS 1 と相互運用するようにこの信頼を設定する必要があります。*x*フェデレーションサービス:<p>1. **[データソースの選択]** ページで、 **[証明書利用者の信頼に関するデータを手動で入力]** する を選択します。<br />2. **[プロファイルの選択]** ページで、 **[AD FS 1.0 および1.1 プロファイル]** を選択します。<br />3. **[URL の構成]** ページで、[ **WS\-フェデレーションパッシブ URL**] に、AD FS 1 で定義されている**フェデレーションサービスエンドポイント url**を入力します。パートナーの*x*フェデレーションサービス。<br />4. **[識別子の構成]** ページの **[要求プロバイダー信頼の識別子]** に、AD FS 1 で定義されている**フェデレーションサービス URI**を入力します。パートナーの*x*フェデレーションサービス。|要求](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[プロバイダー信頼を手動で作成 AD FS ために](../../ad-fs/operations/Create-a-Claims-Provider-Trust.md)要求 ![使用する|  
|![AD FS からの要求を使用する](media/icon_checkboxo.gif)|先ほど作成した要求プロバイダー信頼では、AD FS 1.x フェデレーションサービスから受信した要求を取得し、それらをパススルー、フィルター処理、または名前 ID 要求の種類に変換する要求規則を作成する必要があります。<p>名前 ID 要求の種類が渡され、フィルター処理または変換された場合、Windows Server 2012 の AD FS フェデレーションサービスによって認識および使用できるように、別の規則または規則の入力として使用できます。|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1. x 互換の要求を送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)AD FS ![|  
|![AD FS からの要求を使用する](media/icon_checkboxo.gif)|AD FS 1 の管理者に連絡してください。*x*フェデレーションサービス、AD FS 1 の管理者がいます。*x*フェデレーションサービス新しいリソースパートナーの信頼を設定します。 また、管理者にフェデレーションサービス URI \(をフェデレーションサービスプロパティ\)、フェデレーションサービスエンドポイント URL、およびエクスポートされたトークン\-署名証明書ファイル \(公開キーのみ\)を指定します。 信頼を設定するには、管理者がこれらの項目を必要とします。|N\/A|  
  

