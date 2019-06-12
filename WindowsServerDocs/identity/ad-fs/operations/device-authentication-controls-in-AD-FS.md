---
title: AD FS でデバイス認証の制御
description: このドキュメントは、Windows Server 2016 と 2012 R2 の AD FS でデバイス認証を有効にする方法を説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/09/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f52d3d237573e4ed0028e228ff80273862a0aaf2
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444645"
---
# <a name="device-authentication-controls-in-ad-fs"></a>AD FS でデバイス認証の制御
次のドキュメントでは、Windows Server 2016 と 2012 R2 でデバイス認証の制御を有効にする方法を示します。

## <a name="device-authentication-controls-in-ad-fs-2012-r2"></a>AD FS 2012 R2 でデバイス認証の制御
AD FS 2012 R2 のグローバル認証プロパティと呼ばれる 1 つを使用する必要がある最初の`DeviceAuthenticationEnabled`制御されたデバイスを認証します。

設定を構成する、`Set-AdfsGlobalAuthenticationPolicy`コマンドレットは、次のようを使用しました。


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```



デバイス認証を無効にするには、同じコマンドレットは、値を $false に設定に使用されました。

## <a name="device-authentication-controls-in-ad-fs-2016"></a>Ad FS 2016 デバイス認証の制御
2012 R2 でサポートされるデバイスの認証の唯一の種類では、しの clientTLS はでした。  Ad FS 2016 でし、clientTLS に加えては最新のデバイス認証に対してデバイス認証の 2 つの新しい型です。  それらを次に示します。
- PKeyAuth
- PRT

新しい動作を制御する、`DeviceAuthenticationEnabled`プロパティがという名前の新しいプロパティと組み合わせて使用`DeviceAuthenticationMethod`します。  

デバイスの認証方法は、実行するデバイスの認証の種類を決定します。PRT、PKeyAuth、しの clientTLS は、またはそれらの組み合わせ。
次の値があります。
 - SignedToken:PRT のみ
 - PKeyAuth:PRT + PKeyAuth
 - ClientTLS は:PRT + し clientTLS
 - すべて:上記以外のすべて

ご覧のとおり、PRT の一部であるすべてのデバイス認証方法は常に既定の方法に影響する場合に有効になっている`DeviceAuthenticationEnabled`に設定されている`$true`します。

以下に例を示します。メソッドを構成するには、新しいプロパティと共に、上、として DeviceAuthenticationEnabled コマンドレットを使用します。

``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```

>[!NOTE]
> ADFS の 2019年で`DeviceAuthenticationMethod`で使用できる、`Set-AdfsRelyingPartyTrust`コマンド。

``` powershell
PS:\>Set-AdfsRelyingPartyTrust -DeviceAuthenticationMethod ClientTLS
```

>[!NOTE]
> デバイス認証を有効にする (設定`DeviceAuthenticationEnabled`に`$true`) ことを意味、`DeviceAuthenticationMethod`に暗黙的に設定されている`SignedToken`に相当する**PRT**します。


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationMethod All
```
> [!NOTE]
> 既定のデバイスの認証方法は`SignedToken`します。  他の値は**PKeyAuth、** <strong>し ClientTLS、</strong>と**すべて**します。

意味、 `DeviceAuthenticationMethod` AD FS 2016 がリリースされてから、値が若干変更されました。  更新プログラムのレベルに応じて、各値の意味は、以下の表を参照してください。


|AD FS のバージョン|DeviceAuthenticationMethod 値|意味|
| ----- | ----- | ----- |
|2016 RTM|SignedToken|PRT + PkeyAuth|
||clientTLS|clientTLS|
||すべての|PRT + PkeyAuth し clientTLS|
|2016 RTM +、Windows Update と日付の最大|SignedToken (つまり、変更された)|PRT (のみ)|
||PkeyAuth (新規)|PRT + PkeyAuth|
||clientTLS|PRT + し clientTLS|
||すべての|PRT + PkeyAuth し clientTLS|

## <a name="see-also"></a>関連項目
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
