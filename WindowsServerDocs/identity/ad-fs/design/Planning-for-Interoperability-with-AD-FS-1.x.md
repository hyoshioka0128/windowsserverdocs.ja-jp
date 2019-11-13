---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: AD FS 1.x との相互運用性の計画
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e9f72bd83c90a804749329521a72e3232589c735
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407966"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>AD FS 1.x との相互運用性の計画

Active Directory フェデレーションサービス (AD FS) \(\) AD FS windows Server®2012を実行しているフェデレーションサーバーは、windows server 2003 R2 AD FS \(と共にインストールされた\) 1.0 フェデレーションサービスと、Windows Server 2008 または Windows Server 2008 R2 AD FS \(と共にインストールされた\) 1.1 フェデレーションサービスの両方と相互運用できます。 次の相互運用性の任意の組み合わせがサポートされています。  

-   任意の AD FS 1。*x*フェデレーションサービスは、Windows Server 2012 の AD FS フェデレーションサービスで使用できる要求を送信できます。 詳細については、「[チェックリスト: AD FS 1.x からの要求を使用するように AD FS を構成する](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)」を参照してください。  

-   Windows Server 2012 の AD FS フェデレーションサービスは AD FS 1 を送信できます。AD FS 1 で使用できる*x*\-互換性のある要求。*x*フェデレーションサービス。 詳細については、「 [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)」を参照してください。  

-   Windows Server 2012 の AD FS フェデレーションサービスは AD FS 1 を送信できます。AD FS 1 を実行している1つ以上の Web サーバーで使用できる*x*\-互換性のある要求。*x*要求\-対応する Web エージェント。 詳細については、「 [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Claims-Aware Web Agent](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)」を参照してください。  

> [!NOTE]  
> AD FS では、AD FS 1 をサポートしたり、相互運用したりすることはできません。*x* Windows NT トークンベースの Web エージェント。  

AD FS 1 です。*x*\-互換性のある要求は、Windows Server 2012 の AD FS フェデレーションサービスによって送信され、AD FS 1 で認識できる要求です。*x*フェデレーションサービス。 AD FS 1 になります。*x*フェデレーションサービスは、AD FS フェデレーションサービスが送信する要求、名前識別子 \(ID\) 要求の種類を送信する必要があります。  

## <a name="understanding-the-name-id-claim-type"></a>名前 ID 要求の種類の認識  
名前 ID 要求の種類は、AD FS 1.*x* が使用する識別子要求の種類に相当します。 これは、AD FS 1.*x*と相互運用する場合には必ず使用する必要があります。 名前 ID 要求の種類では、AD FS 1 を有効にします。*x*フェデレーションサービスまたは AD FS 1。*x*要求は、次の表のいずれかの名前 ID 形式で送信された場合に限り、Windows Server 2012 で AD FS が送信する要求を使用するために、\-認識されます。  


|      名前 ID の形式       |               対応する URI                |
|---------------------------|------------------------------------------------|
| AD FS 1.*x* 電子メール アドレス | http://schemas.xmlsoap.org/claims/EmailAddress |
|   AD FS 1.*x* 電子メール UPN   |     http://schemas.xmlsoap.org/claims/UPN      |
|        共通名        |  http://schemas.xmlsoap.org/claims/CommonName  |
|           グループ           |    http://schemas.xmlsoap.org/claims/Group     |

送信される必要があるのは、適切な形式の名前 ID 要求 1 つのみです。 この条件を満たさないと、表に記載された制限に準拠していると見なされ、他の多くの要求も送信される場合があります。  

> [!NOTE]  
> AD FS 1 です。*x*フェデレーションサービスは、 http://schemas.xmlsoap.org/claims/の UNIFORM RESOURCE IDENTIFIER \(URI\) で始まる入力方向の要求の種類のみを解釈できます。  

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
