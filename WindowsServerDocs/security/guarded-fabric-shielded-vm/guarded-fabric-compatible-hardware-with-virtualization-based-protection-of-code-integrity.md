---
title: 互換性のあるハードウェアと Windows Server Virtualization によるコードの整合性保護
ms.topic: article
ms.assetid: 15ded82c-f70f-4efb-9e26-2731127931af
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 616718b2b2a5ce3c30655d3fef37da5ee2ea25e5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971359"
---
# <a name="compatible-hardware-with-windows-server-virtualization-based-protection-of-code-integrity"></a>互換性のあるハードウェアと Windows Server Virtualization によるコードの整合性保護

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 では、システムコードを変更する攻撃から物理マシンと仮想マシンを保護するために、新しい仮想化ベースのコード保護が導入されました。
この高い保護レベルを実現するために、Microsoft はコンピューターのハードウェアメーカー (相手先ブランド供給メーカー、または Oem) と連携して、システム実行コードへの悪意のある書き込みを防止します。
この保護は任意のシステムに適用でき、シールドされた仮想マシン (Vm) の Hyper-v ホストの正常性を実装するための構成要素の1つとして使用されます。

ハードウェアベースの保護と同様に、一部のシステムは、実行可能ファイルとしてのメモリページの不適切なマーキング、実際に実行時にコードを変更しようとするなどの問題が原因で準拠していない可能性があります

新しいセキュリティ機能を完全にサポートするには、Oem は、2.6 2016 年1月に公開された UEFI で定義されているメモリアドレステーブルを実装する必要があります。
新しい UEFI 標準の導入には時間がかかります。その一方で、お客様が問題を発生させないようにするために、この機能セットをテストしたシステムと構成、および互換性のないことがわかっているシステムに関する情報を提供したいと考えています。

## <a name="non-compatible-systems"></a>互換性のないシステム

次の構成は、仮想化ベースのコードの整合性保護との互換性がないことがわかっているため、シールドされた Vm のホストとして使用することはできません。

- PERC H330 RAID コントローラーを実行する dell PowerEdge サーバー詳細については、「Dell サポート H330」の次の記事を参照してください。 [Win 2016 os で "Host Guardian Hyper-v Support" または "Device Guard" を有効にすると os のブートエラー](http://www.dell.com/Support/Article/us/en/19/QNA44045)が発生します。


## <a name="compatible-systems"></a>互換性のあるシステム

これらのシステムは、当社とパートナーの環境でテストされています。
システムが環境内で期待どおりに動作することを確認してください。

- Virtual Machines – Windows Server 2016 以降の Hyper-v ホスト上で実行される仮想マシンで、仮想化ベースのコードの整合性保護を有効にすることができます。



