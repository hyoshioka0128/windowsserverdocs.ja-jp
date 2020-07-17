---
title: AD フォレストの回復-削除された dc のメタデータをクリーニングしています
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: e7543381-4081-407f-adad-a9de792c6616
ms.technology: identity-adds
ms.openlocfilehash: b9ba00939ccb2ee747501733fb9654edb4c8132e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824255"
---
# <a name="ad-forest-recovery---cleaning-metadata-of-removed-writable-domain-controllers"></a>AD フォレストの回復-削除された書き込み可能なドメインコントローラーのメタデータをクリーニングしています

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

メタデータのクリーンアップでは、DC を識別するデータをレプリケーションシステムに Active Directory 削除します。  

次の手順を使用して、AD DS を再インストールして、ネットワークに戻す予定の dc の DC オブジェクトを削除します。  
  
Active Directory ユーザーとコンピューター、またはリモートサーバー管理ツール (RSAT) に含まれる Active Directory サイトとサービスのバージョンを使用している場合、DC オブジェクトを削除すると、メタデータのクリーンアップが自動的に実行されます。  

## <a name="deleting-a-domain-controller-using-active-directory-users-and-computers"></a>Active Directory ユーザーとコンピューターを使用してドメインコントローラーを削除する

Active Directory ユーザーとコンピューターのバージョン、またはリモートサーバー管理ツール (RSAT) の Active Directory 管理センターを使用する場合、DC オブジェクトを削除するとメタデータのクリーンアップが自動的に実行されます。 サーバーオブジェクトとコンピューターオブジェクトも自動的に削除されます。  

代わりに、RSAT の Active Directory サイトとサービスを使用して、DC オブジェクトを削除することもできます。 Active Directory サイトとサービスを使用する場合は、DC オブジェクトを削除する前に、関連付けられているサーバーオブジェクトと NTDS 設定オブジェクトを削除する必要があります。  

RSAT のインストールの詳細については、「[リモートサーバー管理ツール](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)」を参照してください。
  
次の手順は、Windows Server 2016、2012、2008 R2、または2008のいずれかを実行している Dc でも同じです。 メタデータクリーンアップ操作のターゲット DC は、任意のバージョンの Windows Server を実行できます。  
  
### <a name="to-delete-a-domain-controller-object-using-active-directory-users-and-computers-in-rsat"></a>RSAT で Active Directory ユーザーとコンピューターを使用してドメインコントローラーオブジェクトを削除するには  
  
1. **[スタート]** 、 **[管理ツール]** の順にクリックし、 **[Active Directory ユーザーとコンピュータ]** をクリックします。  
2. コンソールツリーで、ドメインコンテナーをダブルクリックし、**ドメインコントローラー**の組織単位 (OU) をダブルクリックします。  
3. 詳細ウィンドウで、削除する DC を右クリックし、 **[削除]** をクリックします。
   ![削除](media/AD-Forest-Recovery-Cleaning-Metadata/delete1.png) 
4. **[はい]** をクリックして削除を確定します。 [**このドメインコントローラーは完全にオフラインになっており、Active Directory ドメインサービスインストールウィザード (DCPROMO)] チェックボックスを使用して降格できなく**なり、 **[削除]** をクリックします。  
5. DC がグローバルカタログサーバーである場合は、[**はい]** をクリックします。削除されたことを確認します。  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
