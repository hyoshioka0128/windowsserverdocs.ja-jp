---
title: "AD フォレストの回復 - 削除された dc のメタデータをクリーンアップします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e7543381-4081-407f-adad-a9de792c6616
ms.technology: identity-adfs
ms.openlocfilehash: 3027c59b58801b44d20127e6bcf62dd7319708bd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---cleaning-metadata-of-removed-writable-domain-controllers"></a>AD フォレストの回復 - 削除された書き込み可能ドメイン コント ローラーのメタデータをクリーンアップします。 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:
 
 メタデータのクリーンアップは、レプリケーション システムに DC を識別する Active Directory データを削除します。  
  
 AD DS を再インストールしてネットワークに追加するのに予定の Dc の DC オブジェクトを削除するのにには、次の手順を使用します。  
  
 Active Directory ユーザーとコンピューターのバージョンを使用している場合、または Active Directory サイトとサービスにリモート サーバー管理ツール (RSAT) が含まれている DC オブジェクトを削除するときにメタデータのクリーンアップが自動的に実行するが。  
  

## <a name="deleting-a-domain-controller-using-active-directory-users-and-computers"></a>Active Directory ユーザーとコンピューターを使用してドメイン コント ローラーを削除します。  
 Active Directory ユーザーとコンピューター、または Active Directory 管理センター リモート サーバー管理ツール (RSAT) のバージョンを使用するとメタデータのクリーンアップが自動的に実行 DC オブジェクトを削除するとします。 サーバー オブジェクトとコンピューター オブジェクトから自動的に削除されます。  
  
 代わりも使う Active Directory サイトとサービス RSAT で DC オブジェクトを削除します。 Active Directory サイトとサービスを使用する場合、DC オブジェクトを削除する前に、関連するサーバー オブジェクトと、NTDS 設定オブジェクトを削除する必要があります。  
  
 RSAT をダウンロードします。  

-   [Windows 10 用のリモート サーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=45520)
  
-   [Windows 8 用のリモート サーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=28972)  

-   [Windows 7 Service pack 1 (SP1) 用のリモート サーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=7887)  
  
-   [Windows Vista 用 Microsoft リモート サーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=21090)  
  
 次の手順では、Windows Server 2016、2012、2008 R2、または 2008 が実行されている Dc の同じです。 ターゲット DC のメタデータのクリーンアップ操作は、任意のバージョンの Windows Server を実行できます。  
  
### <a name="to-delete-a-domain-controller-object-using-active-directory-users-and-computers-in-rsat"></a>RSAT で Active Directory ユーザーとコンピューターを使用してドメイン コント ローラーのオブジェクトを削除するには  
  
1.  をクリックして**開始**、] をクリックして**管理ツール**、] をクリックし、 **Active Directory ユーザーとコンピューター**します。  
2.  コンソール ツリーで、ドメイン コンテナーをダブルクリックし、順にダブルクリック、**ドメイン コント ローラー**組織単位 (OU)。  
3.  詳細ウィンドウで、削除、およびをクリックする DC を右クリックして**削除**します。 
![削除](media/AD-Forest-Recovery-Cleaning-Metadata/delete1.png) 
4.  をクリックして**はい**削除を確定します。 選択、**このドメイン コント ローラーが今後オンラインになるし、Active Directory ドメイン サービス インストール ウィザード (DCPROMO) を使用して降格は、不要になったことができます**] チェック ボックスとクリック**削除**します。  
5.  ドメイン コント ローラーがグローバル カタログ サーバーの場合は、クリックして**はい**いることを確認、削除します。  
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
  
