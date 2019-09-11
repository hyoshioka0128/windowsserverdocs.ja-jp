---
ms.assetid: ''
title: AD FS のクライアントアクセス要求の種類
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0b309dfe3c4c13629144342198197f382a2f25c2
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866206"
---
# <a name="client-access-policy-claim-types-in-ad-fs"></a>AD FS のクライアントアクセスポリシー要求の種類

クライアントアクセスポリシーは、追加の要求コンテキスト情報を提供するために、次の要求の種類を使用します。要求の種類は、要求ヘッダー情報から生成 AD FS ます。  詳細については、「[要求エンジンの役割](../technical-reference/the-role-of-the-claims-engine.md)」を参照してください。

## <a name="x-ms-forwarded-client-ip"></a>X-ミリ秒-クライアント-IP

要求の種類:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

この AD FS 要求は、要求を行っているユーザー (Outlook クライアントなど) の IP アドレスを突き止めるに "最適な試行" を表します。 この要求には、要求を転送したすべてのプロキシのアドレスを含む、複数の IP アドレスを含めることができます。  この要求は、現在 Exchange Online によって設定されている HTTP ヘッダーから作成されます。これは、認証要求を AD FS に渡すときに、ヘッダーを入力します。 要求の値には、次のいずれかを指定できます。


- 単一の IP アドレス-Exchange Online に直接接続されているクライアントの IP アドレス

    >!付箋企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイス IP アドレスとして表示されます。

- 1つ以上の IP アドレス
  - 接続しているクライアントの IP アドレスを Exchange Online が特定できない場合は、HTTP ベースの要求に含めることができ、多くのクライアント、ロードバランサー、およびでサポートされている非標準ヘッダーの x 転送済みヘッダーの値に基づいて値が設定されます。市場のプロキシ。
  - クライアント IP アドレスを示す複数の IP アドレスと、要求に合格した各プロキシのアドレスは、コンマで区切られます。

    >!付箋Exchange Online インフラストラクチャに関連する IP アドレスは、一覧に表示されません。


>!要する現在、Exchange Online は IPV4 アドレスのみをサポートしています。IPV6 アドレスはサポートされていません。 


## <a name="x-ms-client-application"></a>X-MS-クライアント-アプリケーション

要求の種類:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

この AD FS 要求は、エンドクライアントが使用するプロトコルを表します。このプロトコルは、使用されているアプリケーションに対して弱くなります。  この要求は、現在 Exchange Online によって設定されている HTTP ヘッダーから作成されます。これは、認証要求を AD FS に渡すときに、ヘッダーを入力します。 アプリケーションによっては、この要求の値は次のいずれかになります。



- Exchange Active Sync を使用するデバイスの場合、値は "Microsoft. Exchange. ActiveSync" になります。 
- Microsoft Outlook クライアントを使用すると、次のいずれかの値が返される場合があります。
    - Microsoft. Exchange. 自動検出
    - OfflineAddressBook
    - Microsoft. Exchange. RPC
    - Microsoft. Exchange...
    - Microsoft. Exchange. Mapi
- このヘッダーには、次のような値を指定できます。
    - Microsoft. Exchange. Powershell
    - Microsoft. Exchange. SMTP
    - Microsoft. Exchange. PopImap
    - Microsoft. Exchange. Pop
    - Microsoft. Exchange. Imap

## <a name="x-ms-client-user-agent"></a>X-MS-クライアント-ユーザーエージェント

要求の種類:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

この AD FS 要求は、クライアントがサービスにアクセスするために使用しているデバイスの種類を表す文字列を提供します。 これは、特定のデバイス (特定の種類のスマートフォンなど) へのアクセスをユーザーが禁止する場合に使用できます。  この要求は、現在 Exchange Online によって設定されている HTTP ヘッダーから作成されます。これは、認証要求を AD FS に渡すときに、ヘッダーを入力します。 この要求の値の例には、以下の値が含まれます (ただし、これらに限定されません)。
>!付箋次に示すのは、x-ms クライアントアプリケーションが "Microsoft. Exchange. ActiveSync" であるクライアントに対して、ユーザーエージェントの値に含まれる可能性のある例です。

- 渦/1.0
- IPad1C1/812.1
- IPhone3C1/811.2
- Apple iPhone/704.11
- Moto-DROID2/4.5.1
- SAMSUNGSPHD700/100.202
- Android/0.3

>!付箋この値が空である可能性もあります。


## <a name="x-ms-proxy"></a>X-MS-プロキシ

要求の種類:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

この AD FS 要求は、要求がフェデレーションサーバープロキシを経由して渡されたことを示します。  この要求は、フェデレーションサーバープロキシによって作成されます。これにより、認証要求をバックエンドフェデレーションサービスに渡すときにヘッダーが設定されます。 AD FS は、それをクレームに変換します。 

要求の値は、要求を受けたフェデレーションサーバープロキシの DNS 名です。

## <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-エンドポイント-絶対パス (アクティブとパッシブ)

要求の種類:`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

この要求の種類を使用して、"アクティブ" (リッチ) クライアントと "パッシブ" (web ブラウザーベース) クライアントからの要求を特定できます。 これにより、Outlook Web アクセス、SharePoint Online、Office 365 ポータルなどのブラウザーベースのアプリケーションからの外部要求が許可されますが、Microsoft Outlook などのリッチクライアントからの要求はブロックされます。

要求の値は、要求を受信した AD FS サービスの名前です。
