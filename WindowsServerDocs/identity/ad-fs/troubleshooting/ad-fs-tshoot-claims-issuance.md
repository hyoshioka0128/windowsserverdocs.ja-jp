---
title: AD FS のトラブルシューティング-要求の発行
description: このドキュメントでは、AD FS によるトークンの発行に関する問題をトラブルシューティングする方法について説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.openlocfilehash: 9eb5ce1ee92e828cc1fd6ceb40ddddec453afe87
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954188"
---
# <a name="ad-fs-troubleshooting---claims-issuance"></a>AD FS のトラブルシューティング-要求の発行
クレームは、1つのサブジェクトがそれ自体または別のサブジェクトに対して行うステートメントです。  要求は証明書利用者によって発行され、1つまたは複数の値が与えられ、AD FS サーバーによって発行されたセキュリティトークンにパッケージ化されます。  このプロセスにはいくつかの可動要素があるため、要求の発行はこれらの主要部分に分割できます。

>[!NOTE]
>[ADFS ヘルプ](https://adfshelp.microsoft.com)サイトの[ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest)を使用して、要求の問題のトラブルシューティングを行うことができます。

## <a name="token-request"></a>トークンが要求
証明書利用者にアクセスすると、トークン要求を使用して AD FS にリダイレクトされます。  要求で問題が発生する可能性があります。  特に重要なものは、

### <a name="the-request-formatting-with-3rd-parties-particularly-saml"></a>サードパーティによる要求の書式設定 (特に SAML)

### <a name="pre-formated-urls-that-have-typos"></a>誤字を含む Url を事前に設定する
Federaion 証明書利用者からトークンを発行するときに、トークン要求に URL クエリ文字列パラメーターが含まれています。  証明書利用者が AD FS にリダイレクトするときに、その URL に正しいパラメーターが指定されていない場合、要求に問題が発生する可能性があります。


トークン形式を verifiy するために、web デバッガーツールを使用できます。


## <a name="token-response"></a>トークン応答

## <a name="authentication"></a>認証

## <a name="claim-rule-processing"></a>要求規則の処理