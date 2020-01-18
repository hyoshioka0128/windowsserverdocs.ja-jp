---
title: リモート デスクトップ クライアント
description: すべてのデバイスで使うことができるさまざまなリモート デスクトップ クライアントについて説明します
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7d8158c-aee1-4c60-8a46-40ce5595b8e8
author: HeidiLohr
manager: lizross
ms.author: helohr
ms.date: 01/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: ccf6fa376bfb54498851407bfae175736e75ebc9
ms.sourcegitcommit: 76469d1b7465800315eaca3e0c7f0438fc3939ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919849"
---
# <a name="remote-desktop-clients"></a>リモート デスクトップ クライアント

>適用先:Windows 10、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

Microsoft リモート デスクトップ クライアントを使用すると、リモート PC や仕事用リソースに接続できます。使用できるデバイスに制限はほとんどなく、場所もほぼどこからでも接続できます。 仕事用 PC に接続して、自分のデスクで作業しているときと同じように、すべてのアプリ、ファイル、ネットワーク リソースを利用できます。 RD クライアントを使用するだけで、職場でアプリを開いたままにしておいて、そのアプリを自宅で表示できます。

開始する前にあることを確認するチェック アウト、 [サポートされる構成](remote-desktop-supported-config.md) にリモート デスクトップ クライアントを使用して接続できる Pc について説明する記事です。 [クライアント FAQ](remote-desktop-client-faq.md) も確認してください。

次のクライアント アプリを利用できます。

| デバイス          | アプリの入手                                                                                                  | セットアップ手順                                                                |
|-----------------|-----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| Windows デスクトップ | [Windows デスクトップ クライアント](windowsdesktop.md#install-the-client)                                               | [Windows デスクトップ クライアントの概要](windowsdesktop.md) |
| Windows ストア   | [Microsoft Store の Windows 10 クライアント](https://go.microsoft.com/fwlink/?LinkID=616709)                   | [Microsoft Store クライアントの概要](windows.md)          |
| Android         | [Google Play の Android クライアント](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)     | [Android クライアントの概要](remote-desktop-android.md) |
| iOS             | [iTunes ストアの iOS クライアント](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8)     | [iOS クライアントの概要](remote-desktop-ios.md)         |
| macOS           | [iTunes ストアの macOS クライアント](https://itunes.apple.com/app/microsoft-remote-desktop/id1295203466?mt=12) | [macOS クライアントの概要](remote-desktop-mac.md)       |

## <a name="configuring-the-remote-pc"></a>リモート PC の構成

リモートでアクセスする前にリモート PC を構成するには、[PC へのアクセスを許可します](remote-desktop-allow-access.md)。

## <a name="remote-desktop-client-uri-scheme"></a>リモート デスクトップ クライアントの URI スキーム

統一リソース識別子 (URI) スキームを有効にすると、プラットフォーム間でリモート デスクトップ クライアントの機能を統合できます。 チェック アウト、 [URI 属性をサポートされている](remote-desktop-uri.md) iOS、Mac、および Android クライアントで使用できます。
