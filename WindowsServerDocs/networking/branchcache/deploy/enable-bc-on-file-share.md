---
title: ファイル共有上の BranchCache を有効にする (省略可能)
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-bc
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9c465a9e-c504-44ec-9ebc-4e06ba54db30
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fd1757f6da011c2f774d8f97f628e5f0e87d3bf7
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284033"
---
# <a name="enable-branchcache-on-a-file-share-optional"></a>ファイル共有上の BranchCache を有効にする (省略可能)

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

ファイル共有の BranchCache を有効にするのには、この手順を使用することができます。  
  
> [!IMPORTANT]  
> 値は、ハッシュのパブリケーション設定を構成する場合は、この手順を実行する必要はありません**すべての共有フォルダーのハッシュの発行を許可する**します。  
  
メンバーシップ **管理者**, 、または同等がこの手順を実行するために必要な最小値。  
  
### <a name="to-enable-branchcache-on-a-file-share"></a>ファイル共有で BranchCache を有効にするには  
  
1.  Windows PowerShell を開き、「 **mmc**」と入力して、Enter キーを押します。 Microsoft 管理コンソール (MMC) が開きます。  
  
2.  MMC で、 **[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。 **スナップインを追加または** ダイアログ ボックスが表示されます。  
  
3.  **スナップインを追加または**で、**利用できるスナップイン**、ダブルクリックして**共有フォルダー**します。 ローカル コンピューター オブジェクトを選択したフォルダーの共有ウィザードが開きます。 必要に応じて、ビューの構成 をクリックして**完了**、順にクリックします**OK**。  
  
4.  ダブルクリック**共有フォルダー (ローカル)** 、 をクリックし、**共有**。  
  
5.  詳細ペインで、共有を右クリックし をクリックし、**プロパティ**します。 共有の**プロパティ** ダイアログ ボックスが表示されます。  
  
6.  **プロパティ**] ダイアログ ボックス [、**全般**] タブで [**オフライン設定**。 **オフライン設定** ダイアログ ボックスが表示されます。  
  
7.  いることを確認**ファイルとユーザーを指定するプログラムはオフライン利用が専用**が選択されているし、をクリックし、 **BranchCache を有効にする**します。  
  
8.  **[OK]** を 2 回クリックします。  
  

