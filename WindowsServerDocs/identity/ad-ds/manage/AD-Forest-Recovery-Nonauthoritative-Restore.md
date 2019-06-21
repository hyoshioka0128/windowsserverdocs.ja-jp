---
title: AD フォレストの回復の権限のない状態の復元
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e4ce1d18-d346-492a-8bca-f85513aa3ac1
ms.technology: identity-adds
ms.openlocfilehash: 65e33e6507d2affc4d07cc0780a7baf91a170a09
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280585"
---
# <a name="performing-a-nonauthoritative-restore-of-active-directory-domain-services"></a>Active Directory Domain Services の権限のない状態の復元を実行します。 

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

権限のない状態の復元を実行するには、次の手順を実行します。  
  
次の手順では、Active Directory または Active Directory Domain Services (AD DS) の権限のない状態の復元を実行するのに、Wbadmin.exe を使用します。 別のバックアップ ソリューションを使用している場合、またはフォレスト回復のプロセスの後半で SYSVOL の authoritative restore を完了する場合は、これらの方法を使用して、SYSVOL の authoritative restore を実行できます。  
  
- ファイル レプリケーション サービス (FRS) の SYSVOL レプリケートするを使用している場合の手順に従います[記事 290762](https://go.microsoft.com/fwlink/?LinkId=148443)マイクロソフト サポート技術情報を使用して、 **BurFlags** FRS レプリカを再初期化するレジストリ キーセット、または必要に応じて、アーティクル 315457 [315457](https://support.microsoft.com/kb/315457)SYSVOL ツリーを再構築します。 Frs SYSVOL をレプリケートするかどうかを確認するのを参照してください。[を決定するかどうか、ドメイン コント ローラーの SYSVOL フォルダーは、DFSR または FRS によってレプリケートされた](https://msdn.microsoft.com/library/windows/desktop/cc507518.aspx#determining_whether_a_domain_controller_s_sysvol_folder_is_replicated_by_dfsr_or_frs)します。  
- SYSVOL をレプリケートする分散ファイル システム (DFS) レプリケーションを使用する場合は、次を参照してください。 [DFSR でレプリケートされた SYSVOL の権限のある同期を実行](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)します。  

## <a name="performing-a-nonauthoritative-restore"></a>権限のない復元を実行します。

Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 を実行している DC で wbadmin.exe を使用して AD DS の権限のない状態の復元と SYSVOL の authoritative restore と同時を実行するのにには、次の手順を使用します。 バックアップがシステム状態データを明示的に含める必要があります。サーバー全体の回復に使用されるサーバーの完全バックアップは機能しません。 システム状態のバックアップを作成する方法の詳細については、次を参照してください。[システム状態データをバックアップする](AD-Forest-Recovery-Backing-up-System-State.md)します。  
  
### <a name="to-perform-a-nonauthoritative-restore-of-ad-ds-and-authoritative-restore-of-sysvol-using-wbadminexe"></a>Wbadmin.exe を使用して SYSVOL の権限のない状態の復元を使用している AD DS の権限のある復元を実行するには  
  
- 含まれて、 **- authsysvol**次の例に示すように回復コマンドで切り替えます。  

   ```  
   wbadmin start systemstaterecovery <otheroptions> -authsysvol  
   ```  

   例:  

   ```  
   wbadmin start systemstaterecovery -version:11/20/2012-13:00 -authsysvol  
   ```  
  
![[復元]](media/AD-Forest-Recovery-Nonauthoritative-Restore/nonauth.png)

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
