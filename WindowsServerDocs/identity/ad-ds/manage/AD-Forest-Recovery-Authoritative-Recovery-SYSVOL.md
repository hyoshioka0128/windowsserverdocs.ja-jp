---
title: AD フォレストの回復-SYSVOL の権限のある同期
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 38a1c543-c76d-4b8e-a06b-53742aaa172f
ms.openlocfilehash: 8d4df4b7b893c0c6e8fc6b467ee115e9013335f9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956899"
---
# <a name="ad-forest-recovery---performing-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>AD フォレストの回復-DFSR によってレプリケートされた SYSVOL の権限のある同期を実行する

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

SYSVOL の authoritative restore を実行するには、さまざまな方法があります。 **Msdfsr-Options**属性を編集するか、wbadmin – authsysvol を使用してシステム状態の復元を実行することができます。 システム状態のバックアップを復元するオプションがある場合 (つまり、AD DS を同じハードウェアおよびオペレーティングシステムのインスタンスに復元する場合)、wbadmin – authsysvol を使用する方が簡単です。 ただし、ベアメタル復元を実行する必要がある場合は、 **Msdfsr-Options**属性を編集する必要があります。

次の手順を使用して、 **msdfsr-Options**属性を編集することにより、SYSVOL の権限のある同期を実行します (DFSR を使用してレプリケートされている場合)。 SYSVOL が FRS を使用してレプリケートされる場合は、[記事 290762](https://go.microsoft.com/fwlink/?LinkId=148443)を参照してください。

## <a name="to-perform-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>DFSR でレプリケートされた SYSVOL の権限のある同期を実行するには

1. [Active Directory ユーザーとコンピューター] を開きます。
2. [**表示**] をクリックし、[**コンテナーとしてのユーザー、連絡先、グループ、およびコンピューター** ] と [**高度な機能**] を選択します。

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol1.png)

3. ツリービューで、[**ドメインコントローラー**]、復元した DC の名前、 **LocalSettings**、[**ドメインシステムボリューム**] の順にクリックします。

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol2.png)

4. 詳細ウィンドウで、[ **SYSVOL サブスクリプション**] を右クリックし、[**プロパティ**] をクリックして、[**属性エディター**] をクリックします。

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol3.png)

5. [ **Msdfsr-Options**] をクリックし、[**編集**] をクリックして「 **1**」と入力し、[ **OK** ] をクリックします。

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol4.png)

6. [ **OK** ] をクリックして属性エディターを閉じます。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
