---
title: DNS ゾーンを編集する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: a35164e1-11ad-47c8-9843-580d30c70d07
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4ee5416bfe416759bc4a190575eb63534ec9b76d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971799"
---
# <a name="edit-a-dns-zone"></a>DNS ゾーンを編集する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、IPAM クライアントコンソールで DNS ゾーンを編集する方法について説明します。

この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

### <a name="to-edit-a-dns-zone"></a>DNS ゾーンを編集するには

1.  サーバーマネージャーで、[ **IPAM**] をクリックします。 IPAM クライアントコンソールが表示されます。

2.  ナビゲーションウィンドウの [**監視と管理**] で、[ **DNS ゾーン数**] をクリックします。 上部のナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。

3.  下のナビゲーションウィンドウで、次のいずれかの選択を行います。

    -   前方参照

    -   IPv4 逆引き参照

    -   IPv6 逆引き参照

4.  たとえば、[IPv4 逆引き参照] を選択します。

    ![ゾーンの種類を選択してください](../../media/Edit-a-DNS-Zone/ipam_EditZone_01.jpg)

5.  表示ウィンドウで、編集するゾーンを右クリックし、[ **DNS ゾーンの編集**] をクリックします。

    ![DNS ゾーンの編集](../../media/Edit-a-DNS-Zone/ipam_EditZone_02.jpg)

6.  [ **DNS ゾーンの編集**] ダイアログボックスが開き、 **[全般**] ページが選択された状態で表示されます。 必要に応じて、[ **DNS サーバー**]、[**ゾーンカテゴリ**]、[**ゾーンの種類**] の [全般] ゾーンプロパティを編集し、[**適用**] をクリックします。編集が完了したら、[ **OK]** をクリックします。

    ![ゾーンのプロパティを編集して保存する](../../media/Edit-a-DNS-Zone/ipam_EditZone_03a.jpg)

7.  [ **DNS ゾーンの編集**] ダイアログボックスで、[**詳細設定**] をクリックします。 **[高度な**ゾーンのプロパティ] ページが開きます。 必要に応じて、変更するプロパティを編集し、[**適用**] をクリックします。編集が完了したら、[ **OK]** をクリックします。

    ![高度なゾーンのプロパティの編集](../../media/Edit-a-DNS-Zone/ipam_EditZone_04a.jpg)

8.  必要に応じて、追加のゾーンプロパティページ名 (ネームサーバー、SOA、ゾーン転送) を選択し、編集を行い、[**適用**] または [ **OK]** をクリックします。 ゾーンの編集をすべて確認するには、[**概要**] をクリックし、[ **OK**] をクリックします。

## <a name="see-also"></a>参照
[DNS ゾーンの管理](DNS-Zone-Management.md) 
[IPAM の管理](Manage-IPAM.md)



