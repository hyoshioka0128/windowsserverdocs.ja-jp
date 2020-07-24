---
title: iSCSI ターゲット サーバーの概要
TOCTitle: iSCSI Target Server
ms.prod: windows-server
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 34515988c46b680701cc39b3948fcd53645741f4
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961354"
---
# <a name="iscsi-target-server-overview"></a>iSCSI ターゲットサーバーの概要

適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、iscsi プロトコルを使用して記憶域を使用できるようにする、Windows Server の役割サービスである iSCSI ターゲットサーバーの概要について簡単に説明します。 これは、ネイティブの Windows ファイル共有プロトコルである SMB を使用して通信できないクライアントのために、Windows server 上の記憶域へのアクセスを提供する場合に便利です。

iSCSI ターゲット サーバーは、以下の目的に最適です。

* **ネットワークとディスクなしのブート**    ブートに対応したネットワークアダプターまたはソフトウェアローダーを使用すると、数百台のディスクなしのサーバーを展開できます。 iSCSI ターゲット サーバーを使用すると、すばやい展開が可能です。 マイクロソフトの内部テストでは、256 台のコンピューターを 34 分で展開できました。 差分仮想ハード ディスクを使用すると、オペレーティング システム イメージ用に使用される記憶域スペースを最大 90% 節約できます。 これは、Hyper-V や高性能コンピューティング (HPC) クラスターを実行している仮想マシンのように、同じオペレーティング システム イメージを大規模に展開する場合に適しています。

* **サーバーアプリケーションの記憶域**    一部のアプリケーションでは、ブロック記憶域が必要です。 iSCSI ターゲット サーバーは、このようなアプリケーションに継続的に使用可能なブロック記憶域を提供できます。 記憶域にはリモートでアクセスできるため、本社または支部にあるブロック記憶域を統合することもできます。

* **異種ストレージ**    iSCSI ターゲットサーバーでは、Microsoft 以外の iSCSI イニシエーターがサポートされているため、ソフトウェア環境が混在しているサーバー上の記憶域を簡単に共有することができます。

* **開発、テスト、デモ、およびラボ環境**    ISCSI ターゲットサーバーを有効にすると、Windows Server オペレーティングシステムを実行しているコンピューターが、ネットワークからアクセス可能なブロック記憶装置になります。 これは、記憶域ネットワーク (SAN) に展開する前にアプリケーションをテストする場合に便利です。

## <a name="block-storage-requirements"></a>ブロック記憶域の要件

iSCSI ターゲット サーバーを有効にしてブロック記憶域を提供することで、既存のイーサネット ネットワークを活用できます。 ハードウェアを追加する必要はありません。 高可用性が重要な条件である場合は、高可用性クラスターをセットアップすることを検討してください。 高可用性クラスター用の共有記憶域 (ハードウェア ファイバー チャネル記憶域または Serial Attached SCSI (SAS) 記憶域アレイ) が必要になります。

ゲスト クラスタリングを有効にする場合は、ブロック記憶域を提供する必要があります。 iSCSI ターゲット サーバーを使用して Windows Server のソフトウェアを実行しているサーバーでは、ブロック記憶域を提供できます。

## <a name="see-also"></a>参照

[iSCSI ターゲット ブロック記憶域: 操作方法](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh848268(v%3dws.11))  
[Windows Server の iSCSI ターゲット サーバーの新機能](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn305893(v%3dws.11))
