---
title: リモート デスクトップのリッスン ポートを変更します。
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
ms.openlocfilehash: 5bf90010143e742f7a0c9b5c262be01e6ccf8c5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882723"
---
# <a name="change-the-listening-port-for-remote-desktop-on-your-computer"></a>コンピューターにリモート デスクトップのリッスン ポートを変更します。

>適用対象:Windows 10、Windows 8.1、Windows 8、Windows Server 2016、Windows Server 2012 R2、Windows Server 2008 R2

コンピューターにリモート デスクトップ機能が定義されているリッスン ポート経由の接続要求を「が」して、リモート デスクトップ クライアント経由でコンピューター (Windows クライアントまたは Windows Server) に接続するときに (既定では 3389)。 Windows コンピューター上でリッスンしているそのポートを変更するには、レジストリを変更します。

1. レジストリ エディターを起動します。 (検索ボックスに「regedit」を入力)。
2. 次のレジストリ サブキーに移動します。HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\PortNumber
3. クリックして**編集 > 変更**、順にクリックします**Decimal**します。
4. 新しいポート番号を入力し、クリックして**OK**します。 
5. レジストリ エディタを終了し、コンピューターを再起動します。

次回リモート デスクトップ接続を使用してこのコンピューターに接続する新しいポートを入力する必要があります。 ファイアウォールを使用している場合は、新しいポート番号への接続を許可するようにファイアウォールを構成することを確認してください。
