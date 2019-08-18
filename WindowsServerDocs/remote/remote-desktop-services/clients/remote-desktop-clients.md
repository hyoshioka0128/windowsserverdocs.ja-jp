---
title: リモート デスクトップ クライアント
description: すべてのデバイスで使うことができるさまざまなリモート デスクトップ クライアントについて説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7d8158c-aee1-4c60-8a46-40ce5595b8e8
author: HeidiLohr
manager: dougkim
ms.author: helohr
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: b7810d0b8b7cbd8d886b99a07d1419cb5e8197ed
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546410"
---
# <a name="remote-desktop-clients"></a>リモート デスクトップ クライアント

>適用対象:Windows 10、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

Microsoft リモート デスクトップ クライアントを使用すると、リモート PC や仕事用リソースに接続できます。使用できるデバイスに制限はほとんどなく、場所もほぼどこからでも接続できます。 仕事用 PC に接続して、自分のデスクで作業しているときと同じように、すべてのアプリ、ファイル、ネットワーク リソースを利用できます。 RD クライアントを使用するだけで、職場でアプリを開いたままにしておいて、そのアプリを自宅で表示できます。

開始する前に、リモート デスクトップ クライアントを使って接続できる PC について説明している[サポートされている構成](remote-desktop-supported-config.md)の記事を確認してください。 [クライアント FAQ](remote-desktop-client-faq.md) も確認してください。

次のクライアント アプリを利用できます。

| デバイス   | アプリを入手する                                                                                                     | セットアップ手順                                                                |
|----------|-----------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| Windows  | [Microsoft Store の Windows 10 クライアント](https://go.microsoft.com/fwlink/?LinkID=616709)                      | [Windows のリモート デスクトップの概要](windows.md)                |
| Android  | [Google Play の Android クライアント](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)        | [Android のリモート デスクトップ クライアントの概要](remote-desktop-android.md) |
| iOS      | [iTunes ストアの iOS クライアント](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8)     | [iOS のリモート デスクトップ クライアントの概要](remote-desktop-ios.md)         |
| macOS    | [iTunes ストアの macOS クライアント](https://itunes.apple.com/app/microsoft-remote-desktop/id1295203466?mt=12) | [Mac でリモート デスクトップ クライアントを使用する](remote-desktop-mac.md)         |

## <a name="configuring-the-remote-pc"></a>リモート PC の構成

リモートでアクセスする前にリモート PC を構成するには、[PC へのアクセスを許可します](remote-desktop-allow-access.md)。

## <a name="remote-desktop-client-uri-scheme"></a>リモート デスクトップ クライアントの URI スキーム

統一リソース識別子 (URI) スキームを有効にすると、プラットフォーム間でリモート デスクトップ クライアントの機能を統合できます。 チェック アウト、 [URI 属性をサポートされている](remote-desktop-uri.md) iOS、Mac、および Android クライアントで使用できます。
