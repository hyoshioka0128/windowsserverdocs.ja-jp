---
title: リモート デスクトップのリッスン ポートを変更する
description: リモート デスクトップ クライアントのリッスン ポートを変更する方法について説明します。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 818ae5217d0144b2a4ec6e45f3a7757455cfabf1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854665"
---
# <a name="change-the-listening-port-for-remote-desktop-on-your-computer"></a>お使いのコンピューターでリモート デスクトップ用のリッスン ポートを変更する

>適用先:Windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、Wndows Server 2012 R2、Windows Server 2008 R2

リモート デスクトップ クライアント経由でコンピューター (Windows クライアントまたは Windows Server) に接続すると、お使いのコンピューターのリモート デスクトップ機能が、定義されたリッスン ポート (既定では 3389) を介して接続要求を "聞きます"。 Windows コンピューター上のそのリッスン ポートは、レジストリを変更することで変更できます。

1. レジストリ エディターを起動します。 (検索ボックスに regedit と入力してください。)
2. 次のレジストリ サブキーに移動します。HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\PortNumber
3. **[編集] > [修正]** の順にクリックし、次に **[10 進数]** をクリックします。
4. 新しいポート番号を入力し、次に **[OK]** をクリックします。 
5. レジストリ エディターを閉じて、コンピューターを再起動します。

次回リモート デスクトップ接続を使用してこのコンピューターに接続したときには、新しいポートを入力する必要があります。 ファイアウォールを使用している場合は、必ず新しいポート番号への接続を許可するようにファイアウォールを構成してください。
