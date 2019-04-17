---
title: "AD フォレストの回復 - 非 Authoritative restore"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e4ce1d18-d346-492a-8bca-f85513aa3ac1
ms.technology: identity-adfs
ms.openlocfilehash: 684672491a0574b12e9b117a8e3c9c1f0936f357
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="performing-a-nonauthoritative-restore-of-active-directory-domain-services"></a>Active Directory ドメイン サービスの非 authoritative restore を実行します。 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:
 
 非 authoritative restore を実行するには、次の手順を実行します。  
  
 次の手順では、Wbadmin.exe を使用して、Active Directory や Active Directory ドメイン サービス (AD DS) の非 authoritative restore を実行します。 さまざまなバックアップ ソリューションを使用している場合、またはフォレスト回復プロセスの後で SYSVOL の authoritative restore を完了する場合は、これらの方法を使用して SYSVOL の authoritative restore を実行できます。  
  
-   ファイル レプリケーション サービス (FRS) SYSVOL をレプリケートするを使用している場合の手順に従います[記事 290762](https://go.microsoft.com/fwlink/?LinkId=148443)、Microsoft サポート技術情報を使用して、**BurFlags**レジストリ キーを再初期化してから、FRS レプリカ セットまたは必要に応じて、記事 315457 [315457](https://support.microsoft.com/kb/315457)SYSVOL 順にツリーを再構築します。 Frs SYSVOL をレプリケートするかどうかを確認するのを参照してください。[DFSR または FRS で決定するかどうか、ドメイン コントローラーの SYSVOL フォルダーはレプリケート](https://msdn.microsoft.com/en-us/library/windows/desktop/cc507518.aspx#determining_whether_a_domain_controller_s_sysvol_folder_is_replicated_by_dfsr_or_frs)します。  
  
-   SYSVOL をレプリケートする分散ファイル システム (DFS) レプリケーションを使用する場合は「[DFSR でレプリケートされた SYSVOL の権限のある、同期実行](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)します。  
  
 
## <a name="performing-a-nonauthoritative-restore"></a>非 authoritative restore を実行します。  
 Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 を実行している DC で wbadmin.exe を使用して AD DS の権限のない復元と同時に SYSVOL の authoritative restore を実行するのにには、次の手順を使用します。 バックアップがシステム状態データを明示的に含める必要があります。サーバーの完全回復に使用するサーバーの完全バックアップは機能しません。 システム状態のバックアップの作成の詳細については、次を参照してください。[システム状態データをバックアップする](AD-Forest-Recovery-Backing-up-System-State.md)します。  
  
### <a name="to-perform-a-nonauthoritative-restore-of-ad-ds-and-authoritative-restore-of-sysvol-using-wbadminexe"></a>AD DS の非 authoritative restore および wbadmin.exe を使用して SYSVOL の authoritative restore を実行するには  
  
-   含める、**- authsysvol**次の例のように、回復コマンド内のスイッチします。  
  
    ```  
    wbadmin start systemstaterecovery <otheroptions> -authsysvol  
    ```  
  
     例えば：  
  
    ```  
    wbadmin start systemstaterecovery -version:11/20/2012-13:00 -authsysvol  
    ```  
  
 ![復元](media/AD-Forest-Recovery-Nonauthoritative-Restore/nonauth.png)

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
