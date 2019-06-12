---
title: リモート デスクトップ - クライアント アプリの比較
description: 別の RD アプリがに関してはサポートされている機能と機能を比較する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12efe858-6b76-4e08-9f72-b9603aceb0fc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0e001b590f524711185e3dd70db3bc52a9b8d9af
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447127"
---
# <a name="compare-the-client-apps"></a>クライアント アプリを比較します。

>適用対象:Windows 10、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

別のリモート デスクトップ クライアント アプリのと比較多くの場合、求めます。 同じ操作を行うすべての操作を行いますか。 ここでは、それらの質問に対する回答をします。

## <a name="redirection-support"></a>リダイレクトのサポート

次の表では、デバイスと Remote Desktop Connection アプリ、ユニバーサル アプリ、Android アプリ、ios、macOS アプリと web クライアントでは、他のリダイレクトのサポートを比較します。 これらのテーブルでは、リモート セッションで 1 回にアクセスできるリダイレクトについて説明します。 

場合するパーソナル デスクトップにリモートであるで構成できる追加のリダイレクト、**追加設定**セッション。 リモート デスクトップまたはアプリが組織に管理されている場合、管理者は有効または、グループ ポリシー設定でリダイレクトを無効にできます。

### <a name="input-redirection"></a>入力のリダイレクト

| リダイレクト | リモート デスクトップ<br> 接続 | ユニバーサル | Android | iOS | macOS |          web クライアント           |
|-------------|-------------------------------|-----------|---------|-----|-------|-------------------------------|
|  キーボード   |               x               |     X     |    X    |  X  |   X   |               x               |
|    マウス    |               x               |     X     |    x    | X\* |   x   |               x               |
|    タッチ    |               x               |     X     |    X    |  x  |       | X (Edge、IE はサポートされません) |
|    その他    |              ペン              |           |         |     |       |                               |

* 表示、 [iOS Beta のリモート デスクトップ クライアントでサポートされる入力デバイスの一覧](remote-desktop-ios.md#supported-input-devices)します。

### <a name="port-redirection"></a>ポートのリダイレクト   

| リダイレクト | リモート デスクトップ <br>接続 | ユニバーサル | Android | iOS | macOS | web クライアント |
|-------------|-------------------------------|-----------|---------|-----|-------|------------|
| シリアル ポート | x                             |           |         |     |       |            |
| USB         | x                             |           |         |     |       |            |

USB ポートのリダイレクトを有効にすると、USB ポートに接続されているすべての USB デバイスは、リモート セッションで自動的に認識されます。

### <a name="other-redirection-devices-etc"></a>(デバイスなど) は、その他のリダイレクト



| リダイレクト         | リモート デスクトップ接続 | ユニバーサル   | Android | iOS         | macOS                                    | web クライアント    |
|---------------------|---------------------------|-------------|---------|-------------|------------------------------------------|---------------|
| カメラ             | x                         |             |         |             |                                          |               |
| クリップボード           | x                         | テキスト、イメージ | text    | テキスト、イメージ | x                                        | text          |
| ローカル ドライブのストレージ | x                         |             | x       |             | ○                                        |               |
| Location            | x                         |             |         |             |                                          |               |
| マイク         | x                         |X            |         |             | x                                        |               |
| プリンター            | x                         |             |         |             | X (CUP のみ)                            | PDF 印刷     |
| スキャナー            | x                         |             |         |             |                                          |               |
| スマート カード         | x                         |             |         |             | X (Windows 認証がサポートされていません) |               |
| スピーカー            | x                         | X           | X       | X           | x                                        | X (IE) を除く |

* のプリンターのリダイレクトは、macOS アプリは、既定で発行元のイメージ セッターのプリンター ドライバーをサポートします。 ネイティブのプリンター ドライバーのリダイレクトがサポートしていません。
