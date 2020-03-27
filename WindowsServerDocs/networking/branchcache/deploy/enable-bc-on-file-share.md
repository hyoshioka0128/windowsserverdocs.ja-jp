---
title: ファイル共有上の BranchCache を有効にする (省略可能)
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-bc
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9c465a9e-c504-44ec-9ebc-4e06ba54db30
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d2b98e7ccd3604de60bfabf865404506569f8c82
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319137"
---
# <a name="enable-branchcache-on-a-file-share-optional"></a>ファイル共有上の BranchCache を有効にする (省略可能)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次の手順を使用して、ファイル共有で BranchCache を有効にすることができます。  
  
> [!IMPORTANT]  
> [**すべての共有フォルダーにハッシュの発行を許可**する] の値を使用してハッシュの発行設定を構成する場合は、この手順を実行する必要はありません。  
  
メンバーシップ **管理者**, 、または同等がこの手順を実行するために必要な最小値。  
  
### <a name="to-enable-branchcache-on-a-file-share"></a>ファイル共有で BranchCache を有効にするには  
  
1.  Windows PowerShell を開き、「**mmc**」と入力して、Enter キーを押します。 Microsoft 管理コンソール (MMC) が開きます。  
  
2.  MMC の **[ファイル]** メニューで、 **[スナップインの追加と削除]** をクリックします。 **[スナップインの追加と削除]** ダイアログボックスが表示されます。  
  
3.  **[スナップインの追加と削除]** の **[使用できるスナップ]** イン で、 **[共有フォルダー]** をダブルクリックします。 [ローカルコンピューター] オブジェクトが選択された状態で、共有フォルダーウィザードが開きます。 必要に応じてビューを構成し、 **[完了]** をクリックして、 **[OK]** をクリックします。  
  
4.  **[共有フォルダー (ローカル)]** をダブルクリックし、 **[共有]** をクリックします。  
  
5.  詳細ウィンドウで、共有を右クリックし、 **[プロパティ]** をクリックします。 共有の **[プロパティ]** ダイアログボックスが表示されます。  
  
6.  **[プロパティ]** ダイアログボックスの **[全般]** タブで、 **[オフライン設定]** をクリックします。 **[オフライン設定]** ダイアログボックスが表示されます。  
  
7.  [**ユーザーが指定したファイルとプログラムのみをオフラインで使用できる**ようにする] が選択されていることを確認し、[ **BranchCache を有効に**する] をクリックします。  
  
8.  **[OK]** を 2 回クリックします。  
  

