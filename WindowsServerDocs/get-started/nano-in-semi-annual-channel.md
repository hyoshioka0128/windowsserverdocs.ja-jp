---
title: Windows Server 半期チャネルで Nano Server に加えられる変更
description: 新しい Windows Server のサービス モデルでは、Nano Server がコンテナー オペレーティング システムのみとなり、いくつかの機能が変更されます。
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 05/21/2019
ms.topic: get-started-article
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: 0ede3b13c1180b5cf8031738d69b68abd9e4c631
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826135"
---
# <a name="changes-to-nano-server-in-windows-server-semi-annual-channel"></a>Windows Server 半期チャネルで Nano Server に加えられる変更

>適用先:Windows Server 半期チャネル

[Window Server 半期チャネル](../get-started-19/servicing-channels-19.md) サービス モデルは以前に Current Branch for Business (CBB) モデルで提供されているため、Nano Server を実行しているお客様には既に使用されています。 Windows Server 半期チャネルは、モデル名が新しくなりましたが、内容は同じです。 このモデルでは、Nano Server の機能更新のリリースが年に 2 回～ 3 回発生すると予想されます。

ただし、Windows Server バージョン 1803 以降、Nano Server は、**コンテナーの基本 OS イメージ**としてのみ利用可能です。 このイメージは、Windows Server に含まれる Server Core インストールをはじめとするコンテナー ホスト内で、コンテナーとして実行する必要があります。 このリリースの Nano Server を使用して実行されるコンテナーは、これまでのリリースと比べ次のような違いがあります。

- Nano Server は、.NET Core アプリケーションに最適化されています。
- Nano Server は、Windows Server 2016 バージョンよりもさらに小型です。
- PowerShell Core、.NET Core、および WMI は既定では含まれませんが、コンテナーの構築時に、[PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) コンテナーや [.NET Core](https://hub.docker.com/r/microsoft/dotnet/) コンテナーのパッケージに含めることができます。
- Nano Server にサービス スタックは含まれなくなりました。 Microsoft は、再展開する Docker Hub に対する更新済みの Nano コンテナーを公開しています。
- 新しい Nano コンテナーのトラブルシューティングには、Docker を使います。
- Nano コンテナーが、IoT Core で実行できるようになりました。

## <a name="related-topics"></a>関連トピック

- [Windows コンテナーに関するドキュメント](https://aka.ms/windowscontainers)
- [Windows Server の半期チャネルの概要](../get-started-19/servicing-channels-19.md)
