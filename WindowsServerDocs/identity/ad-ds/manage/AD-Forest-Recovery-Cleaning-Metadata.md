---
title: 削除された dc のメタデータのクリーニング - AD フォレストの回復
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e7543381-4081-407f-adad-a9de792c6616
ms.technology: identity-adds
ms.openlocfilehash: b71cab51a362a96ab6071e5eed3cf31c4421041c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843043"
---
# <a name="ad-forest-recovery---cleaning-metadata-of-removed-writable-domain-controllers"></a>削除された書き込み可能なドメイン コント ローラーのメタデータのクリーニング - AD フォレストの回復

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

メタデータのクリーンアップは、DC にレプリケーション システムを識別する Active Directory データを削除します。  

AD DS の再インストールによるネットワークに追加するのに予定の Dc の DC オブジェクトを削除するのにには、次の手順を使用します。  
  
Active Directory ユーザーとコンピューターのバージョンを使用しているかは、Active Directory サイトとサービスにリモート サーバー管理ツール (RSAT) が含まれている、DC オブジェクトを削除するときにメタデータのクリーンアップが自動的に実行します。  

## <a name="deleting-a-domain-controller-using-active-directory-users-and-computers"></a>Active Directory ユーザーとコンピューターを使用してドメイン コント ローラーを削除します。

Active Directory ユーザーとコンピューター、または Active Directory 管理センター リモート サーバー管理ツール (RSAT) でのバージョンを使用するとメタデータのクリーンアップが自動的に実行 DC オブジェクトを削除するときに。 サーバー オブジェクトとコンピューター オブジェクトが自動的に削除もされます。  

代わりに、使用することできますも Active Directory サイトとサービス RSAT で DC オブジェクトを削除します。 Active Directory サイトとサービスを使用する場合は、DC オブジェクトを削除する前に、関連付けられているサーバー オブジェクト、NTDS 設定オブジェクトを削除する必要があります。  

RSAT をインストールする方法の詳細については、この記事を参照してください。[リモート サーバー管理ツール](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)します。
  
次の手順は、いずれか Windows Server 2016、2012、2008 R2、または 2008 を実行しているドメイン コント ローラーは同じです。 メタデータのクリーンアップ操作のターゲット DC では、任意のバージョンの Windows Server を実行できます。  
  
### <a name="to-delete-a-domain-controller-object-using-active-directory-users-and-computers-in-rsat"></a>RSAT で Active Directory ユーザーとコンピューターを使用して、ドメイン コント ローラー オブジェクトを削除するには  
  
1. **[スタート]**、**[管理ツール]** の順にクリックし、**[Active Directory ユーザーとコンピュータ]** をクリックします。  
2. コンソール ツリーで、ドメインのコンテナーをダブルクリックし、ダブルクリック、**ドメイン コント ローラー**組織単位 (OU)。  
3. 詳細ペインで、削除、およびクリックする DC を右クリックして**削除**します。
   ![削除](media/AD-Forest-Recovery-Cleaning-Metadata/delete1.png) 
4. クリックして**はい**削除を確定します。 選択、**このドメイン コント ローラーは完全にオフラインであり、Active Directory ドメイン サービス インストール ウィザード (DCPROMO) を使用して不要になった降格できます** チェック ボックスをクリックします**削除**します。  
5. DC がグローバル カタログ サーバーの場合は、クリックして**はい**ことを確認します、削除します。  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
