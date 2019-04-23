---
title: HYPER-V で標準または実稼働のチェックポイント間での選択します。
description: 標準または実稼働のチェックポイントを使用する仮想マシンを構成する方法についてを説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92bb573b-03b7-470e-b72e-e35edf52b349
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 239cce3c9f1acb2d45935e0f60fb1875b004485b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880953"
---
# <a name="choose-between-standard-or-production-checkpoints-in-hyper-v"></a>HYPER-V で標準または実稼働のチェックポイント間での選択します。

>適用先:Windows 10、Windows Server 2016、Microsoft HYPER-V Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019

  
Windows Server 2016 および Windows 10 以降、各仮想マシンの standard、および実稼働のチェックポイント間で選択できます。 運用チェックポイントは、新しい仮想マシンの既定値です。
  
- 運用チェックポイントは、すべての実稼働ワークロードを完全にサポートされている方法で後で復元可能な仮想マシンの「特定の時点」のイメージです。 これは、保存された状態を利用する代わりに、ゲスト内のバックアップ技術を利用してチェックポイントを作成することで行います。  
  
- 標準のチェックポイントでは、実行中の仮想マシンの状態、データ、およびハードウェア構成をキャプチャし、開発およびテストのシナリオでの使用を意図しています。 標準のチェックポイントは、問題のトラブルシューティングを行うことができるように、特定の状態または実行中の仮想マシンの状態を再作成する必要がある場合に役立ちます。  
 
 ## <a name="change-checkpoints-to-production-or-standard-checkpoints"></a>運用環境または標準チェックポイントにチェックポイントを変更します。  
  
1.  **、HYPER-V Manager**、仮想マシンを右クリックして**設定**します。  
  
2.  で、**管理**セクションで、**チェックポイント**します。  
  
3.  運用チェックポイントまたは標準チェックポイントのいずれかを選択します。  
  
    実稼働のチェックポイントを選択した場合は、実稼働のチェックポイントを取得できない場合に、ホストが標準チェックポイントを取得するかどうかも指定できます。 このチェック ボックスをオフにする、実稼働のチェックポイントを取得できない場合は、チェックポイントは取得されません。  
  
4.  チェックポイントの構成ファイルを別の場所に保管する場合を変更することで、**チェックポイント ファイルの場所**セクション。  
  
5.  クリックして**適用**変更を保存します。 完了したら、クリックして**OK**ダイアログ ボックスを閉じます。  
  
> [!NOTE]
> のみ**運用チェックポイント**Active Directory Domain Services の役割 (ドメイン コント ローラー) または Active Directory ライトウェイト ディレクトリ サービスの役割を実行しているゲストでサポートされます。

## <a name="see-also"></a>関連項目  
  
-   [実稼働のチェックポイント](../What-s-new-in-Hyper-V-on-Windows.md#BKMK_check)  
  
-   [有効にするか、チェックポイントを無効にします。](Enable-or-disable-checkpoints-in-Hyper-V.md)  
  


