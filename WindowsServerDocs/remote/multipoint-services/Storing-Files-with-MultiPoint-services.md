---
title: MultiPoint Services でファイルを保存する
description: MultiPoint Services で file storage についてください。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9eb0461-3846-4ddc-97ff-de10f03f30cf
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: b432ca793b156997761f9fadab7340c394e3b553
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817343"
---
# <a name="storing-files-with-multipoint-services"></a>MultiPoint Services でファイルを保存する
MultiPoint Services では、次の方法でユーザーのファイルの格納をサポートしています。  
  
-   **ハード ディスク ドライブのオペレーティング システム パーティション。** 既定では、MultiPoint サービスは、オペレーティング システムとハード ディスク ドライブ上のユーザー ファイルを格納します。  
  
-   **別のハード ディスク ドライブのパーティション。** ときに、MultiPoint Services システムは、最初に設定する、*パーティション*ハード ディスク ドライブ。 つまり、別のドライブの場合と同様に機能するように、ドライブのセクションを構成できます。 これにより、簡単に復元またはユーザー ファイルの影響を与えずに、オペレーティング システムをアップグレードします。 詳細については、次を参照してください。[パーティションまたは論理ドライブを作成](https://go.microsoft.com/fwlink/?LinkId=182618)、Windows Server テクニカル ライブラリにします。  
  
-   **内部または外部ハード ディスク ドライブ。** MultiPoint Services を保存およびデータをバックアップするには、その他の内部または外部ハード ディスク ドライブをアタッチできます。  
  
-   **共有ネットワーク フォルダー。** あらゆるステーションからユーザー ファイルを使用できるようにするには、ネットワーク上の共有フォルダーを作成できます。 これは、別のコンピューターまたは MultiPoint Services を実行しているコンピューターだけでなく、サーバーが必要です。 これは、ファイル サーバーがある使用可能な場合は、ファイルを格納するための推奨される方法です。  
  
    使用可能なファイル サーバーのない MultiPoint Services を実行している 2 ~ 3 のコンピューターの小規模なシステムでは、MultiPoint Services コンピューターのすべてのファイル サーバーとして機能 MultiPoint Services コンピューターの 1 つ。 ファイル サーバーとして動作している MultiPoint Services のすべてのユーザーのユーザー アカウントを作成します。  
  
