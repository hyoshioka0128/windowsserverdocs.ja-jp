---
title: MultiPoint Services でファイルを保存する
description: MultiPoint Services のファイルストレージについて
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9eb0461-3846-4ddc-97ff-de10f03f30cf
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: bf31f5c582cffb5b38cff8cb15fcfdb4b3f76386
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389300"
---
# <a name="storing-files-with-multipoint-services"></a>MultiPoint Services でファイルを保存する
MultiPoint Services では、次の方法でユーザーファイルを格納できます。  
  
-   **ハードディスクドライブのオペレーティングシステムパーティション。** 既定では、MultiPoint Services はユーザーファイルをハードディスクドライブにオペレーティングシステムと共に保存します。  
  
-   **ハードディスクドライブの別のパーティション。** MultiPoint Services システムを初めてセットアップするときに、ハードディスクドライブを*パーティション分割*することができます。 つまり、ドライブのセクションを構成して、別のドライブとして機能するようにすることができます。 これにより、ユーザーファイルに影響を与えることなく、オペレーティングシステムの復元またはアップグレードが容易になります。 詳細については、Windows Server テクニカルライブラリの「[パーティションまたは論理ドライブを作成する](https://go.microsoft.com/fwlink/?LinkId=182618)」を参照してください。  
  
-   **追加の内蔵または外付けハードディスクドライブ。** データの保存とバックアップを行うために、追加の内部または外部のハードディスクドライブを MultiPoint Services に接続することができます。  
  
-   **共有ネットワークフォルダー内。** ユーザーファイルを任意のステーションから使用できるようにするには、ネットワーク上に共有フォルダーを作成します。 これには、MultiPoint Services を実行しているコンピューターに加えて、別のコンピューターまたはサーバーが必要です。 ファイルサーバーが使用可能な場合は、この方法を使用してファイルを保存することをお勧めします。  
  
    ファイルサーバーを使用しない MultiPoint Services を実行している2-3 コンピューターの小規模なコンピューターでは、MultiPoint Services コンピューターの1つを、multipoint services のすべてのコンピューターのファイルサーバーとして機能させることができます。 次に、ファイルサーバーとして機能する MultiPoint Services のすべてのユーザーのユーザーアカウントを作成します。  
  
