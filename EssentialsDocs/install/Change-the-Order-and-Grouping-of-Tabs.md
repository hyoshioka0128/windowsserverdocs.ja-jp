---
title: "順序とタブ グループを変更します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79a417fd-1b3e-47ab-ae33-bb1faf95c86d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 578c5619cfdf076bb2735254494f393d56d35713
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="change-the-order-and-grouping-of-tabs"></a>順序とタブ グループを変更します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

ダッシュ ボードのタブの順序を変更するには、ユーザーのタブ (左側) タブの行に 1 つ目ができるようにします。 これを行うには、レジストリにエントリを追加します。 タブのグループには、レジストリにエントリを追加しても影響ことができます。 タブの順序には、メイン タブ、Microsoft 内蔵タブ、続けて、その他のタブのいずれかの後に、サード パーティのタブがあります。  
  
## <a name="change-the-order-of-the-tabs-in-the-dashboard"></a>ダッシュ ボードのタブの順序を変更します。  
 順序を定義するためにレジストリに、タブを表示するアドインの識別子を追加する必要があります。  
  
#### <a name="to-display-your-tab-first-in-the-list-of-tabs"></a>タブの一覧で、最初のタブを表示するには  
  
1.  参照コンピューターで、をクリックして**開始**、入力**regedit**、キーを押します**Enter**します。  
  
2.  左側のウィンドウで [ **HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、展開**Microsoft**、し、展開**Windows Server**します。 場合、 **OEM**キーが存在しない、作成時に、次の手順を実行する必要があります。  
  
    1.  右クリック**Windows Server**、] をポイント**新規**、] をクリックし、**キー**します。  
  
    2.  種類**OEM**、キーの名前。  
  
3.  右クリック**OEM**、] をポイント**新規**、] をクリックし、**文字列値**します。  
  
4.  種類**DashboardMainTabID**文字列名と、キーを押します**Enter**します。  
  
5.  右側のウィンドウで、新しい文字列を右クリックし、をクリックして**変更**します。  
  
6.  最上位タブに対して定義された GUID を入力し、キーを押します**Enter**します。  
  
     作成と識別の最上位タブの詳細については、次を参照してください。[最上位タブの作成](https://msdn.microsoft.com/library/gg513957)、Windows Server Solutions SDK にします。  
  
7.  レジストリに変更を保存します。  
  
8.  タブをグループ化するための識別子の一覧で、ユーザーのメイン最上位タブの GUID も含める必要があります。 これを行うに示された手順を実行**ダッシュ ボードのタブのグループを変更**します。  
  
## <a name="change-the-grouping-of-tabs-in-the-dashboard"></a>ダッシュ ボードのタブのグループを変更します。  
 タブがグループ化され、識別子をレジストリに追加することで、内蔵 Microsoft タブの一覧に含まれていることを確認することができます。  
  
#### <a name="to-change-the-grouping-of-tabs"></a>タブのグループを変更するには  
  
1.  Regedit が開いていない場合はクリックして**開始**、入力**regedit**、キーを押します**Enter**します。  
  
2.  左側のウィンドウで [ **HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、展開**Microsoft**、し、展開**Windows Server**します。  
  
3.  右クリック**OEM**、] をポイント**新規**、] をクリックし、**キー**します。  
  
4.  種類**DashboardAddins**続けてキーを押すとキーの名前として**Enter**します。  
  
5.  右クリック**DashboardAddins**、] をポイント**新規**、] をクリックし、**文字列値**します。  
  
6.  文字列名としてユーザーのタブの GUID 識別子を入力します。 値は必要ありません。  
  
7.  タブおよびサブタブごとに、手順 5 と 6 を繰り返します。  
  
8.  レジストリの変更を保存します。  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)