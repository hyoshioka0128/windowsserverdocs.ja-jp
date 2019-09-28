---
title: 記憶域スペースの概要
ms.prod: windows-server
ms.author: jgerend
ms.manager: dougkim
ms.technology: storage-file-systems
ms.topic: article
author: jasongerend
ms.date: 05/22/2018
ms.openlocfilehash: 5de8b36916624b595d8f2ac9ddb0c000e015ee65
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366063"
---
# <a name="storage-spaces-overview"></a>記憶域スペースの概要

記憶域スペースは、Windows および Windows Server のテクノロジであり、ドライブの障害からデータを保護するのに役立ちます。 概念的には、ソフトウェアに実装されている RAID に似ています。 記憶域スペースを使用して、3台以上のドライブを1つの記憶域プールにグループ化し、そのプールの容量を使用して記憶域スペースを作成することができます。 これらは通常、データの余分なコピーを格納するので、いずれかのドライブで障害が発生した場合でも、データのコピーはそのまま保持されます。 容量が不足している場合は、記憶域プールにドライブを追加するだけです。

記憶域スペースを使用するには、主に次の4つの方法があります。

- **WINDOWS PC**の場合-詳細については、「 [Windows 10 の記憶域スペース](http://windows.microsoft.com/en-us/windows-10/storage-spaces-windows-10)」を参照してください。
- **単一サーバー内のすべての記憶域を持つスタンドアロンサーバー** -詳細については、「[スタンドアロンサーバーに記憶域スペースを展開する](deploy-standalone-storage-spaces.md)」を参照してください。
- **クラスター化されたサーバーで、各クラスターノードにローカルの直接接続ストレージと共に記憶域スペースダイレクトを使用**する-詳細については、「[記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)」を参照してください。
- **すべてのドライブを保持する1つ以上の共有 SAS 記憶域エンクロージャがあるクラスター化されたサーバー** -詳細については、「[共有 sas を使用したクラスターの記憶域スペースの概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831739(v%3dws.11))」を参照してください。

