---
title: リモート デスクトップ - クライアント アプリの比較
description: さまざまな RD アプリを、サポートされている機能に関して比較します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 237bb79fae6460bc3b31fb1753e2d679c8d67512
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404170"
---
# <a name="compare-the-client-apps"></a>クライアント アプリの比較

>適用対象:Windows 10、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

よく寄せられる質問の中に、さまざまなリモート デスクトップ クライアント アプリの違いを尋ねるものがあります。 「これらの機能はすべて同じなのでしょうか?」 こうした質問に対する回答を以下に示します。

## <a name="redirection-support"></a>リダイレクトのサポート

以下の表では、リモート デスクトップ接続アプリ、ユニバーサル アプリ、Android アプリ、iOS アプリ、macOS アプリ、および Web クライアントでサポートされるデバイスなどのリダイレクトを比較しています。 これらの表には、リモート セッションに入ったときにアクセスできるリダイレクトが含まれています。 

パーソナル デスクトップにリモート接続する場合、そのセッションの**追加設定**で構成できる追加のリダイレクトがあります。 リモート デスクトップまたはアプリが組織によって管理されている場合、管理者はグループ ポリシー設定でリダイレクトを有効または無効にできます。

### <a name="input-redirection"></a>入力のリダイレクト

| リダイレクト | リモート デスクトップ<br> 接続 | ユニバーサル | Android | iOS | macOS |          Web クライアント           |
|-------------|-------------------------------|-----------|---------|-----|-------|-------------------------------|
|  キーボード   |               X               |     X     |    X    |  X  |   X   |               X               |
|    マウス    |               X               |     X     |    X    | X\* |   X   |               X               |
|    タッチ    |               X               |     X     |    X    |  X  |       | X (Microsoft Edge と IE はサポート対象外) |
|    その他    |              ペン              |           |         |     |       |                               |

*[リモート デスクトップ iOS クライアントのベータ版でサポートされる入力デバイスの一覧](remote-desktop-ios.md#supported-input-devices)をご覧ください。

### <a name="port-redirection"></a>ポートのリダイレクト   

| リダイレクト | リモート デスクトップ <br>接続 | ユニバーサル | Android | iOS | macOS | Web クライアント |
|-------------|-------------------------------|-----------|---------|-----|-------|------------|
| シリアル ポート | X                             |           |         |     |       |            |
| USB         | X                             |           |         |     |       |            |

USB ポートのリダイレクトを有効にすると、USB ポートに接続されている USB デバイスはすべて、リモート セッションで自動的に認識されます。

### <a name="other-redirection-devices-etc"></a>その他のリダイレクト (デバイスなど)



| リダイレクト         | リモート デスクトップ接続 | ユニバーサル   | Android | iOS         | macOS                                    | Web クライアント    |
|---------------------|---------------------------|-------------|---------|-------------|------------------------------------------|---------------|
| カメラ             | X                         |             |         |             |                                          |               |
| クリップボード           | X                         | テキスト、イメージ | テキスト    | テキスト、イメージ | X                                        | テキスト          |
| ローカル ドライブ/ストレージ | X                         |             | X       |             | ○                                        |               |
| Location            | X                         |             |         |             |                                          |               |
| マイク         | X                         |X            |         |             | X                                        |               |
| プリンター            | X                         |             |         |             | X (CUPS のみ)                            | PDF 印刷     |
| スキャナー            | X                         |             |         |             |                                          |               |
| スマート カード         | X                         |             |         |             | X (Windows 認証はサポート対象外) |               |
| スピーカー            | X                         | X           | X       | X           | X                                        | X (IE を除く) |

*プリンターのリダイレクト - macOS アプリでは、既定で Publisher Imagesetter のプリンター ドライバーがサポートされます。 ネイティブのプリンター ドライバーのリダイレクトはサポートされません。
