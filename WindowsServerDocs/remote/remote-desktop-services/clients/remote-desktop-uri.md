---
title: リモート デスクトップ クライアントの URI スキーム
description: リモート デスクトップ クライアントの Uniform Resource Identifier スキームについて説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c3f1eb6-835c-4522-99ff-56c6ee4bb911
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: f2934fed43c8f4feec2f321d684cc3593933eb5d
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297471"
---
# リモート デスクトップ クライアント ユニバーサル リソース識別子 (URI) スキームをサポートします。

>適用対象: Windows Server バージョン 1803、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

Uniform Resource Identifier (URI) スキームを有効にすると、IT 担当者と開発者のプラットフォーム間でリモート デスクトップ クライアントの機能を統合する方法を提供し、ことを許可するユーザー エクスペリエンスの向上します。 

- サード パーティ製アプリケーションを Microsoft リモート デスクトップを起動し、定義済みの設定が (URI 文字列の一部として提供される) でリモート セッションを開始します。
- エンドユーザーが事前に構成された Url を使用してリモート接続を開始します。

>[!NOTE]
> Windows オペレーティング システムの URI を使用して、RD クライアントに接続はサポートされていません:、MacOS、iOS、Android デバイスと、URI を使用します。

Microsoft リモート デスクトップでは、URI スキーム rdp://query_string を使用して、クライアントを起動するときに使用される事前構成済みの属性の設定を保存します。 クエリ文字列は、1 つまたは URL で提供される RDP 属性のセットを表します。 

RDP 属性は、アンパサンド記号 (&) で区切られます。 たとえば、PC に接続するは、文字列を示します。

```
rdp://full%20address=s:mypc:3389&audiomode=i:2&disable%20themes=i:1
```

この表では、iOS、Mac、Android のリモート デスクトップ クライアントで使用できる、サポートされている属性の完全な一覧を示します。 (プラットフォーム] 列で"x"は、属性がサポートされていることを示します。 山かっこ (<>) で示される値を表すリモート デスクトップ クライアントによってサポートされている値。)

| **RDP 属性**                                           | **Android** | **Mac** | **iOS** |
|---------------------------------------------------------|---------|-----|-----|
| デスクトップ コンポジションを許可する i =:&lt;0 または 1&gt;                    | x       | x   | x   |
| フォントのスムージング = i:<0 または 1&gt;                         | x       | x   | x   |
| 別のシェル = s:&lt;文字列&gt;                              | x       | x   | x   |
| [audiomode i =:&lt;0、1、または 2&gt;](https://technet.microsoft.com/library/ff393707.aspx)                                | x       | x   | x   |
| [認証レベル i =:&lt;0 または 1&gt;](https://technet.microsoft.com/library/ff393709.aspx)                         | x       | x   | x   |
| コンソールに接続 i =:&lt;0 または 1&gt;                           | x       | x   | x   |
| カーソルの設定を無効にする i =:&lt;0 または 1&gt;                      | x       | x   | x   |
| フル ウィンドウのドラッグを無効にする i =:&lt;0 または 1&gt;                     | x       | x   | x   |
| メニュー anims を無効にする i =:&lt;0 または 1&gt;                           | x       | x   | x   |
| テーマを無効にする i =:&lt;0 または 1&gt;                               | x       | x   | x   |
| 壁紙を無効にする i =:&lt;0 または 1&gt;                            | x       | x   | x   |
| [drivestoredirect = s: *](https://technet.microsoft.com/library/ff393728(v=ws.10).aspx)(これは、サポートされている唯一の値) | x       | x   |     |
| [desktopheight i =:&lt;ピクセル単位の値&gt;](https://technet.microsoft.com/library/ff393702.aspx)                       |         | x   |     |
| [desktopwidth i =:&lt;ピクセル単位の値&gt;](https://technet.microsoft.com/library/ff393697.aspx)                        |         | x   |     |
| [ドメイン = s:&lt;文字列&gt;](https://technet.microsoft.com/library/ff393673.aspx)                           | x | x | x |
| [完全なアドレス = s:&lt;文字列&gt;](https://technet.microsoft.com/library/ff393661.aspx)                     | x | x | x |
| gatewayhostname = s:&lt;文字列&gt;                  | x | x | x |
| [gatewayusagemethod i =:&lt;1 または 2&gt;](https://msdn.microsoft.com/aa381329.aspx)               | x | x | x |
| [クライアントでの資格情報の入力を求める i =:&lt;0 または 1&gt;](https://technet.microsoft.com/library/ff393660(v=ws.10).aspx) |   | x |   |
| [loadbalanceinfo = s:&lt;文字列&gt;](https://technet.microsoft.com/library/ff393684.aspx)                  | x | x | x |
| [redirectprinters i =:&lt;0 または 1&gt;](https://technet.microsoft.com/library/ff393671(v=ws.10).aspx)                 |   | x |   |
| remoteapplicationcmdline = s:&lt;文字列&gt;         | x | x | x |
| remoteapplicationmode i =:&lt;0 または 1&gt;            | x | x | x |
| remoteapplicationprogram = s:&lt;文字列&gt;         | x | x | x |
| シェルの作業ディレクトリ = s:&lt;文字列&gt;          | x | x | x |
| リダイレクト サーバー名を使用する i =:&lt;0 または 1&gt;      | x | x | x |
| [ユーザー名 = s:&lt;文字列&gt;](https://technet.microsoft.com/library/ff393678.aspx)                         | x | x | x |
| [スクリーン モード id = i:&lt;1 または 2&gt;](https://technet.microsoft.com/library/ff393692.aspx)                   |   | x |   |
| [セッション bpp i =:&lt;8、15、16、24、または 32&gt;](https://technet.microsoft.com/library/ff393680.aspx)        |   | x |   |
| [multimon の実行時に使う i =:&lt;0 または 1&gt;](https://technet.microsoft.com/library/ff393695(v=ws.10).aspx)          |   | x |   |