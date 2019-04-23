---
title: ファイルをプライベートな状態で保持する
description: MultiPoint Services 内のユーザーから特定のファイルを保護する方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 909049dc-6514-4040-89fb-fcf33fa96a9d
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: f254b07c1f6f8ffdc83a1fe506bee7e6d5aa89ce
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879653"
---
# <a name="keep-files-private"></a>ファイルをプライベートな状態で保持する
このトピックでは、ドキュメントなどのコンテンツに適用した\(として、*管理ユーザー* \)と*標準ユーザー* MultiPoint Services では、他のユーザーと共有したくないです。システム。  

MultiPoint Services のプライバシーの詳細については、「[プライバシーとセキュリティに関する考慮事項](Privacy-and-Security-Considerations.md)」を参照してください。
  
## <a name="to-keep-content-private-in-windows-explorer"></a>エクスプローラーにプライベートな状態でコンテンツを保持するには  
  
ドキュメントおよびその他のコンテンツをプライベートな状態で保持するには、エクスプローラーの **[ドキュメント]** ライブラリの **[マイ ドキュメント]** フォルダーに、作業したデータを保存する必要があります。 既定では、**[マイ ドキュメント]** フォルダーはプライベート フォルダーです。 ただし、管理ユーザーはエクスプローラーのプライベート フォルダーにアクセスできます。  
  
> [!WARNING]  
> USB フラッシュ ドライブなどの外部の記憶装置が、ホストの USB ポートまたはステーション ハブ以外の USB ハブの USB ポートに接続されている間は、MultiPoint Services システムにログオンしているすべての標準ユーザーと管理ユーザーが、この記憶装置を参照できます。 外部の記憶装置に保存されるコンテンツについて、プライバシーまたはセキュリティ上の懸念がある場合は、MultiPoint Services システムのステーション ハブにのみ、その外部記憶装置を接続するようにします。 USB 記憶装置の使用方法については、「[USB フラッシュ ドライブでのファイルの保存と共有](Save-and-Share-Files-on-a-USB-Flash-Drive.md)」トピックを参照してください。  
  
## <a name="see-also"></a>関連項目  
[ユーザー ファイルを管理します。](Manage-User-Files.md)  
[保存し、USB フラッシュ ドライブ上のファイルの共有](Save-and-Share-Files-on-a-USB-Flash-Drive.md)