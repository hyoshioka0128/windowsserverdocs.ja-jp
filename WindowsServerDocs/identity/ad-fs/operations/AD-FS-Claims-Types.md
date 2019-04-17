---
ms.assetid: 
title: "クライアント アクセス要求の AD FS での種類"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1e37aded450555d293806d1ed8903a51e3df9424
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
#<a name="client-access-policy-claim-types-in-ad-fs"></a>クライアントのアクセス ポリシー要求の AD FS での種類

その他の要求のコンテキスト情報を提供するには、クライアント アクセス ポリシーは、次の要求の種類は、AD FS を生成処理のための要求のヘッダー情報からを使用します。  詳細については、次を参照してください。[要求エンジンの役割](../technical-reference/the-role-of-the-claims-engine.md)します。

##<a name="x-ms-forwarded-client-ip"></a>X-MS-転送-クライアントの ip アドレス

要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

この AD FS のクレームでは、要求を行っているユーザー (たとえば、Outlook クライアント) の IP アドレスを突き止めるで「ベスト試行」を表します。 この要求の要求を転送するすべてのプロキシ アドレスなど、複数の IP アドレスを含めることができます。  この要求は、現在の HTTP ヘッダーから入力される認証要求を AD FS を渡す際に、ヘッダーをあらかじめ設定 Exchange Online、によってのみ設定します。 要求の値には、次のいずれかを指定できます。


- 単一の IP アドレス - Exchange Online に直接接続されているクライアントの IP アドレス

    >![注]企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイスの IP アドレスとして表示されます。

- 1 つまたは複数の IP アドレス
    - Exchange Online を判断できない場合、接続するクライアントの IP アドレス、HTTP ベースに含めることが標準でないヘッダーを要求し、多くのクライアント、ロード バランサー、および市場でのプロキシでは、x-転送-のヘッダーの値に基づいた値に設定されます。
    - クライアントの IP アドレスとの要求が渡される各プロキシ アドレスを示す複数の IP アドレスは、コンマで区切るされます。

    >![注]Exchange Online のインフラストラクチャに関連する IP アドレスは、リスト内に存在できません。


>![警告]Exchange Online 現在サポートされている IPV4 アドレスだけです。IPV6 アドレスはサポートされません。 


## <a name="x-ms-client-application"></a>X MS クライアント アプリケーション

要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

この AD FS のクレームでは、使用されているアプリケーションを柔軟に対応する終了クライアントによって使用されるプロトコルを表します。  この要求は、現在の HTTP ヘッダーから入力される認証要求を AD FS を渡す際に、ヘッダーをあらかじめ設定 Exchange Online、によってのみ設定します。 アプリケーションに応じて、この要求の値は、次のいずれかになります。



- を Exchange Active Sync を使用するデバイスの場合は、値は、Microsoft.Exchange.ActiveSync です。 
- 次の値のいずれかで Microsoft Outlook クライアントの使用があります。
    - Microsoft.Exchange.Autodiscover
    - Microsoft.Exchange.OfflineAddressBook
    - Microsoft.Exchange.RPC
    - Microsoft.Exchange.WebServices
    - Microsoft.Exchange.Mapi
- このヘッダーで使用できるその他の値は次のとおりです。
    - Microsoft.Exchange.Powershell
    - Microsoft.Exchange.SMTP
    - Microsoft.Exchange.PopImap
    - Microsoft.Exchange.Pop
    - Microsoft.Exchange.Imap

## <a name="x-ms-client-user-agent"></a>X-MS-クライアントのユーザー エージェント

要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

この AD FS のクレームでは、サービスにアクセスするクライアントが使用しているデバイスの種類を表す文字列を提供します。 これは、特定のデバイス (スマート フォンの特定の種類) などのアクセスを防ぐを作成するときに使用できます。  この要求は、現在の HTTP ヘッダーから入力される認証要求を AD FS を渡す際に、ヘッダーをあらかじめ設定 Exchange Online、によってのみ設定します。 この要求の値の例が含まれます (ただし、これらに限定されません) 以下の値。
>![注]X-ms-クライアント-アプリケーションが"Microsoft.Exchange.ActiveSync"は、クライアントを含む可能性のある x ms ユーザー エージェント値の例を示します

- Vortex/1.0
- Apple-iPad1C1/812.1
- Apple-iPhone3C1/811.2
- Apple-iPhone/704.11
- Moto-DROID2/4.5.1
- SAMSUNGSPHD700/100.202
- Android/0.3

>![注]この値が空であることもできます。


## <a name="x-ms-proxy"></a>X-MS-プロキシ

要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

この AD FS のクレームでは、フェデレーション サーバー プロキシ、要求に渡されたことを示します。  この要求はバックエンド フェデレーション サービスを認証要求を渡す際に、ヘッダーを設定、フェデレーション サーバー プロキシによって設定されます。 AD FS に変換を要求します。 

要求の値は、要求が渡されるフェデレーション サーバー プロキシの DNS 名です。

## <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-エンドポイントの絶対パスのパス (アクティブまたはパッシブ)

要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

(Web ブラウザー ベース) クライアントを「パッシブ」と"active"(リッチ) クライアントから送信された要求を判別するため、この要求の種類を使用できます。 これにより、Outlook Web Access、SharePoint Online、または Office 365 ポータル Microsoft Outlook などのリッチ クライアントから送信された要求がブロックされている間に許可するなどのブラウザー ベースのアプリケーションからの要求を外部できます。

要求の値は、要求を受信した AD FS サービスの名前です。
