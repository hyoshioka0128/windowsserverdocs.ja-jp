---
title: 手順 5:Windows Server Essentials の移行先サーバーの移行でフォルダー リダイレクトを有効にします。
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3925f80-552d-431f-b2a6-2af202e50ca4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 98b1a7adc23fca15c06ae9588d52bc9bcd532252
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432605"
---
# <a name="step-5-enable-folder-redirection-on-the-destination-server-for-windows-server-essentials-migration"></a>手順 5:Windows Server Essentials の移行先サーバーの移行でフォルダー リダイレクトを有効にします。

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

移行元サーバーでフォルダー リダイレクトが有効になっている場合は、移行先サーバーでフォルダー リダイレクトを有効にしてから、以前のフォルダー リダイレクト グループ ポリシー設定を削除できます。  
  
 最初に、Windows Server Essentials ダッシュ ボードを使用して、移行先サーバーでフォルダー リダイレクトを有効にします。 次に、古いフォルダー リダイレクト グループ ポリシーの設定を削除します。  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>移行先サーバーでフォルダー リダイレクトを有効にするには  
  
1.  移行先サーバーでは、Windows Server Essentials ダッシュ ボードを開きます。  
  
2.  ナビゲーション バーで、 **[デバイス]** をクリックします。  
  
3.  **[デバイスのタスク]** ウィンドウで、 **[グループ ポリシーの実装]** をクリックします。  
  
4.  **[フォルダー リダイレクト グループ ポリシーを有効にする]** ページで、リダイレクトするフォルダーを選択し、 **[次へ]** をクリックします。  
  
5.  **[セキュリティ ポリシー設定を有効にする]** ページで、 **[完了]** をクリックします。  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>古いフォルダー リダイレクト グループ ポリシーの設定を削除するには  
  
1. 移行先サーバーで、 **[グループ ポリシーの管理]** 管理ツールを開きます。  
  
2. **Group Policy Management**、展開**フォレスト:** <em>ネットワーク ドメイン名</em>、展開**ドメイン**、展開*ネットワーク ドメイン名*、順に展開**グループ ポリシー オブジェクト**します。  
  
3. 削除するポリシーを右クリックして、 **[削除]** をクリックします。  
  
4. 警告を読み、 **[はい]** をクリックします。  
  
5. **[グループ ポリシーの管理]** を閉じます。  
  
   フォルダー リダイレクトの変更を適用するには、ネットワーク ユーザーがそれぞれのコンピューターからログオフして、ログオンし直す必要があります。 これにより、リダイレクトされるすべてのフォルダーが移行先サーバーに転送されます。  
  
## <a name="next-steps"></a>次のステップ  
 移行先サーバーでフォルダー リダイレクトを有効にしました。 次に「[手順 6。降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)します。  
  

すべての手順を表示するを参照してください。 [Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

