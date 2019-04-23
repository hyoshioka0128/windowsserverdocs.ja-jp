---
title: 記憶域スペースの概要
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dougkim
ms.technology: storage-file-systems
ms.topic: article
author: jasongerend
ms.date: 05/22/2018
ms.openlocfilehash: 9977bb35be3676e31cdcab7322b5b5a2cfc67609
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832913"
---
# <a name="storage-spaces-overview"></a>記憶域スペースの概要

記憶域スペースは、Windows および Windows Server ドライブの障害からデータを保護できるようにするテクノロジです。 ソフトウェアで実装された RAID に概念的に似ています。 記憶域スペースを使用して、記憶域プールに 3 つまたは複数のドライブをグループ化し、そのプールから容量を使用して、記憶域スペースを作成することができます。 通常、データの余分なコピーを格納も、データの完全な状態のコピーがあるドライブのいずれかが失敗した場合は、ようにします。 容量の不足を実行する場合、記憶域プールにドライブを追加します。

記憶域スペースを使用する 4 つの主要な方法はあります。

- **Windows PC で**- 詳細についてを参照してください[Windows 10 での記憶域スペース](http://windows.microsoft.com/en-us/windows-10/storage-spaces-windows-10)します。
- **1 つのサーバーのすべての記憶域のスタンドアロン サーバーで**- 詳細についてを参照してください[スタンドアロン サーバー上の記憶域スペースの展開](deploy-standalone-storage-spaces.md)します。
- **各クラスター ノードでローカルの直接接続された記憶域と記憶域スペース ダイレクトを使用してクラスター化されたサーバーで**- 詳細についてを参照してください[記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)します。
- **クラスター化された 1 つまたは複数共有 SAS 記憶域エンクロージャのすべてのドライブを保持しているサーバーに**- 詳細についてを参照してください[共有 SAS の概要を使用するクラスターに記憶域スペース](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831739(v%3dws.11))します。

