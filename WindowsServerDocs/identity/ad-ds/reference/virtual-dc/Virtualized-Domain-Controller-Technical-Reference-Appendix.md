---
ms.assetid: 73a4deba-7da6-4eae-8fdd-2a4d369f9cbb
title: 仮想化ドメイン コントローラーのテクニカル リファレンスの付録
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9e3a5cc2c71455bb040f1311bdbfed1ac7e213fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832233"
---
# <a name="virtualized-domain-controller-technical-reference-appendix"></a>仮想化ドメイン コントローラーのテクニカル リファレンスの付録

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、次の内容について説明します。  
  
-   [用語集](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_Terms)  
  
-   [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)  
  
## <a name="BKMK_Terms"></a>用語集  
  
-   **スナップショット**-特定の時点で仮想マシンの状態。 ハードウェアで作成された以前のスナップショットのチェーンと仮想化プラットフォームに依存します。  
  
-   **複製**- 完了し、仮想マシンのコピーを区切ります。 仮想ハードウェア (ハイパーバイザー) に依存しています。  
  
-   **完全な複製**-完全な複製は独立したリソースを共有するない親仮想マシンと複製操作の後に仮想マシンのコピー。 完全な複製の実行中の操作は、親の仮想マシンからはまったく別です。  
  
-   **差分ディスク**-継続的な方法で、親の仮想マシンと仮想ディスクを共有する仮想マシンのコピー。 これは、通常ディスク領域を節約でき、同じソフトウェアのインストールを使用する複数の仮想マシン。  
  
-   **VM のコピー**- ファイル システム関連のすべてのファイルのコピーと仮想マシンのフォルダー。  
  
-   **VHD ファイルのコピー** -仮想マシンの VHD のコピー  
  
-   **VM 生成 ID** - ハイパーバイザーで仮想マシンに指定された 128 ビットの整数。 この ID はメモリに格納され、スナップショットが適用されるたびにリセットします。 設計では、ハイパーバイザーに依存しないメカニズムを使用して、仮想マシン内の Vm-generation ID を提示するのです。 HYPER-V の実装では、仮想マシンの ACPI テーブルの ID を公開します。  
  
-   **インポート/エクスポート**-ユーザーは、全体の仮想マシン (VM ファイル、VHD と、マシンの構成) を保存できるようにする、HYPER-V 機能です。 同じ VM (移動)、または新しい VM を (コピー) として別のコンピューターにユーザーが、同じ VM (復元) と同じコンピューターに戻り、マシンをそのファイルのセットを使用して、します。  
  
## <a name="BKMK_FixPDCPerms"></a>FixVDCPermissions.ps1  
  
```  
# Unsigned script, requires use of set-executionpolicy remotesigned -force  
# You must run the Windows PowerShell console as an elevated administrator  
  
# Load Active Directory Windows PowerShell Module and switch to AD DS drive  
import-module activedirectory  
cd ad:  
  
## Get Domain NC  
$domainNC = get-addomain  
  
## Get groups and obtain their SIDs   
$dcgroup = get-adgroup "Cloneable Domain Controllers"  
  
$sid1 = (get-adgroup $dcgroup).sid  
  
## Get the DACL of the domain  
$acl = get-acl $domainNC  
  
## The following object specific ACE grants extended right 'Allow a DC to create a clone of itself' for the CDC group to the Domain NC  
## 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e is the schemaIDGuid for 'DS-Clone-Domain-Controller"  
  
$objectguid = new-object Guid 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e  
$ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid1,"ExtendedRight","Allow",$objectguid  
  
## Add the ACE in the ACL and set the ACL on the object   
  
$acl.AddAccessRule($ace1)  
set-acl -aclobject $acl $domainNC  
write-host "Done writing new VDC permissions."  
cd c:   
```  
  


