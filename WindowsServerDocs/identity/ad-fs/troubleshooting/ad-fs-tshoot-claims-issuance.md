---
title: AD FS のトラブルシューティング-要求の発行
description: このドキュメントでは、AD FS によるトークンの発行に関する問題をトラブルシューティングする方法について説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ea0e6112f00f9cace6a0c580661a5319b5adaea5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366241"
---
# <a name="ad-fs-troubleshooting---claims-issuance"></a>AD FS のトラブルシューティング-要求の発行
クレームは、1つのサブジェクトがそれ自体または別のサブジェクトに対して行うステートメントです。  要求は証明書利用者によって発行され、1つまたは複数の値が与えられ、AD FS サーバーによって発行されたセキュリティトークンにパッケージ化されます。  このプロセスにはいくつかの可動要素があるため、要求の発行はこれらの主要部分に分割できます。

>[!NOTE]  
>[ADFS ヘルプ](https://adfshelp.microsoft.com)サイトの[ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest)を使用して、要求の問題のトラブルシューティングを行うことができます。   

## <a name="token-request"></a>トークン要求
証明書利用者にアクセスすると、トークン要求を使用して AD FS にリダイレクトされます。  要求で問題が発生する可能性があります。  特に重要なものは次のとおりです。

### <a name="the-request-formatting-with-3rd-parties-particularly-saml"></a>サードパーティによる要求の書式設定 (特に SAML)

### <a name="pre-formated-urls-that-have-typos"></a>誤字を含む Url を事前に設定する
Federaion 証明書利用者からトークンを発行するときに、トークン要求に URL クエリ文字列パラメーターが含まれています。  証明書利用者が AD FS にリダイレクトするときに、その URL に正しいパラメーターが指定されていない場合、要求に問題が発生する可能性があります。


トークン形式を verifiy するために、web デバッガーツールを使用できます。


## <a name="token-response"></a>トークン応答

## <a name="authentication"></a>認証

## <a name="claim-rule-processing"></a>要求規則の処理