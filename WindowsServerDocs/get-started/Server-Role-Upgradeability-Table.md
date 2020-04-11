---
title: Windows Server 2016 向けのサーバーの役割のアップグレードと移行に関する一覧表
description: Windows Server 2016 にアップグレードまたは移行できるサーバーの役割について説明します。
ms.prod: windows-server
ms.date: 10/05/2016
ms.technology: server-general
ms.topic: article
ms.assetid: 7e031a64-b1e6-4cf6-994a-e7c575835f6a
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 4e1b783c43eb435e61c7caaccaf842a0137b5eec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826525"
---
# <a name="server-role-upgrade-and-migration-matrix-for-windows-server-2016"></a>Windows Server 2016 向けのサーバーの役割のアップグレードと移行に関する一覧表

>適用先:Windows Server 2016

このページの表には、サーバーの役割をアップグレードおよび移行するうえで、特に Windows Server 2016 への移行に適用できるオプションの説明が記載されています。 個々の役割の移行ガイドについては、「[Windows Server の役割と機能を移行する](https://docs.microsoft.com/windows-server/get-started/migrate-roles-and-features)」を参照してください。 インストールとアップグレードの詳細については、「[Windows Server Installation, Upgrade, and Migration (Windows Server のインストール、アップグレード、移行)](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade)」を参照してください。

|サーバーの役割|Windows Server 2012 R2 からアップグレードできるか?|Windows Server 2012 からアップグレードできるか?|移行はサポートされているか?|ダウンタイムなしで移行を完了できるか?|  
|-------------------|----------|--------------|--------------|----------|  
|Active Directory 証明書サービス|    はい|    はい|    はい|    いいえ|
|[Active Directory Domain Services]|    はい|    はい|    はい|    はい|
|Active Directory フェデレーション サービス|    いいえ|    いいえ|    はい|    いいえ (新しいノードをファームに追加する必要がある)|
|Active Directory ライトウェイト ディレクトリ サービス|    はい|    はい|    はい|    はい|
|Active Directory Rights Management サービス|    はい|    はい|    はい|    いいえ|
|DHCP サーバー|    はい|    はい|    はい|    はい|
|DNS サーバー|    はい|    はい|    はい|    いいえ|
|フェールオーバー クラスター|はい (ノードの一時停止、ドレイン、削除、Windows Server 2016 へのアップグレード、元のクラスターへの再参加を含む[クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) プロセスを使用)。 はい (アップグレードのためにサーバーがクラスターによって削除された後、別のクラスターに追加された場合)。|いいえ (サーバーがクラスターに属している場合)。 はい (アップグレードのためにサーバーがクラスターによって削除された後、別のクラスターに追加された場合)。    |はい|いいえ (Windows Server 2012 フェールオーバー クラスターの場合)。 はい (Hyper-V VM を備えた Windows Server 2012 R2 フェールオーバー クラスター、またはスケールアウト ファイル サーバーの役割を実行している Windows Server 2012 R2 フェールオーバー クラスターの場合)。 [クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)に関するページを参照。|
|ファイル サービスおよび記憶域サービス|    はい|    はい|    サブ機能によって異なる|    いいえ|
|Hyper-V| はい。 (ホストがクラスターに属し、ノードの一時停止、ドレイン、削除、Windows Server 2016 へのアップグレード、元のクラスターへの再参加を含むクラスター OS のローリング アップグレード プロセスを使用している場合)。|  いいえ|   はい|  いいえ (Windows Server 2012 フェールオーバー クラスターの場合)。 はい (Hyper-V VM を備えた Windows Server 2012 R2 フェールオーバー クラスター、またはスケールアウト ファイル サーバーの役割を実行している Windows Server 2012 R2 フェールオーバー クラスターの場合)。 [クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)に関するページを参照。| 
|印刷サービスと FAX サービス|    いいえ|    いいえ|    はい (Printbrm.exe)|    いいえ|
|リモート デスクトップ サービス|    はい (すべてのサブロールで可能。ただし、混在モードのファームはサポートされていない)|    はい (すべてのサブロールで可能。ただし、混在モードのファームはサポートされていない)|    はい|    いいえ|
|Web サーバー (IIS)|    はい|    はい|    はい|    いいえ|
|Windows Server Essentials Experience|    はい|    該当なし - 新機能|    はい|    いいえ|
|Windows Server Update Services|    はい|    はい|    はい|    いいえ|
|作業フォルダー|    はい|    はい|    はい|    はい ([クラスター OS のローリング アップグレード](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)を使用した場合に WS 2012 R2 クラスターから)。|

