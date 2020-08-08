---
ms.assetid: 04b63d9f-e924-4146-9b1d-785ed8b4239c
title: AD FS 1.x との相互運用性の計画
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 94313fc185a4f326ad00a95e4c594fd3e696f61a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967609"
---
# <a name="planning-for-interoperability-with-ad-fs-1x"></a>AD FS 1.x との相互運用性の計画

Active Directory フェデレーションサービス (AD FS) \( AD FS Windows \) server 2012 を実行しているフェデレーションサーバーは、windows Server &reg; \( 2003 R2 フェデレーションサービスと共にインストールされた AD FS 1.0 \) と、 \( Windows server 2008 または windows server 2008 R2 AD FS と共にインストールされたフェデレーションサービス1.1 の両方と相互運用できます \) 。 次の相互運用性の任意の組み合わせがサポートされています。

-   任意の AD FS 1。*x*フェデレーションサービスは、Windows Server 2012 の AD FS フェデレーションサービスで使用できる要求を送信できます。 詳細については、「[チェックリスト: AD FS 1.x からの要求を使用するように AD FS を構成する](../../ad-fs/deployment/Checklist--Configuring-AD-FS--to-Consume-Claims-from-AD-FS-1.x.md)」を参照してください。

-   Windows Server 2012 の AD FS フェデレーションサービスは AD FS 1 を送信できます。*x* \-AD FS 1 で使用できる互換性のある要求。*x*フェデレーションサービス。 詳細については、「 [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Federation Service](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Federation-Service.md)」を参照してください。

-   Windows Server 2012 の AD FS フェデレーションサービスは AD FS 1 を送信できます。*x* \-AD FS 1 を実行する1つ以上の Web サーバーで使用できる互換性のある要求。*x*要求に \- 対応する Web エージェント。 詳細については、「 [Checklist: Configuring AD FS to Send Claims to an AD FS 1.x Claims-Aware Web Agent](../../ad-fs/deployment/Checklist--Configuring-AD-FS-to-Send-Claims-to-an-AD-FS-1.x-Claims-Aware-Web-Agent.md)」を参照してください。

> [!NOTE]
> AD FS では、AD FS 1 をサポートしたり、相互運用したりすることはできません。*x* Windows NT トークンベースの Web エージェント。

AD FS 1 です。*x* \-互換性のある要求は、Windows Server 2012 の AD FS フェデレーションサービスによって送信でき、AD FS 1 で認識される要求です。*x*フェデレーションサービス。 AD FS 1 になります。*x*フェデレーションサービスは、AD FS フェデレーションサービスが送信する要求を使用でき \( ます。名前識別子 ID の要求の種類を送信する \) 必要があります。

## <a name="understanding-the-name-id-claim-type"></a>名前 ID 要求の種類の認識
名前 ID 要求の種類は、AD FS 1.*x* が使用する識別子要求の種類に相当します。 これは、AD FS 1.*x* と相互運用する場合には必ず使用する必要があります。 名前 ID 要求の種類では、AD FS 1 を有効にします。*x*フェデレーションサービスまたは AD FS 1。*x*次の \- 表のいずれかの名前 ID 形式でこれらの要求が送信される限り、Windows Server 2012 で AD FS れる要求を使用するために、x 要求に対応する Web エージェントは送信します。


|      名前 ID の形式       |               対応する URI                |
|---------------------------|------------------------------------------------|
| AD FS 1.*x* 電子メール アドレス | http://schemas.xmlsoap.org/claims/EmailAddress |
|   AD FS 1.*x* 電子メール UPN   |     http://schemas.xmlsoap.org/claims/UPN      |
|        共通名        |  http://schemas.xmlsoap.org/claims/CommonName  |
|           グループ           |    http://schemas.xmlsoap.org/claims/Group     |

送信される必要があるのは、適切な形式の名前 ID 要求 1 つのみです。 この条件を満たさないと、表に記載された制限に準拠していると見なされ、他の多くの要求も送信される場合があります。

> [!NOTE]
> AD FS 1 です。*x*フェデレーションサービスは、の Uniform Resource Identifier URI で始まる入力方向の要求の種類のみを解釈でき \( \) http://schemas.xmlsoap.org/claims/ ます。

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
