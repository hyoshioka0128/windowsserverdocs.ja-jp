---
title: AD FS のトラブルシューティング - 要求の発行
description: このドキュメントが AD FS トークンの発行に関する問題のトラブルシューティング方法について説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fdf8851fe9b35f82191458ba3313fda2dc3ee4cf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839663"
---
# <a name="ad-fs-troubleshooting---claims-issuance"></a>AD FS のトラブルシューティング - 要求の発行
クレームは、ステートメント自体または別の方法により、その 1 つのサブジェクトが対象です。  要求は、証明書利用者のパーティによって発行し、1 つまたは複数の値が指定され、AD FS サーバーによって発行されるセキュリティ トークンにパッケージ化します。  このプロセスで複数の移動パーツがあるためは、これらのキー部分に要求の発行が分割ことができます。

>[!NOTE]  
>使用することができます[ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest)上、 [ADFS ヘルプ](https://adfshelp.microsoft.com)要求の問題のトラブルシューティングに役立つサイト。   

## <a name="token-request"></a>トークン要求
証明書利用者のパーティに移動するとするトークンの要求に AD FS にリダイレクトされます。  要求に問題が発生することができます。  最も顕著なは。

### <a name="the-request-formatting-with-3rd-parties-particularly-saml"></a>サード パーティ (SAML では特に) との書式設定要求

### <a name="pre-formated-urls-that-have-typos"></a>入力ミスがある事前形式の Url
WS Federaion 証明書利用者からトークンを発行するときにそのトークンの要求は、URL クエリ文字列パラメーターの間では。  場合は、証明書利用者は、要求に問題が発生し、AD FS にリダイレクトが発生したら、適切なパラメーターをその URL に指定されていません。


トークンの形式のことを確認する順番は、web のデバッガー ツールを使用できます。


## <a name="token-response"></a>トークン応答

## <a name="authentication"></a>認証

## <a name="claim-rule-processing"></a>要求ルールの処理