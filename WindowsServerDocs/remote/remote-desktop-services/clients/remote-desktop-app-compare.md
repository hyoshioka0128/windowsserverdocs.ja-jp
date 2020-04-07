---
title: リモート デスクトップ - クライアントの比較
description: さまざまな RD クライアントを、サポートされている機能に関して比較します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12efe858-6b76-4e08-9f72-b9603aceb0fc
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 03/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 11c91ac951db27915d9313f7f98e5e2cfc56b726
ms.sourcegitcommit: 78c00944b6990702d28bdcc4a9215927ca901bfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80440369"
---
# <a name="compare-the-clients"></a>クライアントの比較

>適用先:Windows 10、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

よく寄せられる質問の中に、さまざまなリモート デスクトップ クライアントの違いを尋ねるものがあります。 「これらの機能はすべて同じなのでしょうか?」 こうした質問に対する回答を以下に示します。

## <a name="redirection-support"></a>リダイレクトのサポート

次の表は、さまざまなクライアントについてデバイスとその他のリダイレクトのサポートを比較したものです。 これらの表には、リモート セッションに入ったときにアクセスできるリダイレクトが含まれています。

パーソナル デスクトップにリモート接続する場合、そのセッションの**追加設定**で構成できる追加のリダイレクトがあります。 リモート デスクトップまたはアプリが組織によって管理されている場合、管理者はグループ ポリシー設定または RDP プロパティでリダイレクトを有効または無効にできます。

### <a name="input-redirection"></a>入力のリダイレクト

| リダイレクト | Windows 受信トレイ</br>(MSTSC) | Windows デスクトップ</br>(MSRDC) | Windows ストア | Android | iOS | macOS | Web クライアント    |
|-------------|---------------------------|-----------------------------|---------------|---------|-----|-------|---------------|
| キーボード    | X                         | X                           | X             | X       | X   | X     | X             |
| マウス       | X                         | X                           | X             | X       | X\* | X     | X             |
| Touch       | X                         | X                           | X             | X       | X   |       | X (IE を除く) |
| ペン         | X                         | X                           |               |         |     |       |               |

*[リモート デスクトップ iOS クライアントでサポートされる入力デバイスの一覧](remote-desktop-ios.md#supported-input-devices)をご覧ください。

### <a name="port-redirection"></a>ポートのリダイレクト

| リダイレクト | Windows 受信トレイ</br>(MSTSC) | Windows デスクトップ</br>(MSRDC) | Windows ストア | Android | iOS | macOS | Web クライアント |
|-------------|---------------------------|-----------------------------|---------------|---------|-----|-------|------------|
| シリアル ポート | X                         | X                           |               |         |     |       |            |
| USB         | X                         | X                           |               |         |     |       |            |

USB ポートのリダイレクトを有効にすると、USB ポートに接続されている USB デバイスはすべて、リモート セッションで自動的に認識されます。

### <a name="other-redirection-devices-etc"></a>その他のリダイレクト (デバイスなど)

| リダイレクト         | Windows 受信トレイ</br>(MSTSC) | Windows デスクトップ</br>(MSRDC) | Windows ストア | Android | iOS         | macOS                           | Web クライアント    |
|---------------------|---------------------------|-----------------------------|---------------|---------|-------------|---------------------------------|---------------|
| カメラ             | X                         | X                           |               |         |             | X                               |               |
| クリップボード           | X                         | X                           | X             | テキスト    | テキスト、イメージ | X                               | テキスト          |
| ローカル ドライブ/ストレージ | X                         | X                           |               | X       |             | X                               |               |
| インストール先            | X                         | X                           |               |         |             |                                 |               |
| マイク         | X                         | X                           | X             |         |             | X                               |               |
| プリンター            | X                         | X                           |               |         |             | X (CUPS のみ)                   | PDF 印刷     |
| スキャナー            | X                         | X                           |               |         |             |                                 |               |
| Smart Cards         | X                         | X                           |               |         |             | X (Windows ログオンはサポートされていません) |               |
| Speakers            | X                         | X                           | X             | X       | X           | X                               | X (IE を除く) |

*プリンターのリダイレクト - macOS アプリでは、既定で Publisher Imagesetter のプリンター ドライバーがサポートされます。 ネイティブのプリンター ドライバーのリダイレクトはサポートされません。
