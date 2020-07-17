---
title: リモート デスクトップの URI のスキーマ
description: リモート デスクトップ クライアントの Uniform Resource Identifier スキームについて説明します
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 0c3f1eb6-835c-4522-99ff-56c6ee4bb911
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 06/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: aadb115c68108125abdaf980c12eac951d798bba
ms.sourcegitcommit: df94dac422d13566c32e1cdb8c6e7a4e82747947
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84205613"
---
# <a name="remote-desktop-uri-scheme"></a>リモート デスクトップの URI のスキーマ

> 適用先:Windows Server バージョン 1803、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

このドキュメントでは、リモート デスクトップの URI (Uniform Resource Identifier) の形式を定義します。 これらの URI スキームを使用すると、さまざまなコマンドを使用してリモート デスクトップ クライアントを呼び出すことができます。

## <a name="ms-rd-uri-scheme"></a>ms-rd URI スキーム

>[!NOTE]
> ms-rd URI スキームは、現在、Windows デスクトップ クライアント (MSRDC) でのみサポートされています。

ms-rd URI には、次の形式を使用して、クライアントのコマンドとコマンドに固有のパラメーターのセットを指定するオプションが用意されています。

```
ms-rd:command?parameters
```

パラメーターでは、キー = 値のペアのクエリ文字列形式を & で区切って使用して、指定されたコマンドに関する追加情報を提供します。

```
param1=value1&param2=value2&…
```

### <a name="commands-and-parameters"></a>コマンドとパラメーター

現在サポートされているコマンドとそれに対応するパラメーターの一覧を次に示します。

コマンドを指定せずに `ms-rd:` を使用すると、クライアントが起動されます。

#### <a name="subscribe"></a>Subscribe

このコマンドは、クライアントを起動し、サブスクリプション プロセスを開始します。

**コマンド名:** subscribe

**コマンドのパラメーター:**

| パラメーター | 説明                  | 値 |
|-----------|------------------------------|--------|
| url       | ワークスペースの URL を指定します。 | <https://contoso.com> などの有効な URL。 |

**例:** ms-rd:subscribe?url=https://contoso.com

## <a name="legacy-rdp-uri-scheme"></a>レガシ rdp URI スキーム

>[!NOTE]
> 次の URI スキームは、macOS、iOS、および Android デバイス用のクライアントでのみサポートされています。 これは、上記の新しい ms rd URI に置き換えられています。

Microsoft リモート デスクトップでは、URI スキーム rdp://query_string を使用して、クライアントを起動するときに使用される事前構成されている属性の設定を格納します。 クエリ文字列は、URL で指定する単一または一連の RDP 属性を表します。

RDP 属性は、アンパサンド記号で区切ります (&)。 たとえば、PC に接続する場合、文字列は次のようになります。

```
rdp://full%20address=s:mypc:3389&audiomode=i:2&disable%20themes=i:1
```

次の表に、iOS、Mac、Android のリモート デスクトップ クライアントで使うことができる、サポートされている属性の完全な一覧を示します (プラットフォームの列の "x" は属性がサポートされていることを示します。 山かっこ (<>) 内の値は、リモート デスクトップ クライアントでサポートされている値を表します)。

| RDP 属性                                           | Android | Mac | iOS |
|---------------------------------------------------------|---------|-----|-----|
| allow desktop composition=i:&lt;0 または 1&gt;              | x       | x   | x   |
| allow font smoothing=i:<0 または 1&gt;                      | x       | x   | x   |
| alternate shell=s:&lt;文字列&gt;                        | x       | x   | x   |
| [audiomode=i:&lt;0、1、または 2&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393707(v=ws.10)) | x       | x   | x   |
| [authentication level=i:&lt;0 または 1&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393709(v=ws.10)) | x       | x   | x   |
| connect to console=i:&lt;0 または 1&gt;                     | x       | x   | x   |
| disable cursor settings=i:&lt;0 または 1&gt;                | x       | x   | x   |
| disable full window drag=i:&lt;0 または 1&gt;               | x       | x   | x   |
| disable menu anims=i:&lt;0 または 1&gt;                     | x       | x   | x   |
| disable themes=i:&lt;0 または 1&gt;                         | x       | x   | x   |
| disable wallpaper=i:&lt;0 または 1&gt;                      | x       | x   | x   |
| [drivestoredirect = s: *](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393728(v=ws.10)) (これは、唯一サポートされる値です) | x       | x   |     |
| [desktopheight=i:&lt;ピクセル単位の値&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393702(v=ws.10)) |         | x   |     |
| [desktopwidth=i:&lt;ピクセル単位の値&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393697(v=ws.10))  |         | x   |     |
| [domain=s:&lt;文字列&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393673(v=ws.10))                 | x | x | x |
| [full address=s:&lt;文字列&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393661(v=ws.10))           | x | x | x |
| gatewayhostname=s:&lt;文字列&gt;                  | x | x | x |
| [gatewayusagemethod=i:&lt;1 または 2&gt;](https://docs.microsoft.com/windows/win32/termserv/imsrdpclienttransportsettings-gatewayusagemethod)                | x | x | x |
| [prompt for credentials on client=i:&lt;0 または 1&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393660(v=ws.10)) |   | x |   |
| [loadbalanceinfo=s:&lt;文字列&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393684(v=ws.10))                  | x | x | x |
| [redirectprinters=i:&lt;0 または 1&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393671(v=ws.10))                 |   | x |   |
| remoteapplicationcmdline=s:&lt;文字列&gt;         | x | x | x |
| remoteapplicationmode=i:&lt;0 または 1&gt;            | x | x | x |
| remoteapplicationprogram=s:&lt;文字列&gt;         | x | x | x |
| shell working directory=s:&lt;文字列&gt;          | x | x | x |
| Use redirection server name=i:&lt;0 または 1&gt;      | x | x | x |
| [username=s:&lt;文字列&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393678(v=ws.10))                  | x | x | x |
| [screen mode id=i:&lt;1 または 2&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393692(v=ws.10))            |   | x |   |
| [session bpp=i:&lt;8、15、16、24、または 32&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393680(v=ws.10)) |   | x |   |
| [use multimon=i:&lt;0 または 1&gt;](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff393695(v=ws.10))              |   | x |   |
