---
title: 構成の AD FS には、記述した IP アドレスが禁止されています
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/28/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 01ef992554a1e0961d8d795e9baa7730a1a1d682
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189889"
---
# <a name="ad-fs-and-banned-ip-addresses"></a>AD FS と禁止された IP アドレスします。


2018 年 6 月に、Windows Server 2016 での AD FS が導入された**Ip の禁止**と AD FS の 2018 年 6 月の更新します。  この更新プログラムを使用する AD FS でグローバルに一連の IP アドレスを構成またはこれらの IP アドレスからの要求にこれらの IP アドレスがあるように、 **x-転送-の**または**x ms-転送-クライアントの ip**ヘッダーは、AD FS によってブロックされます。

## <a name="adding-banned-ips"></a>禁止の ip アドレスを追加します。
グローバル リストに禁止されている ip アドレスを追加するを使用して、以下の Powershell コマンドレット。

``` powershell
PS C:\ >Set-AdfsProperties -AddBannedIps "1.2.3.4", "::3", "1.2.3.4/16"
```

許可されている形式

1.  IPv4
2.  IPv6
3.  CIDR 形式では、IPv4 または v6

禁止されている IP アドレスのエントリを 300 の制限があります。 CIDR または範囲の形式を使用すると、大きなブロックを 1 つのエントリを持つエントリを拒否します。

## <a name="removing-banned-ips"></a>禁止の ip アドレスを削除します。
グローバル リストから、禁止されている ip アドレスを削除するを使用して、以下の Powershell コマンドレット。

``` powershell
PS C:\ >Set-AdfsProperties -RemoveBannedIps "1.2.3.4"
```

#### <a name="read-banned-ips"></a>読み取り禁止の ip アドレス
現在禁止されている IP アドレスのセットを読み取るには、以下の Powershell コマンドレット。

``` powershell
PS C:\ >Get-AdfsProperties 
```

出力の例:

```
BannedIpList                   : {1.2.3.4, ::3,1.2.3.4/16}
```



## <a name="additional-references"></a>その他の参照情報  
[Active Directory フェデレーション サービスをセキュリティで保護するためのベスト プラクティス](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-adfsproperties](https://technet.microsoft.com/itpro/powershell/windows/adfs/set-adfsproperties)

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
