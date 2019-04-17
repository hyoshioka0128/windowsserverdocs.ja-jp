---
title: リモート デスクトップのリスニング ポートを変更します。
description: リモート デスクトップ クライアントのリスニング ポートを変更する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: b70479b644f4984c93136d6493483c372703244d
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297322"
---
# お使いのコンピューターでリモート デスクトップのリスニング ポートを変更します。

>適用対象: Windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2008 R2

リモート デスクトップ クライアントを使用して (Windows クライアントまたは Windows Server) コンピューターに接続すると、コンピューターでリモート デスクトップ機能「認識する」定義リスニング ポートを経由接続要求 (既定では 3389)。 レジストリを変更することによって、Windows コンピューターでリッスンするポートを変更できます。

1. レジストリ エディターを起動します。 (Regedit と検索ボックスに入力します。)
2. 次のレジストリ サブキーの下に移動します: Server\WinStations\RDP-Tcp\PortNumber のします。
3. **_Gt 変更の編集**] をクリックし、 **10 進**] をクリックします。
4. 新しいポート番号を入力し、 **[ok]** をクリックします。 
5. レジストリ エディターを終了し、コンピューターを再起動します。

次回のリモート デスクトップ接続を使用してこのコンピューターに接続する新しいポートを入力する必要があります。 ファイアウォールを使用している場合は、新しいポート番号に接続を許可するファイアウォールを構成することを確認してください。
