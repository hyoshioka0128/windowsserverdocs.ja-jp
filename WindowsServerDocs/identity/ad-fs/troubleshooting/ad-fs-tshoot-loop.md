---
title: AD FS トラブルシューティング-ループ検出
description: このドキュメントでは、ループ検出をトラブルシューティングする方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.openlocfilehash: e3d654f44ba75d9b647c0c1d9db7345c7ea75435
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953092"
---
# <a name="ad-fs-troubleshooting---loop-detection"></a>AD FS トラブルシューティング-ループ検出

AD FS のループは、証明書利用者が有効なセキュリティトークンを継続的に拒否し、AD FS にリダイレクトするときに発生します。

## <a name="loop-detection-cookie"></a>ループ検出クッキー
これが起こらないように、AD FS では、ループ検出クッキーと呼ばれるものが実装されています。 既定では、AD FS は**MSISLoopDetectionCookie**という名前の web パッシブクライアントに cookie を書き込みます。 この cookie には、タイムスタンプ値と、発行されたトークンの数が格納されます。  これにより、AD FS が特定の期間内にクライアントがフェデレーションサービスにアクセスした頻度と回数を追跡できます。

パッシブクライアントがトークンのフェデレーションサービスを20秒以内に5回アクセスする場合、AD FS は次のエラーをスローします。

**MSIS7042: 同じクライアントブラウザーセッションが {0} 最後の ' ' 秒間に ' ' 要求を行いました {1} 。詳細については、管理者に問い合わせてください。**

無限ループに入るのは、多くの場合、AD FS によって発行されたトークンを正常に使用できない、正常に動作していない証明書利用者アプリケーションによって発生し、アプリケーションが新しいトークンに対して AD FS にパッシブクライアントを繰り返し送信しているためです。  AD FS は、20秒以内に5つの要求を超えない限り、パッシブクライアントに毎回新しいトークンを発行します。

## <a name="adjusting-the-loop-detection-cookie"></a>ループ検出クッキーの調整
PowerShell を使用して、発行されるトークンの数と timespan 値を変更できます。

```powershell
Set-AdfsProperties -LoopDetectionMaximumTokensIssuedInterval 5  -LoopDetectionTimeIntervalInSeconds 20
```
**LoopDetectionMaximumTokensIssuedInterval**の最小値は1です。

**LoopDetectionTimeIntervalInSeconds**の最小値は5です。

また、パフォーマンステストを実行するときにループ検出を無効にすることもできます。

```powershell
Set-AdfsProperties -EnableLoopDetection $false
```

>[!IMPORTANT]
>ループの検出を完全に無効にすることはお勧めしません。これにより、ユーザーが無限ループ状態に入るのを防ぐことができます。


## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)



