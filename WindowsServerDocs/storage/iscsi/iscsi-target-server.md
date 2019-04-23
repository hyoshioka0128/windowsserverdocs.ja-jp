---
title: iSCSI Target Server Overview
TOCTitle: iSCSI Target Server
ms.prod: windows-server-threshold
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 14dd373b71c1be2f1a4ff157b9c631530532fc80
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837943"
---
# <a name="iscsi-target-server-overview"></a>iSCSI ターゲット サーバーの概要

適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、iSCSI ターゲット サーバー、記憶域を iSCSI プロトコル経由で使用できるようにすることができる Windows Server の役割サービスの概要を説明します。 これは、ネイティブの Windows ファイル共有プロトコル、SMB 経由で通信できないクライアントの Windows サーバー上のストレージへのアクセスを提供するために役立ちます。

iSCSI ターゲット サーバーは、以下の目的に最適です。

* **ネットワークおよびディスクなしのブート**   ブートに対応したネットワーク アダプターまたはソフトウェア ローダーを使用すると、数百のディスクなしのサーバーを展開することができます。 iSCSI ターゲット サーバーを使用すると、すばやい展開が可能です。 マイクロソフトの内部テストでは、256 台のコンピューターを 34 分で展開できました。 差分仮想ハード ディスクを使用すると、オペレーティング システム イメージ用に使用される記憶域スペースを最大 90% 節約できます。 これは、Hyper-V や高性能コンピューティング (HPC) クラスターを実行している仮想マシンのように、同じオペレーティング システム イメージを大規模に展開する場合に適しています。

* **サーバー アプリケーション記憶域**   一部のアプリケーションは、ブロック記憶域を必要とします。 iSCSI ターゲット サーバーは、このようなアプリケーションに継続的に使用可能なブロック記憶域を提供できます。 記憶域にはリモートでアクセスできるため、本社または支部にあるブロック記憶域を統合することもできます。

* **異種記憶域**   iSCSI ターゲット サーバーは、Microsoft 以外の iSCSI イニシエーターを簡単にソフトウェアの混在環境でのサーバー上の記憶域を共有することをサポートしています。

* **開発、テスト、デモ、およびラボ環境**   iSCSI ターゲット サーバーが有効にすると、Windows Server オペレーティング システムを実行しているコンピューターがネットワークからアクセス可能なブロック記憶装置になります。 これは、記憶域ネットワーク (SAN) に展開する前にアプリケーションをテストする場合に便利です。

## <a name="block-storage-requirements"></a>ブロック記憶域の要件

iSCSI ターゲット サーバーを有効にしてブロック記憶域を提供することで、既存のイーサネット ネットワークを活用できます。 ハードウェアを追加する必要はありません。 高可用性が重要な条件である場合は、高可用性クラスターをセットアップすることを検討してください。 高可用性クラスター用の共有記憶域 (ハードウェア ファイバー チャネル記憶域または Serial Attached SCSI (SAS) 記憶域アレイ) が必要になります。

ゲスト クラスタリングを有効にする場合は、ブロック記憶域を提供する必要があります。 iSCSI ターゲット サーバーを使用して Windows Server のソフトウェアを実行しているサーバーでは、ブロック記憶域を提供できます。

## <a name="see-also"></a>関連項目

[iSCSI ターゲット ブロック記憶域にする方法](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh848268(v%3dws.11))  
[ISCSI ターゲット サーバーの Windows Server の新します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn305893(v%3dws.11))

