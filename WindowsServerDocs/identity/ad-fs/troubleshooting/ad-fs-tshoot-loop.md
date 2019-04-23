---
title: AD FS のトラブルシューティング - ループが検出
description: このドキュメントは、ループの検出のトラブルシューティングを行う方法を説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cc8eeb11e44da3b8f26b1ab94143c189bca9ed38
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830913"
---
# <a name="ad-fs-troubleshooting---loop-detection"></a>AD FS のトラブルシューティング - ループが検出 
 
AD FS でのループには、証明書利用者は継続的に有効なセキュリティ トークンを拒否し、AD FS にリダイレクトするときに発生します。

## <a name="loop-detection-cookie"></a>ループ検出 cookie
これが事態を防ぐためにループ検出 cookie と呼ばれる AD FS を実装しました。 既定では、AD FS は web のパッシブ クライアントという名前にクッキーを書き込みます**MSISLoopDetectionCookie**します。 この cookie はタイムスタンプ値を保持し、トークンの数は、値を発行します。  これにより、AD FS の特定の期間内のフェデレーション サービスが何度もクライアントにアクセスしたどのくらいの頻度とどのように追跡できます。

パッシブ クライアントにアクセスする場合は 5 倍 (5) 内で 20 秒、AD FS トークンをフェデレーション サービスに、次のエラーがスローされます。

**MSIS7042:同じクライアント ブラウザー セッションが行われた '{0}'、最後の要求'{1}' 秒。詳細については、管理者にお問い合わせください。**

誤動作が、AD FS によって発行されたトークンは正常に使用していないことをアプリケーションに証明書利用者によって多くの場合、原因は、無限ループに入ると、アプリケーションが送信パッシブ クライアント、AD FS に繰り返し、新しいトークンです。  AD FS はパッシブ クライアント新しいトークンが発行するたびに、20 秒で 5 つの要求を超えていない限り、します。 

## <a name="adjusting-the-loop-detection-cookie"></a>ループの検出の cookie を調整します。
PowerShell を使用して、トークンの発行元の値および timespan の値の数を変更することができます。

```powershell
Set-AdfsProperties -LoopDetectionMaximumTokensIssuedInterval 5  -LoopDetectionTimeIntervalInSeconds 20
```
最小値**LoopDetectionMaximumTokensIssuedInterval**は 1 です。

最小値**LoopDetectionTimeIntervalInSeconds**は 5 です。

パフォーマンス テストを行っているときも、ループの検出を無効にすることができます。

```powershell
Set-AdfsProperties -EnableLoopDetection $false
```

>[!IMPORTANT]
>これは、無限ループ状態に入るをユーザーが妨げられるこのループの検出を完全に無効にすること勧めしません。


## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)



