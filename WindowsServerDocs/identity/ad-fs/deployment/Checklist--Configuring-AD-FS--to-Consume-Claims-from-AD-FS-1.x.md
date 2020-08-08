---
ms.assetid: e7f9e518-2d5d-4a0d-9147-34e1304f42ac
title: チェックリスト-AD FS 1.x からの要求を使用するように従来の AD FS を構成する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 0d27f72aee5289b0ce8dc63aa31c2490d0bf2a62
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969779"
---
# <a name="checklist-configuring-ad-fs--to-consume-claims-from-ad-fs-1x"></a>チェックリスト: AD FS 1.x からの要求を使用するように AD FS を構成する


## <a name="checklist-configuring-ad-fs-to-consume-claims-from-adfs1x"></a>チェックリスト: AD FS 1.x からの要求を使用するように AD FS を構成する
このチェックリストには、 \( \) AD FS 1 によって送信された要求を使用するために、Windows Server 2012 で Active Directory フェデレーションサービス (AD FS) AD FS フェデレーションサービスを構成するために必要なタスクが含まれています。*x*フェデレーションサービス。

> [!NOTE]
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。

![AD FS チェックリストからの要求の使用](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**: AD FS 1.x からの要求を使用するように AD FS を構成します。**

|タスク|リファレンス|
|--------|-------------|
|Windows Server 2012 と以前のバージョンの AD FS の AD FS 間の相互運用性を計画し、Name ID 要求の種類の詳細について説明します。|![AD FS 1.x との](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[相互運用性のために AD FS 計画](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678040(v=ws.11))の要求を使用する|
| 以前のバージョンの AD FS と相互運用するには、まず AD FS フェデレーションサービスで要求プロバイダー信頼を作成する必要があります。 **注:** AD FS 1 を持つ信頼を作成することはできません。*x*フェデレーションサービスフェデレーションメタデータを使用します。<p>右側のリンクにある手順を使用して信頼を設定する場合は、要求プロバイダー信頼の追加ウィザードで次の操作を行って、AD FS 1 と相互運用するようにこの信頼を設定する必要があります。*x*フェデレーションサービス:<p>1. [**データソースの選択**] ページで、[**証明書利用者の信頼に関するデータを手動で入力**する] を選択します。<br />2. [**プロファイルの選択**] ページで、[ **AD FS 1.0 および1.1 プロファイル**] を選択します。<br />3. [ **URL の構成**] ページの [ **ws-federation \- パッシブ URL**] に、AD FS 1 **Federation Service endpoint URL** *で定義されているフェデレーションサービスエンドポイント URL を入力します。* パートナーの x フェデレーションサービス。<br />4. [**識別子の構成**] ページの [**要求プロバイダー信頼の識別子**] に、AD FS 1 で定義されている**フェデレーションサービス URI**を入力します。パートナーの*x*フェデレーションサービス。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求プロバイダー信頼を手動で作成](../../ad-fs/operations/Create-a-Claims-Provider-Trust.md)AD FS の要求を使用する|
| 先ほど作成した要求プロバイダー信頼では、AD FS 1.x フェデレーションサービスから受信した要求を取得し、それらをパススルー、フィルター処理、または名前 ID 要求の種類に変換する要求規則を作成する必要があります。<p>名前 ID 要求の種類が渡され、フィルター処理または変換された場合、Windows Server 2012 の AD FS フェデレーションサービスによって認識および使用できるように、別の規則または規則の入力として使用できます。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1. x 互換の要求を送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)AD FS からの要求を使用する|
| AD FS 1 の管理者に連絡してください。*x*フェデレーションサービス、AD FS 1 の管理者がいます。*x*フェデレーションサービス新しいリソースパートナーの信頼を設定します。 また、 \( フェデレーションサービスのプロパティ \) 、フェデレーションサービスエンドポイント URL、およびエクスポートされたトークン \- 署名証明書ファイル ( \( 公開キーのみ) で、管理者にフェデレーションサービス URI を指定し \) ます。 信頼を設定するには、管理者がこれらの項目を必要とします。|N\/A|
