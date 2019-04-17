---
title: "AD フォレストの回復の仮想化"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adfs
ms.openlocfilehash: 08b0c4a4c5ed230f91241fcfb67db1749935c5e2
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2017
---
# <a name="active-directory-forest-recovery-virtualization"></a>Active Directory フォレストの回復の仮想化

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

このトピックでは、Windows Server 2016、2012 R2、および 2012 で仮想化ドメイン コントローラーの複製機能について説明します。  
 
## <a name="using-virtualized-domain-controller-cloning-to-expedite-forest-recovery"></a>仮想化ドメイン コントローラーの複製を使用して、フォレストの回復を迅速化するには  
 仮想化ドメイン コントローラー (DC) の複製では、簡素化され、ドメインでは、特にいくつかの Dc がハイパーバイザーで実行する場所のデータ センターなどの一元化された場所で追加の仮想化 Dc をインストールするためのプロセスが見込まれます。 各ドメインで 1 つの仮想 DC をバックアップから復元した後の各ドメイン内の他の Dc できます迅速にオンラインにする、仮想化 DC の複製プロセスを使用しています。 回復、シャット ダウン、し、コピーする最初の仮想化 DC を準備するその仮想ハード ディスクのために必要なだけ何回作成複製されるとは、ドメインを構築するための Dc を仮想化します。  
  
 仮想化 DC の複製の要件は次のとおりです。  
  
-   ハイパーバイザーが VM-GenerationID をサポートする必要があります。 Hyper-V で Windows Server 2016、2012 および Windows 8 は、VM-GenerationID をサポートするハイパーバイザーの例を示します。 VM-GenerationID がサポートされている場合は、ハイパーバイザー ベンダーに確認します。  
  
-   複製のソースとして使用されている仮想化 DC は、Windows Server 2016 または 2012 を実行し、複製可能なドメイン コントローラー グループのメンバーである必要があります。  
  
-   PDC エミュレーターは、Windows Server 2016 または 2012 を実行する必要があります。 仮想化されている場合は、PDC エミュレーターを複製することができます。  
  
 実行する方法に関する詳細な手順については、DC の複製を仮想化を参照してください[Introduction to Active Directory ドメイン サービス (AD DS) Virtualization (Level 100)](../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)します。 方法の詳細については、DC の複製機能を仮想化を参照してください[仮想化ドメイン コントローラーのテクニカル リファレンス (レベル 300)](../deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-.md)します。  

-   [AD フォレストの回復の前提条件](AD-Forest-Recovery-Prerequisties.md)  
-   [AD フォレストの回復 - カスタム フォレスト回復計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復 - 問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
-   [AD フォレストの回復 - を回復する方法を決定します。](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [AD フォレストの回復 - 最初の回復を実行](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
-   [AD フォレストの回復のよく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
-   [AD フォレストの回復であれば、マルチ ドメイン フォレスト内で 1 つのドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [AD フォレストの回復 - Windows Server 2003 ドメイン コントローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md) 

  
