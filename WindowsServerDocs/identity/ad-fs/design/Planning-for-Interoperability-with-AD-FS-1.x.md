---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: "AD FS と相互運用性の計画 1.x"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f287261ce6cb56e40385ef4de922045153819a23
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>AD FS と相互運用性の計画 1.x

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server® 2012 を実行している active Directory フェデレーション サービス \(AD FS\) フェデレーション サーバーが両方、AD FS 1.0 と相互運用できます \ (Windows Server 2003 R2\ でインストールされた) フェデレーション サービスと AD FS 1.1 \ (Windows Server 2008 または Windows Server 2008 R2\ にインストールされた) フェデレーション サービス。 次の相互運用性の組み合わせのいずれかがサポートされています。  
  
-   AD FS 1 です。*x*フェデレーション サービスは、Windows Server 2012 で AD FS フェデレーション サービスで消費可能な要求を送信できます。 詳細については、次を参照してください。[チェックリスト: AD FS からの信頼性情報を使用する AD FS を構成する 1.x](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)します。  
  
-   Windows Server 2012 では、AD FS フェデレーション サービスでは、AD FS 1 を送信できます。*x*\-compatible の要求を AD FS 1 で使用できます。*x*フェデレーション サービス。 詳細については、次を参照してください。[チェックリスト: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)します。  
  
-   Windows Server 2012 では、AD FS フェデレーション サービスでは、AD FS 1 を送信できます。*x*\-compatible の要求を AD FS 1 を実行する 1 つまたは複数の Web サーバーで使用できます。*x* claims\ に対応する Web エージェント。 詳細については、次を参照してください。[チェックリスト: Configuring AD FS to Send Claims to an AD FS 1.x Claims-aware Web エージェント](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)します。  
  
> [!NOTE]  
> AD FS のサポートまたは AD FS 1 との相互作用はできません。*x* Windows NT トークン ベースの Web エージェント。  
  
AD FS 1 です。*x*\-compatible 要求は要求を Windows Server 2012 で AD FS フェデレーション サービスによって送信され、AD FS 1 が認識できることができます。*x*フェデレーション サービス。 できるように、AD FS 1 です。*x*フェデレーション サービスは、AD FS フェデレーション サービスに送信する要求をで使用できる、名前識別子 \(ID\) 要求の種類が送信する必要があります。  
  
## <a name="understanding-the-name-id-claim-type"></a>名前 ID 要求の種類を理解します。  
名前 ID 要求の種類は、AD FS 1 を入力する ID 要求のそれと同等です。*x* uses. これは、AD FS 1 と相互運用するときに使用する必要があります。*x*. 名前 ID 要求入力を有効にするか、AD FS 1 します。*x*フェデレーション サービスまたは AD FS 1 です。*x* claims\ に対応する Web エージェントを次の表の名前 ID 形式のいずれかでこれらの要求が送信される限り、Windows Server 2012 で AD FS を送信する要求を利用するためです。  
  
|名前 ID の形式|対応する URI|  
|------------------|---------------------|  
|AD FS 1 です。*x*電子メール アドレス|http://schemas.xmlsoap.org/claims/EmailAddress|  
|AD FS 1 です。*x*電子メール UPN|http://schemas.xmlsoap.org/claims/UPN|  
|共通名|http://schemas.xmlsoap.org/claims/CommonName|  
|グループ|http://schemas.xmlsoap.org/claims/Group|  
  
適切な形式の 1 つだけの名前 ID 要求を送信する必要があります。 この条件が満たされると、その他の多くの信頼性情報を送信できます同様に、表に記載された制限に準拠するいると仮定した場合。  
  
> [!NOTE]  
> AD FS 1 です。*x*フェデレーション サービス http://schemas.xmlsoap.org/claims/ の Uniform Resource Identifier \(URI\) で始まるのみ入力方向の要求の種類を解釈することができます。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
