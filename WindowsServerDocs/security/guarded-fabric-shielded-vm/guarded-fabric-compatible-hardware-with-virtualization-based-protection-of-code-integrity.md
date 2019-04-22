---
title: コードの整合性の Windows Server 仮想化ベースの保護との互換性のあるハードウェア
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 15ded82c-f70f-4efb-9e26-2731127931af
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: a52ff808af94159fe50c72bf0466768047ceea90
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820373"
---
# <a name="compatible-hardware-with-windows-server-virtualization-based-protection-of-code-integrity"></a>コードの整合性の Windows Server 仮想化ベースの保護との互換性のあるハードウェア

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 には、システム コードを変更する攻撃から物理的に保護するために新しい仮想化ベースのコード保護と仮想マシンが導入されました。 Microsoft は、この高度な保護レベルを実現するために、システムの実行のコードに相手先ブランド供給 (Oem) 悪意のある書き込みを防ぐためには、コンピューター ハードウェアの製造元と連携して動作します。 この保護は、任意のシステムに適用されることができ、シールドされた仮想マシン (Vm) の HYPER-V ホストの正常性を実装するため、構成要素の 1 つとして使用します。 

任意のハードウェア ベースの保護と一部のシステムできない可能性がありますメモリ ページの実行可能ファイルとして、または実際にデータの損失、青いなど予期しないエラーが発生する場合があります、実行時にコードを変更しようとしての不正なマークなどの問題が原因で準拠しています。画面のエラー (stop エラーとも呼ばれます)。 

互換性を新しいセキュリティ機能を完全にサポートは、Oem は UEFI 2.6 では、2016 の 1 月に公開されたで定義されているメモリ アドレス テーブルを実装する必要があります。 標準の新しい UEFI の導入の時間します。その一方で、問題が発生する顧客を防ぐためには、するシステムと構成設定でこの機能をテストしましたが、およびそのシステムに互換性がないことがわかっているに関する情報を提供します。 

## <a name="non-compatible-systems"></a>互換性のないシステム

次の構成は互換性のないとわかっているの仮想化ベースの保護とコードの整合性とシールドされた Vm のホストとして使用できません。

- 詳細については、PERC H330 RAID コント ローラーを実行している Dell PowerEdge サーバー Dell サポートから、次の記事を参照してください[H330 – 有効化「Host Guardian HYPER-V サポート」または"Device Guard"Win 2016 OS で OS 起動エラーの原因](http://www.dell.com/Support/Article/us/en/19/QNA44045)します。  


## <a name="compatible-systems"></a>互換性のあるシステム

これらは、および当社のパートナーをこの環境でテストされていますが、システムです。 システムが環境内で期待どおりに動作を確認することを確認してください。 

- Virtual Machines-Windows Server 2016 以降で HYPER-V ホスト上で実行する仮想マシンでのコードの整合性の仮想化ベースの保護を有効にできます。



