---
title: MultiPoint Services でファイルを保存する
description: MultiPoint Services のファイルストレージについて
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: c9eb0461-3846-4ddc-97ff-de10f03f30cf
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 504389af62af8ec303e5b3baa2797a46f3ef52e6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853875"
---
# <a name="storing-files-with-multipoint-services"></a>MultiPoint Services でファイルを保存する
MultiPoint Services では、次の方法でユーザーファイルを格納できます。  
  
-   **ハードディスクドライブのオペレーティングシステムパーティション。** 既定では、MultiPoint Services はユーザーファイルをハードディスクドライブにオペレーティングシステムと共に保存します。  
  
-   **ハードディスクドライブの別のパーティション。** MultiPoint Services システムを初めてセットアップするときに、ハードディスクドライブを*パーティション分割*することができます。 つまり、ドライブのセクションを構成して、別のドライブとして機能するようにすることができます。 これにより、ユーザーファイルに影響を与えることなく、オペレーティングシステムの復元またはアップグレードが容易になります。 詳細については、Windows Server テクニカルライブラリの「[パーティションまたは論理ドライブを作成する](https://go.microsoft.com/fwlink/?LinkId=182618)」を参照してください。  
  
-   **追加の内蔵または外付けハードディスクドライブ。** データの保存とバックアップを行うために、追加の内部または外部のハードディスクドライブを MultiPoint Services に接続することができます。  
  
-   **共有ネットワークフォルダー内。** ユーザーファイルを任意のステーションから使用できるようにするには、ネットワーク上に共有フォルダーを作成します。 これには、MultiPoint Services を実行しているコンピューターに加えて、別のコンピューターまたはサーバーが必要です。 ファイルサーバーが使用可能な場合は、この方法を使用してファイルを保存することをお勧めします。  
  
    ファイルサーバーを使用しない MultiPoint Services を実行している2-3 コンピューターの小規模なコンピューターでは、MultiPoint Services コンピューターの1つを、multipoint services のすべてのコンピューターのファイルサーバーとして機能させることができます。 次に、ファイルサーバーとして機能する MultiPoint Services のすべてのユーザーのユーザーアカウントを作成します。  
  
