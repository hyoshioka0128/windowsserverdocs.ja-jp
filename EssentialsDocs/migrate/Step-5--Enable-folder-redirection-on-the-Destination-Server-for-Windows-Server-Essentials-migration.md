---
title: "手順 5: Windows Server Essentials の移行先サーバーの移行でフォルダー リダイレクトを有効にします。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: 613ff4c80a80ed4f3207cb0c1ead6db12c723e85
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="step-5-enable-folder-redirection-on-the-destination-server-for-windows-server-essentials-migration"></a>手順 5: Windows Server Essentials の移行先サーバーの移行でフォルダー リダイレクトを有効にします。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

移行元サーバーでフォルダー リダイレクトが有効である場合、移行先サーバーでフォルダー リダイレクトを有効にし、古いフォルダー リダイレクト グループ ポリシー設定を削除できます。  
  
 最初に、Windows Server Essentials ダッシュ ボードを使用して、移行先サーバーでフォルダー リダイレクトを有効にします。 その後、古いフォルダー リダイレクト グループ ポリシー設定を削除します。  
  
### <a name="to-enable-folder-redirection-on-the-destination-server"></a>移行先サーバーでフォルダー リダイレクトを有効にするには  
  
1.  移行先サーバーで、Windows Server Essentials ダッシュ ボードを開きます。  
  
2.  ナビゲーション バーで、クリックして**デバイス**します。  
  
3.  **デバイス タスク**] ウィンドウで、をクリックして**グループ ポリシーの実装**します。  
  
4.  **フォルダー リダイレクト グループ ポリシーを有効にする**] ページで、クリックして、リダイレクトするフォルダーを選択**次**します。  
  
5.  **セキュリティ ポリシー設定を有効にする**] ページで [**完了**します。  
  
### <a name="to-delete-the-old-folder-redirection-group-policy-setting"></a>古いフォルダー リダイレクト グループ ポリシー設定を削除するには  
  
1.  移行先サーバーで、開く、**グループ ポリシーの管理**管理ツールです。  
  
2.  **グループ ポリシーの管理**、展開**フォレスト:***ネットワーク ドメイン名*、展開**ドメイン**、展開*ネットワーク ドメイン名*、し、展開**グループ ポリシー オブジェクト**します。  
  
3.  削除、およびをクリックするポリシーを右クリックして**削除**します。  
  
4.  クリックして警告を読み、**はい**します。  
  
5.  閉じる**グループ ポリシー管理**します。  
  
 フォルダー リダイレクトの変更を適用するには、ネットワーク ユーザーは自分のコンピューターからログオフおよびログオンし直す必要があります。 これにより、すべてのリダイレクトされたフォルダーの移行先サーバーに転送されます。  
  
## <a name="next-steps"></a>次の手順  
 移行先サーバーでフォルダー リダイレクトを有効にします。 移動できるようになりました[手順 6: 降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除する](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)します。  
  

すべての手順を参照してください[Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

