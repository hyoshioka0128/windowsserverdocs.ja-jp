---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: AD FS 1.x との相互運用性の計画
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9c5f49bd0ee0da9c3b92bad96f16ca310f82c239
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445333"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>AD FS 1.x との相互運用性の計画

Active Directory フェデレーション サービス\(AD FS\) Windows Server® 2012 を実行しているフェデレーション サーバーは両方、AD FS 1.0 と相互運用できます\(Windows Server 2003 R2 にインストールされている\)フェデレーション サービスと、AD FS1.1 \(Windows Server 2008 または Windows Server 2008 R2 と共にインストール\)フェデレーション サービス。 次の相互運用性の任意の組み合わせがサポートされています。  

-   AD FS 1。*x*フェデレーション サービスは、Windows Server 2012 で AD FS フェデレーション サービスが使用できる要求を送信できます。 詳細については、次を参照してください。[チェックリスト。Configuring AD FS からの要求を使用する AD FS 1.x](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)します。  

-   Windows Server 2012 では、AD FS フェデレーション サービスでは、AD FS 1 を送信できます。*x*\-互換の要求を AD FS 1 で使用できます *。x*フェデレーション サービス。 詳細については、次を参照してください。[チェックリスト。AD FS 1.x のフェデレーション サービスに対するクレームを送信する AD FS を構成する](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)します。  

-   Windows Server 2012 では、AD FS フェデレーション サービスでは、AD FS 1 を送信できます。*x*\-互換の要求を AD FS 1 を実行している 1 つまたは複数の Web サーバーで使用できます *。x*クレーム\-対応する Web エージェントです。 詳細については、次を参照してください。[チェックリスト。AD FS 1.x Claims-aware Web エージェントを要求を送信する AD FS を構成する](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)します。  

> [!NOTE]  
> AD FS のサポートまたは AD FS 1 との相互運用はできません。*x* Windows NT トークン ベースの Web エージェントです。  

AD FS 1。*x*\-互換の要求は、Windows Server 2012 で AD FS フェデレーション サービスによって送信され、AD FS 1 で認識されることを要求します *。x*フェデレーション サービス。 ように、AD FS 1。*x*フェデレーション サービスが使用できる名前識別子、要求を送信すると、AD FS フェデレーション サービス、 \(ID\)要求の種類を送信する必要があります。  

## <a name="understanding-the-name-id-claim-type"></a>名前 ID 要求の種類の認識  
名前 ID 要求の種類は、AD FS 1.*x* が使用する識別子要求の種類に相当します。 これは、AD FS 1.*x*と相互運用する場合には必ず使用する必要があります。 名前 ID 要求を入力できますか、AD FS 1。*x*フェデレーション サービスまたは AD FS 1 *。x*クレーム\-これらの要求は、次の表の名前 ID 形式のいずれかで送信される限り、Windows Server 2012 で AD FS が送信する要求に対応する Web エージェントです。  


|      名前 ID の形式       |               対応する URI                |
|---------------------------|------------------------------------------------|
| AD FS 1.*x* 電子メール アドレス | http://schemas.xmlsoap.org/claims/EmailAddress |
|   AD FS 1.*x* 電子メール UPN   |     http://schemas.xmlsoap.org/claims/UPN      |
|        共通名        |  http://schemas.xmlsoap.org/claims/CommonName  |
|           グループ           |    http://schemas.xmlsoap.org/claims/Group     |

送信される必要があるのは、適切な形式の名前 ID 要求 1 つのみです。 この条件を満たさないと、表に記載された制限に準拠していると見なされ、他の多くの要求も送信される場合があります。  

> [!NOTE]  
> AD FS 1。*x*フェデレーション サービスが Uniform Resource Identifier で始まる受信要求の種類を解釈できる\(URI\)の http://schemas.xmlsoap.org/claims/します。  

## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
