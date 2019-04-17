---
title: (省略可能) ファイル共有の BranchCache を有効にします。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-bc
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9c465a9e-c504-44ec-9ebc-4e06ba54db30
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33ed40ef91d9389bb7940dcf928cba43f0c9dbd2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="enable-branchcache-on-a-file-share-optional"></a>(省略可能) ファイル共有の BranchCache を有効にします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ファイル共有で BranchCache を有効にするのには、この手順を使用することができます。  
  
> [!IMPORTANT]  
> 値を持つハッシュの発行設定を構成する場合は、この手順を実行する必要はありません**すべての共有フォルダーのハッシュの発行を許可する**します。  
  
メンバーシップ**管理者**、またはそれと同等がこの手順を実行するために必要な最小値。  
  
### <a name="to-enable-branchcache-on-a-file-share"></a>ファイル共有で BranchCache を有効にするには  
  
1.  Windows PowerShell を開き、「**mmc**、し、Enter キーを押します。 Microsoft 管理コンソール (MMC) を開きます。  
  
2.  MMC で、上、**ファイル**] メニューのをクリックして**スナップインの追加/削除**します。 **スナップインを追加または**] ダイアログ ボックスが開きます。  
  
3.  **スナップインを追加または**で、**利用できるスナップイン**、] をダブルクリック**共有フォルダー**します。 ローカル コンピューター オブジェクトを選択したフォルダーの共有ウィザードが開きます。 必要に応じて、ビューの構成] をクリックして**完了**、] をクリックし、**[OK]**します。  
  
4.  ダブルクリック**共有フォルダー (ローカル)**、] をクリックし、**共有**します。  
  
5.  詳細ウィンドウで、共有を右クリックし、をクリックして**プロパティ**します。 共有の**プロパティ**] ダイアログ ボックスが開きます。  
  
6.  **プロパティ**] ダイアログ ボックスで、**全般的な**] タブで、をクリックして**オフライン設定**します。 **オフライン設定**] ダイアログ ボックスが開きます。  
  
7.  いることを確認**だけで、ファイルとユーザーを指定するプログラムはオフラインで利用**をクリックして選択して**BranchCache を有効にする**します。  
  
8.  をクリックして**OK** 2 回クリックします。  
  

