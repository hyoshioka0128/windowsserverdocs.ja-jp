---
title: リモート デスクトップのリッスン ポートを変更する
description: リモート デスクトップ クライアントのリッスン ポートを変更する方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: b6b5a48435a99b1bf1392acb6a5764b106984bbe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404191"
---
# <a name="change-the-listening-port-for-remote-desktop-on-your-computer"></a>お使いのコンピューターでリモート デスクトップ用のリッスン ポートを変更する

>適用対象:Windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、Wndows Server 2012 R2、Windows Server 2008 R2

リモート デスクトップ クライアント経由でコンピューター (Windows クライアントまたは Windows Server) に接続すると、お使いのコンピューターのリモート デスクトップ機能が、定義されたリッスン ポート (既定では 3389) を介して接続要求を "聞きます"。 Windows コンピューター上のそのリッスン ポートは、レジストリを変更することで変更できます。

1. レジストリ エディターを起動します。 (検索ボックスに regedit と入力してください。)
2. 次のレジストリ サブキーに移動します。HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\PortNumber
3. **[編集] > [修正]** の順にクリックし、次に **[10 進数]** をクリックします。
4. 新しいポート番号を入力し、次に **[OK]** をクリックします。 
5. レジストリ エディターを閉じて、コンピューターを再起動します。

次回リモート デスクトップ接続を使用してこのコンピューターに接続したときには、新しいポートを入力する必要があります。 ファイアウォールを使用している場合は、必ず新しいポート番号への接続を許可するようにファイアウォールを構成してください。
