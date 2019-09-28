---
ms.assetid: 73a4deba-7da6-4eae-8fdd-2a4d369f9cbb
title: 仮想化ドメイン コントローラーのテクニカル リファレンスの付録
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e1018d5bbff5922df5a696e5c4fad12dc9f6ec3d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408585"
---
# <a name="virtualized-domain-controller-technical-reference-appendix"></a>仮想化ドメイン コントローラーのテクニカル リファレンスの付録

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、次の内容について説明します。  
  
-   [用語](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_Terms)  
  
-   [Fixvdcpermissions.ps1](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)  
  
## <a name="BKMK_Terms"></a>関する  
  
-   **Snapshot** -特定の時点における仮想マシンの状態。 これは、作成された以前のスナップショットのチェーン、ハードウェア、および仮想化プラットフォームに依存します。  
  
-   **複製**-仮想マシンの完全で個別のコピー。 これは、仮想ハードウェア (ハイパーバイザー) に依存します。  
  
-   **完全な複製**-完全な複製は、複製操作後に親仮想マシンとリソースを共有しない仮想マシンの独立したコピーです。 完全な複製の継続的な操作は、親のバーチャルマシンと完全に分離されています。  
  
-   **差分ディスク**-親仮想マシンと仮想ディスクを継続的に共有する仮想マシンのコピー。 これにより、通常、ディスク領域が節約され、複数の仮想マシンが同じソフトウェアインストールを使用できるようになります。  
  
-   **VM コピー**-仮想マシンのすべての関連ファイルとフォルダーのファイルシステムコピー。  
  
-   **Vhd ファイルのコピー** -仮想マシンの vhd のコピー  
  
-   **VM 生成 ID** -ハイパーバイザーによって仮想マシンに指定された128ビットの整数。 この ID はメモリに格納され、スナップショットが適用されるたびにリセットされます。 この設計では、仮想マシンで VM 生成 ID を提示するために、ハイパーバイザーに依存しないメカニズムを使用します。 Hyper-v 実装は、仮想マシンの ACPI テーブルで ID を公開します。  
  
-   **Import/Export** -仮想マシン全体 (VM ファイル、VHD、およびマシン構成) を保存することをユーザーに許可する hyper-v の機能。 その後、ユーザーはそのファイルセットを使用して、同じ VM (復元) と同じマシン上にコンピューターを戻すことができます。また、同じ VM (移動)、または新しい VM (コピー) としてコンピューターを戻すことができます。  
  
## <a name="BKMK_FixPDCPerms"></a>Fixvdcpermissions.ps1  
  
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
  


