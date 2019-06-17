---
title: Windows Server 2016 向けのサーバーの役割のアップグレードと移行に関する一覧表
description: Windows Server 2016 にアップグレードまたは移行できるサーバーの役割について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 10/05/2016
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e031a64-b1e6-4cf6-994a-e7c575835f6a
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 9f8310baf659810d5d51587bafcc868c59ace61a
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "63687273"
---
# <a name="server-role-upgrade-and-migration-matrix-for-windows-server-2016"></a>Windows Server 2016 向けのサーバーの役割のアップグレードと移行に関する一覧表

>適用先:Windows Server 2016

このページの表には、サーバーの役割をアップグレードおよび移行するうえで、特に Windows Server 2016 への移行に適用できるオプションの説明が記載されています。 個々の役割の移行ガイドについては、「[Windows Server の役割と機能を移行する](https://docs.microsoft.com/windows-server/get-started/migrate-roles-and-features)」を参照してください。 インストールとアップグレードの詳細については、「[Windows Server Installation, Upgrade, and Migration (Windows Server のインストール、アップグレード、移行)](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade)」を参照してください。

|サーバーの役割|Windows Server 2012 R2 からアップグレードできるか?|Windows Server 2012 からアップグレードできるか?|移行はサポートされているか?|ダウンタイムなしで移行を完了できるか?|  
|-------------------|----------|--------------|--------------|----------|  
|Active Directory 証明書サービス| 〇|    〇|    〇|    X|
|Active Directory Domain Services|  〇|    〇|    〇|    〇|
|Active Directory フェデレーション サービス|  X| X| 〇|    いいえ (新しいノードをファームに追加する必要がある)|
|Active Directory ライトウェイト ディレクトリ サービス|   〇|    〇|    〇|    〇|
|Active Directory Rights Management サービス|   〇|    〇|    〇|    X|
|DHCP サーバー|   〇|    〇|    〇|    〇|
|DNS サーバー|    〇|    〇|    〇|    X|
|フェールオーバー クラスター|はい (ノードの一時停止、ドレイン、削除、Windows Server 2016 へのアップグレード、元のクラスターへの再参加を含む[クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) プロセスを使用)。 はい (アップグレードのためにサーバーがクラスターによって削除された後、別のクラスターに追加された場合)。|いいえ (サーバーがクラスターに属している場合)。 はい (アップグレードのためにサーバーがクラスターによって削除された後、別のクラスターに追加された場合)。  |〇|いいえ (Windows Server 2012 フェールオーバー クラスターの場合)。 はい (Hyper-V VM を備えた Windows Server 2012 R2 フェールオーバー クラスター、またはスケールアウト ファイル サーバーの役割を実行している Windows Server 2012 R2 フェールオーバー クラスターの場合)。 [クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)に関するページを参照。|
|ファイル サービスおよび記憶域サービス| 〇|    〇|    サブ機能によって異なる|  X|
|Hyper-V| [はい]。 (ホストがクラスターに属し、ノードの一時停止、ドレイン、削除、Windows Server 2016 へのアップグレード、元のクラスターへの再参加を含むクラスター OS のローリング アップグレード プロセスを使用している場合)。|  X|   〇|  いいえ (Windows Server 2012 フェールオーバー クラスターの場合)。 はい (Hyper-V VM を備えた Windows Server 2012 R2 フェールオーバー クラスター、またはスケールアウト ファイル サーバーの役割を実行している Windows Server 2012 R2 フェールオーバー クラスターの場合)。 [クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)に関するページを参照。| 
|印刷サービスと FAX サービス|    X| X| はい (Printbrm.exe)| X|
|リモート デスクトップ サービス|   はい (すべてのサブロールで可能。ただし、混在モードのファームはサポートされていない)|   はい (すべてのサブロールで可能。ただし、混在モードのファームはサポートされていない)|   〇|    X|
|Web サーバー (IIS)|  〇|    〇|    〇|    X|
|Windows Server Essentials Experience|  〇|    該当なし - 新機能|  〇|    X|
|Windows Server Update Services|    〇|    〇|    〇|    X|
|ワーク フォルダー|  〇|    〇|    〇|    はい ([クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)を使用した場合に WS 2012 R2 クラスターから)。|

