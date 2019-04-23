---
title: Windows Server 半期チャネルで Nano Server に加えられる変更
description: 新しい Windows Server のサービス モデルでは、Nano Server がコンテナー オペレーティング システムのみとなり、いくつかの機能が変更されます。
ms.prod: Windows Server
ms.mktglfcycl: manage
ms.sitesec: library
author: jaimeo
ms.localizationpriority: medium
ms.date: 05/02/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: 7e68d292c32ce58c786a3242203330fcae985913
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847773"
---
# <a name="changes-to-nano-server-in-windows-server-semi-annual-channel"></a>Windows Server 半期チャネルで Nano Server に加えられる変更

>適用先:Windows Server 半期チャネル


「[Windows Server 半期チャネルの概要](semi-annual-channel-overview.md)」で説明されているように、Windows Server バージョン 1803 は、半期チャネルの最新リリースです。

このサービス モデルは以前に Current Branch for Business (CBB) モデルで提供されているため、Nano Server を実行しているお客様には既に使用されています。 Windows Server の新しい半期チャネルは、モデル名が新しくなりましたが、内容は同じです。 このモデルでは、Nano Server の機能更新リリースが年に 2 回～ 3 回公開される予定です。

ただし、Windows Server バージョン 1803 のこのリリース と Nano Server は、**コンテナーの基本 OS イメージ**としてのみ利用可能です。 このイメージは、Windows Server に含まれる Server Core インストールをはじめとするコンテナー ホスト内で、コンテナーとして実行する必要があります。 このリリースの Nano Server を使用して実行されるコンテナーは、これまでのリリースと次のような違いがあります。

- Nano Server は、.NET Core アプリケーションに最適化されています。
- Nano Server は、Windows Server 2016 バージョンよりもさらに小型です。
- PowerShell Core、.NET Core、および WMI は既定では含まれませんが、コンテナーの構築時に、[PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) コンテナーや [.NET Core](https://hub.docker.com/r/microsoft/dotnet/) コンテナーのパッケージに含めることができます。
- Nano Server にサービス スタックは含まれません。 マイクロソフトは、再展開する Docker Hub に対する更新済みの Nano コンテナーを公開します。
- 新しい Nano コンテナーのトラブルシューティングには、Docker を使います。
- Nano コンテナーが、IoT Core で実行できるようになりました。

## <a name="related-topics"></a>関連トピック
Insider Program の開始時に、[Windows コンテナーのドキュメント](http://aka.ms/windowscontainers)に詳細情報が提供されます。
