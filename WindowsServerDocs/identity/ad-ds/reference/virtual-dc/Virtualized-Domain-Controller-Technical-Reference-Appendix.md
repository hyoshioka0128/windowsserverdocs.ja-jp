---
ms.assetid: 73a4deba-7da6-4eae-8fdd-2a4d369f9cbb
title: "仮想化ドメイン コント ローラーのテクニカル リファレンス付録"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2e7f264a098b6f67d98c9aa47ec5794374b8920d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="virtualized-domain-controller-technical-reference-appendix"></a>仮想化ドメイン コント ローラーのテクニカル リファレンス付録

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックについて説明します。  
  
-   [用語集](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_Terms)  
  
-   [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)  
  
## <a name="BKMK_Terms"></a>用語集  
  
-   **スナップショット**-特定の時点でのバーチャル マシンの状態。 それは、および仮想化プラットフォーム上で、ハードウェアに、以前に作成されたスナップショットのチェーンに依存します。  
  
-   **複製**- を完了し、仮想マシンのコピーを分離します。 仮想ハードウェア (ハイパーバイザー) に依存しています。  
  
-   **完全な複製**-完全な複製がリソースを共有するありません、親の仮想マシンと複製操作の後に仮想マシンの独立したコピーします。 完全な複製の実行中の操作は、親の仮想マシンから完全に別個です。  
  
-   **差分ディスク**-継続的な方法で、親の仮想マシンと仮想ディスクを共有するバーチャル マシンのコピーします。 これ通常ディスク領域を節約し、同じソフトウェアのインストールを使用する複数の仮想マシンできます。  
  
-   **VM のコピー**- ファイル システム関連のすべてのファイルのコピーおよび仮想マシンのフォルダーです。  
  
-   **VHD ファイルのコピー** -仮想マシンの VHD のコピー  
  
-   **VM 生成 ID** -、128 ビット整数、ハイパーバイザーによって、バーチャル マシンを指定します。 この ID はメモリに格納され、スナップショットが適用されるたびにリセットします。 設計は、仮想マシンで Vm-generation ID を提示するのハイパーバイザーに依存しないメカニズムを使用します。 HYPER-V の実装は、ACPI の表に、仮想マシンの ID を公開します。  
  
-   **インポート/エクスポート**-A HYPER-V 機能により、ユーザーが全体の仮想マシン (VM ファイル、VHD およびマシンの構成) に保存します。 同じ VM (移動)、または新しいバーチャル マシン (コピー) として別のコンピューターで、同じ VM (復元) と同じコンピューターに戻り、マシンにそのファイルのセットを使用するユーザーが許可されます。  
  
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
  


