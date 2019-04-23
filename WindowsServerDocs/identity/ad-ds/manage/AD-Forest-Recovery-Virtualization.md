---
title: AD フォレスト回復の仮想化
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adds
ms.openlocfilehash: 23317f55fdce18e78ac3e7e1490f6fc4937fd062
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858453"
---
# <a name="active-directory-forest-recovery-virtualization"></a>Active Directory フォレスト回復の仮想化

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

このトピックでは、Windows Server 2016、2012 R2、および 2012 で仮想化ドメイン コント ローラーの複製機能について説明します。  

## <a name="using-virtualized-domain-controller-cloning-to-expedite-forest-recovery"></a>仮想化ドメイン コント ローラーの複製を使用して、フォレストの回復を高速化するには

仮想化ドメイン コント ローラー (DC) の複製を簡略化し、ハイパーバイザー上いくつかの Dc を実行しているデータ センターなどの一元的な場所で特に、ドメインの追加の仮想化 Dc をインストールするプロセスを迅速化します。 ドメインごとに 1 つの仮想 DC をバックアップから復元した後各ドメイン内の他の Dc は迅速にオンラインにする、仮想化 DC の複製プロセスを使用しています。 準備するには、最初の仮想化 DC の回復、シャット ダウンし、コピーをその仮想ハード ディスクのために必要な回数だけが複製された作成は、ドメインを構築するための Dc を仮想化します。  
  
仮想化 DC の複製するための要件は次のとおりです。  
  
- ハイパーバイザーが Vm-generationid をサポートする必要があります。 HYPER-V は Windows Server 2016、2012、Windows 8 は、Vm-generationid をサポートするハイパーバイザーの例とします。 Vm-generationid がサポートされている場合、ハイパーバイザー ベンダーに確認します。  
- 複製のソースとして使用される仮想化 DC は、Windows Server 2016 または 2012 を実行し、Cloneable Domain Controllers グループのメンバーである必要があります。 
- PDC エミュレーターは、Windows Server 2016 または 2012 を実行する必要があります。 仮想化されている場合は、PDC エミュレーターを複製することができます。  
  
詳細な手順を実行する方法については、DC の複製を仮想化を参照してください[Active Directory Domain Services (AD DS) Virtualization (Level 100) の概要](../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)します。 方法の詳細については、DC の複製機能を仮想化を参照してください[仮想化ドメイン コント ローラーのテクニカル リファレンス (レベル 300)](../deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-.md)します。 

## <a name="next-steps"></a>次のステップ

- [AD フォレストの回復 - 前提条件](AD-Forest-Recovery-Prerequisties.md)  
- [AD フォレストの回復 - カスタム フォレスト回復の計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復の問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD フォレストの回復に回復する方法を決定](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD フォレストの回復 - 最初の回復を実行します。](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
- [AD フォレストの回復 - よく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
- [AD フォレストの回復 - Multidomain フォレスト内の 1 つのドメインを回復します。](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD フォレストの回復 - Windows Server 2003 ドメイン コント ローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md) 
