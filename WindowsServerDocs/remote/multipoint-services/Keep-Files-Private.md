---
title: ファイルをプライベートな状態で保持する
description: MultiPoint Services 内のユーザーから特定のファイルを保護する方法について説明します。
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 909049dc-6514-4040-89fb-fcf33fa96a9d
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: a2d8f0c869d6cc4c9235c54dec63e77767b6f9bb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853705"
---
# <a name="keep-files-private"></a>ファイルをプライベートな状態で保持する
このトピックの内容は、\(管理ユーザー*と*標準ユーザー\)が MultiPoint Services システム内の他のユーザーと共有しないコンテンツ (ドキュメントなど) に適用されます。  

MultiPoint Services のプライバシーの詳細については、「[プライバシーとセキュリティに関する考慮事項](Privacy-and-Security-Considerations.md)」を参照してください。
  
## <a name="to-keep-content-private-in-windows-explorer"></a>エクスプローラーにプライベートな状態でコンテンツを保持するには  
  
ドキュメントおよびその他のコンテンツをプライベートな状態で保持するには、エクスプローラーの **[ドキュメント]** ライブラリの **[マイ ドキュメント]** フォルダーに、作業したデータを保存する必要があります。 既定では、 **[マイ ドキュメント]** フォルダーはプライベート フォルダーです。 ただし、管理ユーザーはエクスプローラーのプライベート フォルダーにアクセスできます。  
  
> [!WARNING]  
> USB フラッシュ ドライブなどの外部の記憶装置が、ホストの USB ポートまたはステーション ハブ以外の USB ハブの USB ポートに接続されている間は、MultiPoint Services システムにログオンしているすべての標準ユーザーと管理ユーザーが、この記憶装置を参照できます。 外部の記憶装置に保存されるコンテンツについて、プライバシーまたはセキュリティ上の懸念がある場合は、MultiPoint Services システムのステーション ハブにのみ、その外部記憶装置を接続するようにします。 USB 記憶装置の使用方法については、「[USB フラッシュ ドライブでのファイルの保存と共有](Save-and-Share-Files-on-a-USB-Flash-Drive.md)」トピックを参照してください。  
  
## <a name="see-also"></a>参照  
[ユーザー ファイルの管理](Manage-User-Files.md)  
[USB フラッシュ ドライブにファイルを保存して共有する](Save-and-Share-Files-on-a-USB-Flash-Drive.md)