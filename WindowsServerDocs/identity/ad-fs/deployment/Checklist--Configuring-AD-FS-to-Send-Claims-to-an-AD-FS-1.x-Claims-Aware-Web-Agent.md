---
ms.assetid: 551c1a0d-8d30-41b4-9c4a-35a3337dd3bc
title: "フェデレーション サーバーを展開します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 32675aa7fb8c7b928bcf80a4d1072fe5eab7cd61
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>チェックリスト: AD FS 1.x Claims-aware Web エージェントに要求を送信する AD FS を構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
  
## <a name="checklist-configuring-ad-fs-to-send-claims-to-an-ad-fs-1x-claims-aware-web-agent"></a>チェックリスト: AD FS 1.x claims\ 認識 Web エージェントに要求を送信する AD FS を構成します。  
このチェックリストには、AD FS 1 を実行している Web サーバーによってホストされているアプリケーションが理解できる要求を送信する Windows Server 2012 では、Active Directory フェデレーション サービス \(AD FS\) フェデレーション サービスを構成するために必要なタスクが含まれます。*x* claims\ に対応する Web エージェント。  
  
> [!NOTE]  
> 順序でこのチェックリストのタスクを完了します。 参照リンクでは、手順には、このトピックに戻りできるように、このチェックリストの残りのタスクを続行することができます、その手順の手順を完了します。  
  
![要求を送信する AD FS 構成](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: AD FS 1.x claims\ 認識 Web エージェントに要求を送信する AD FS を構成します。**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|Windows Server 2012 で AD FS と AD FS の以前のバージョン間の相互運用性の計画し、詳細については、名前 ID 要求の種類について説明します。|![要求を送信する AD FS 構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS と相互運用性の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|されていない場合は、まず Windows Server 2012 で AD FS フェデレーション サービスと AD FS 1 の間で証明書利用者信頼を作成する、右側に、リンクを使用します。*x*フェデレーション サービス。|[チェックリスト: AD FS 1.x のフェデレーション サービスに要求を送信する AD FS を構成します。](Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|前に AD FS 1 によってホストされているアプリケーションとの相互運用を実現できます。*x* claims\ 対応する Web エージェントを作成する必要が最初に AD FS フェデレーション サービスで証明書利用者信頼を AD FS 1、Windows Server 2012 でします。 *x* claims\ に対応する Web エージェント。 **注:**新しいを追加するのと同じ AD FS フェデレーション サービスにこの信頼を作成することは**アプリケーション**AD fs 1.x Federation Service \ (**フェデレーション Service\\Trust Policy\\My Organization\\Application**\)。 AD FS と同等のものがあるないために、この証明書利用者信頼が必要な**アプリケーション**独自スナップイン内のノード。 ただし、引き続き必要アプリケーションにセキュリティで保護されたチャネルです。<br /><br />右側にあるリンクの手順を使用する信頼をセットアップするときに、信頼の追加証明書利用者のパーティ ウィザード、AD FS 1 と相互運用するこの信頼を設定するでは、次を行う必要があります。*x* claims\ に対応する Web エージェント。<br /><br />1。 で、**データ ソースの選択**ページで、選択**データを入力して、証明書利用者の信頼を手動でパーティ**します。<br />2.、**プロファイルの選択**] ページで、[ **AD FS 1.0 および 1.1 プロファイル**します。<br />3.、 **URL の構成**ページで、 **WS\ フェデレーション パッシブ URL**、種類、**アプリケーション URL** AD FS 1 で定義されています。*x*パートナーのフェデレーション サービス。<br />4.、**識別子の構成**ページで、**部分信頼の証明書利用者識別子**、種類、**アプリケーション URL** AD FS 1 で定義されています。*x* claims\ に対応する Web エージェント|![要求を送信する AD FS 構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[、証明書利用者信頼を手動で作成します。](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|AD FS 1 を実行している Web サーバーの管理者に問い合わせてください。*x* claims\ 認識 Web エージェントと claims\ 対応のアプリケーションに関連付けられている Web.config ファイルを編集する管理者に依頼 \ (下にある既定の Web サイトでインターネット インフォメーション サービス \(IIS\)\) AD FS フェデレーション サービスで Web エージェントをポイントします。<br /><br />たとえば、置換*myresourcefederationserver*タグ`<fs>https://myresourcefederationserver/adfs/fs/federationserverservice.asmx</fs>`有効な AD FS フェデレーション サーバー名を持つ Web.config ファイルのします。<br /><br />これは、アプリケーションと AD FS 1.x claims\ に対応する Web エージェントから Windows Server 2012 で AD FS フェデレーション サービスに送信される要求を使用できるようにするために必要なです。|N\/A|  
|![要求を送信する AD FS を構成します。](media/icon_checkboxo.gif)|要求規則を属性ストアから抽出された入力方向の要求を実行し、パススルー、フィルター処理、または変換名前 ID には要求の種類を理解され、AD によって消費されることができますを作成する必要が以前に作成した証明書利用者のパーティ信頼に FS 1 です。*x* claims\ に対応する Web エージェント。 **注:**この規則を作成する前に、この規則を作成する要求規則セットに最初の属性ストアから、Lightweight Directory Access Protocol \(LDAP\) 属性信頼性情報を抽出する前に付属するルールがあることを確認ください。 この要求は、AD FS 1 を送信するために作成した規則の入力として使用されます。*x*\-compatible 要求します。 LDAP 属性を抽出する規則を作成する方法の詳細については、次を参照してください。 [LDAP 属性を要求として送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)します。|![要求を送信する AD FS 構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[、AD FS を送信する規則を作成する 1.x 互換の要求](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)|  
  

