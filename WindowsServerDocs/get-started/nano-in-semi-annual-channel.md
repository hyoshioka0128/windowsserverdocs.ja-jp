---
title: Windows Server 半期チャネルで Nano Server に加えられる変更
description: 新しい Windows Server のサービス モデルでは、Nano Server がコンテナー オペレーティング システムのみとなり、いくつかの機能が変更されます。
ms.prod: Windows Server
ms.mktglfcycl: manage
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 05/21/2019
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: c9fede02b90e285803a8bcdbc983f264d65a4589
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976512"
---
# <a name="changes-to-nano-server-in-windows-server-semi-annual-channel"></a>Windows Server 半期チャネルで Nano Server に加えられる変更

>適用先:Windows Server 半期チャネル

Nano Server を既に実行している場合、[ウィンドウ Server 半期チャネル](..\get-started-19\servicing-channels-19.md)サービス モデルはなじみのある、Current Branch for Business (CBB) モデルで処理されることが以前から。 Windows Server 半期チャネルでは、同じモデルに対して新しい名です。 このモデルでは、Nano Server の機能更新リリースが年に 2 回～ 3 回公開される予定です。

ただし、以降で Windows Server、バージョン 1803、Nano Server としてのみ使用可能な**コンテナー ベース OS イメージ**します。 このイメージは、Windows Server に含まれる Server Core インストールをはじめとするコンテナー ホスト内で、コンテナーとして実行する必要があります。 このリリースの Nano Server を使用して実行されるコンテナーは、これまでのリリースと次のような違いがあります。

- Nano Server は、.NET Core アプリケーションに最適化されています。
- Nano Server は、Windows Server 2016 バージョンよりもさらに小型です。
- PowerShell Core、.NET Core、および WMI は既定では含まれませんが、コンテナーの構築時に、[PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) コンテナーや [.NET Core](https://hub.docker.com/r/microsoft/dotnet/) コンテナーのパッケージに含めることができます。
- Nano Server にサービス スタックは含まれません。 マイクロソフトは、再展開する Docker Hub に対する更新済みの Nano コンテナーを公開します。
- 新しい Nano コンテナーのトラブルシューティングには、Docker を使います。
- Nano コンテナーが、IoT Core で実行できるようになりました。

## <a name="related-topics"></a>関連トピック

- [Windows コンテナーのドキュメント](http://aka.ms/windowscontainers)
- [ウィンドウのサーバーの場合は半期チャネルの概要](..\get-started-19\servicing-channels-19.md)
