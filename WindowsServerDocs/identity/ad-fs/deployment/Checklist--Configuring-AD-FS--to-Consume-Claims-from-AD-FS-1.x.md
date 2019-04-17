---
ms.assetid: e7f9e518-2d5d-4a0d-9147-34e1304f42ac
title: "チェックリスト - Configuring AD FS からのクレームを使用する AD FS 1.x"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: fe99487d3a770547af36f69722b442d0e2cbb8b1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-configuring-ad-fs--to-consume-claims-from-ad-fs-1x"></a>チェックリスト: 構成を AD FS からのクレームを利用するための AD FS 1.x

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-consume-claims-from-ad-fs-1x"></a>チェックリスト: 構成を AD FS からのクレームを利用するための AD FS 1.x  
このチェックリストには、AD FS 1 から送信される、信頼性情報を使用する Windows Server 2012 で、Active Directory フェデレーション サービス \(AD FS\) フェデレーション サービスを構成するために必要なタスクが含まれます。*x*フェデレーション サービス。  
  
> [!NOTE]  
> 順序でこのチェックリストのタスクを完了します。 参照リンクでは、手順には、このトピックに戻りできるように、このチェックリストの残りのタスクを続行することができます、その手順の手順を完了します。  
  
![AD FS からのクレームを消費する](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: Configuring AD FS からのクレームを使用する AD FS 1.x**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![AD FS からのクレームを消費します。](media/icon_checkboxo.gif)|Windows Server 2012 で AD FS と AD FS の以前のバージョン間の相互運用性の計画し、詳細については、名前 ID 要求の種類について説明します。|![AD FS からのクレームを消費する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS と相互運用性の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![AD FS からのクレームを消費します。](media/icon_checkboxo.gif)|AD FS の以前のバージョンと相互運用することができます、前にまず、AD FS フェデレーション サービス内の要求プロバイダー信頼を作成する必要があります。 **注:** AD FS 1 で信頼を作成することはできません。*x*フェデレーション メタデータを使用してフェデレーション サービス。<br /><br />右へのリンクの手順を使用する信頼をセットアップするときに、追加要求プロバイダー信頼ウィザード、AD FS 1 と相互運用するこの信頼を設定するでは、次を行う必要があります。*x*フェデレーション サービス。<br /><br />1。 で、**データ ソースの選択**ページで、選択**データを入力して、証明書利用者の信頼を手動でパーティ**します。<br />2.、**プロファイルの選択**] ページで、[ **AD FS 1.0 および 1.1 プロファイル**します。<br />3.、 **URL の構成**ページで、 **WS\ フェデレーション パッシブ URL**、種類、**フェデレーション サービス エンドポイント URL** AD FS 1 で定義されています。*x*パートナーのフェデレーション サービス。<br />4.、**識別子の構成**ページで、**要求プロバイダー信頼の識別子**、種類、**フェデレーション サービスの URI** AD FS 1 で定義されています。*x*パートナーのフェデレーション サービス。|![AD FS からのクレームを消費する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[、要求プロバイダー信頼を手動で作成します。](../../ad-fs/operations/Create-a-Claims-Provider-Trust.md)|  
|![AD FS からのクレームを消費します。](media/icon_checkboxo.gif)|以前に作成する要求プロバイダー信頼を作成する必要がある要求規則を AD FS からの入力方向の要求になります 1.x Federation Service とを使用して、パスのフィルター処理、または名前 ID 要求の種類に変換します。<br /><br />名前 ID 要求の種類が、フィルター処理または変換するを使用して、渡されるされたときに理解して Windows Server 2012 で AD FS フェデレーション サービスで使用できるように別の規則または規則の入力として使用できます。|![AD FS からのクレームを消費する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[、AD FS を送信する規則を作成する 1.x 互換の要求](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
|![AD FS からのクレームを消費します。](media/icon_checkboxo.gif)|AD FS 1 の管理者に問い合わせてください。*x*フェデレーション サービスと AD FS 1 の管理者に依頼します。*x*フェデレーション サービスが新しいリソース パートナーの信頼をセットアップします。 また、フェデレーション サービスの URI にその管理者を提供 \ (内、フェデレーション サービス properties\)、フェデレーション サービスのエンドポイントの URL と、エクスポートした token\ 署名証明書ファイル \ (公開キー only\) とします。 管理者は、これらの項目を信頼関係をセットアップする必要があります。|N\/A|  
  

