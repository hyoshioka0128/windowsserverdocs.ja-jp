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
ms.openlocfilehash: 341262243b5bbe8ed046382d7490a6e5c39b8965
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188127"
---
# <a name="remote-desktop-clients"></a>リモート デスクトップ クライアント

>適用対象:Windows 10、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

Microsoft リモート デスクトップ クライアントを使用すると、リモート PC や仕事用リソースに接続できます。使用できるデバイスに制限はほとんどなく、場所もほぼどこからでも接続できます。 仕事用 PC に接続して、自分のデスクで作業しているときと同じように、すべてのアプリ、ファイル、ネットワーク リソースを利用できます。 RD クライアントを使用するだけで、職場でアプリを開いたままにしておいて、そのアプリを自宅で表示できます。

開始する前に、リモート デスクトップ クライアントを使って接続できる PC について説明している[サポートされている構成](remote-desktop-supported-config.md)の記事を確認してください。 [クライアント FAQ](remote-desktop-client-faq.md) も確認してください。

次のクライアント アプリを利用できます。

| デバイス   | アプリを入手する                                                                                                     | セットアップ手順                                                                |
|----------|-----------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| Windows  | [Microsoft Store での Windows 10 クライアント](https://go.microsoft.com/fwlink/?LinkID=616709)                      | [Windows 上のリモート デスクトップ クライアントの概要](windows.md)                |
| Android  | [Google Play の android クライアント](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)        | [Android でリモート デスクトップ クライアントの概要](remote-desktop-android.md) |
| iOS      | [iTunes store で iOS クライアント](https://itunes.apple.com/us/app/microsoft-remote-desktop/id714464092?mt=8)     | [IOS でリモート デスクトップ クライアントの概要](remote-desktop-ios.md)         |
| macOS    | [iTunes store での macOS のクライアント](https://itunes.apple.com/us/app/microsoft-remote-desktop/id1295203466?mt=12) | [Mac でリモート デスクトップ クライアントの概要](remote-desktop-mac.md)         |

## <a name="configuring-the-remote-pc"></a>リモート PC の構成

リモートでアクセスする前にリモート PC を構成するには、[PC へのアクセスを許可します](remote-desktop-allow-access.md)。

## <a name="remote-desktop-client-uri-scheme"></a>リモート デスクトップ クライアントの URI スキーム

統一リソース識別子 (URI) スキームを有効にすると、プラットフォーム間でリモート デスクトップ クライアントの機能を統合できます。 iOS、Mac、Android クライアントで使うことができる[サポートされている URI 属性](remote-desktop-uri.md)を確認してください。
