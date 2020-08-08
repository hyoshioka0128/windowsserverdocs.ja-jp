---
title: AD FS 禁止 IP アドレスの構成
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 06/28/2018
ms.topic: article
ms.openlocfilehash: e5cb939fcf862d16837c2f9e05548644faf3bf71
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956489"
---
# <a name="ad-fs-and-banned-ip-addresses"></a>AD FS と禁止された IP アドレス


2018年6月に、Windows Server 2016 の AD FS では、AD FS 6 月の2018更新プログラムで禁止された**ip**が導入されました。  この更新プログラムを使用すると、AD FS でグローバルに IP アドレスのセットを構成できます。これにより、これらの IP アドレスから送信された要求や、 **x 転送**された-**クライアント-ip**ヘッダー内の ip アドレスを持つ要求が AD FS によってブロックされるようになります。

## <a name="adding-banned-ips"></a>禁止 Ip の追加
禁止された Ip をグローバルリストに追加するには、次の Powershell コマンドレットを使用します。

``` powershell
PS C:\ >Set-AdfsProperties -AddBannedIps "1.2.3.4", "::3", "1.2.3.4/16"
```

許可される形式

1.  IPv4
2.  IPv6
3.  IPv4 または v6 を使用した CIDR 形式

禁止された IP アドレスには、300エントリの制限があります。 CIDR または範囲形式を使用すると、エントリの大きなブロックを1つのエントリで拒否できます。

## <a name="removing-banned-ips"></a>禁止 Ip の削除
グローバルリストから禁止 Ip を削除するには、次の Powershell コマンドレットを使用します。

``` powershell
PS C:\ >Set-AdfsProperties -RemoveBannedIps "1.2.3.4"
```

#### <a name="read-banned-ips"></a>禁止 Ip の読み取り
現在禁止されている IP アドレスのセットを読み取るには、次の Powershell コマンドレットを使用します。

``` powershell
PS C:\ >Get-AdfsProperties
```

出力例:

```
BannedIpList                   : {1.2.3.4, ::3,1.2.3.4/16}
```



## <a name="additional-references"></a>その他の参照情報
[Active Directory フェデレーションサービス (AD FS) をセキュリティで保護するためのベストプラクティス](../../ad-fs/deployment/best-practices-securing-ad-fs.md)

[Set-adfsproperties](/powershell/module/adfs/set-adfsproperties?view=win10-ps)

[AD FS の運用](../ad-fs-operations.md)
