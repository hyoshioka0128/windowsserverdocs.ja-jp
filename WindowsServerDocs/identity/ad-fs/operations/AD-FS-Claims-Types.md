---
ms.assetid: ''
title: クライアント アクセス要求の AD FS での種類
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1e37aded450555d293806d1ed8903a51e3df9424
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839143"
---
#<a name="client-access-policy-claim-types-in-ad-fs"></a>クライアント アクセス ポリシーの要求の AD FS での種類

追加の要求コンテキスト情報を提供するには、クライアント アクセス ポリシーは、次の要求の種類は、AD FS を処理するための要求ヘッダー情報から生成を使用します。  詳細については、次を参照してください。[要求エンジンの役割](../technical-reference/the-role-of-the-claims-engine.md)します。

##<a name="x-ms-forwarded-client-ip"></a>X-MS-転送-クライアントの IP

要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

この AD FS の要求は、要求を行うユーザー (たとえば、Outlook クライアント) の IP アドレスを確認するのに「最適な試行」を表します。 この要求は、各要求を転送するプロキシのアドレスなど、複数の IP アドレスを含めることができます。  この要求のデータは、現在の HTTP ヘッダーを AD FS を認証要求を渡すときに、ヘッダーを設定する Exchange Online、によってのみ設定します。 要求の値には、次のいずれかを指定できます。


- 単一の IP アドレス - Exchange Online に直接接続されているクライアントの IP アドレス

    >![注]企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイスの IP アドレスとして表示されます。

- 1 つまたは複数の IP アドレス
    - HTTP ベースで含めることができる非標準ヘッダーを要求し、ロード バランサー、多数のクライアントでサポートされて、x-転送-のヘッダーの値に基づいて値を設定が Exchange Online を判断できない場合、接続するクライアントの IP アドレス、および市場でのプロキシ。
    - クライアントの IP アドレスと各要求が渡されるプロキシのアドレスを示す複数の IP アドレスはコンマで区切られます。

    >![注]Exchange Online のインフラストラクチャに関連する IP アドレスをリストには表示されません。


>![Warning] Exchange Online currently supports only IPV4 addresses; it does not support IPV6 addresses. 


## <a name="x-ms-client-application"></a>X MS クライアント アプリケーション

要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

この AD FS の要求は、使用されているアプリケーションに柔軟に対応する、エンド クライアントによって使用されるプロトコルを表します。  この要求のデータは、現在の HTTP ヘッダーを AD FS を認証要求を渡すときに、ヘッダーを設定する Exchange Online、によってのみ設定します。 アプリケーションによっては、この要求の値は、次のいずれかが指定されます。



- を Exchange Active Sync を使用するデバイスの場合は、値は、Microsoft.Exchange.ActiveSync です。 
- 次の値のいずれかで Microsoft Outlook クライアントの使用があります。
    - Microsoft.Exchange.Autodiscover
    - Microsoft.Exchange.OfflineAddressBook
    - Microsoft.Exchange.RPC
    - Microsoft.Exchange.WebServices
    - Microsoft.Exchange.Mapi
- このヘッダーに指定できるその他の値を以下に示します。
    - Microsoft.Exchange.Powershell
    - Microsoft.Exchange.SMTP
    - Microsoft.Exchange.PopImap
    - Microsoft.Exchange.Pop
    - Microsoft.Exchange.Imap

## <a name="x-ms-client-user-agent"></a>X-MS-クライアントのユーザー エージェント

要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

この AD FS の要求は、クライアントがサービスへのアクセスを使用してデバイスの種類を表す文字列を提供します。 これは、顧客 (特定の種類のスマート フォン) などの特定のデバイスのアクセスを禁止する場合に使用できます。  この要求のデータは、現在の HTTP ヘッダーを AD FS を認証要求を渡すときに、ヘッダーを設定する Exchange Online、によってのみ設定します。 この要求の例の値が含まれます (ただしこれらに限定されません) 以下の値。
>![注]X-ms-クライアント アプリケーションは"Microsoft.Exchange.ActiveSync"クライアントの x ms ユーザー エージェント値を含めることがあります内容の例を次に示します

- 渦流形/1.0
- Apple-iPad1C1/812.1
- Apple-iPhone3C1/811.2
- Apple-iPhone/704.11
- Moto-DROID2/4.5.1
- SAMSUNGSPHD700/100.202
- Android/0.3

>![注]この値が空であることもできます。


## <a name="x-ms-proxy"></a>X-MS-プロキシ

要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

この AD FS の要求では、フェデレーション サーバー プロキシで要求が成功したことを示します。  この要求は、バック エンドのフェデレーション サービスを認証要求を渡すときに、ヘッダーを設定します、フェデレーション サーバー プロキシによって作成されます。 AD FS では、クレームに、し、変換します。 

要求の値は、要求が渡されるフェデレーション サーバー プロキシの DNS 名です。

## <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-エンドポイントの絶対パス-パス (アクティブまたはパッシブ)

要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

「パッシブ」(web ブラウザー ベース) のクライアントとの「アクティブ」(リッチ) クライアントから送信された要求を決定するため、この要求の種類を使用できます。 これにより、外部からの Outlook Web Access、SharePoint Online、または Office 365 ポータル Microsoft Outlook などのリッチ クライアントからの要求がブロックされている間に許可するなどのブラウザー ベースのアプリケーションから要求できます。

要求の値は、要求を受信した AD FS サービスの名前です。
