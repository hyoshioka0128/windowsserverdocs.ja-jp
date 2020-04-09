---
title: タブの順序とグループの変更
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 79a417fd-1b3e-47ab-ae33-bb1faf95c86d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a07cfbef374ff86a8c7845917f0fbae85e7a2235
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817235"
---
# <a name="change-the-order-and-grouping-of-tabs"></a>タブの順序とグループの変更

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

ダッシュボードのタブの順序を変更して、ユーザーのタブをタブの行の (左から) 1 番目のタブにすることができます。 これを行うには、レジストリにエントリを追加します。 レジストリにエントリを追加することで、タブのグループにも影響を与えることができます。 タブは、ユーザーのメイン タブ、Microsoft 内蔵タブ、ユーザーの追加タブ、サード パーティのタブの順序にすることができます。  
  
## <a name="change-the-order-of-the-tabs-in-the-dashboard"></a>ダッシュボードのタブの順序の変更  
 順序を定義するには、タブを表示するアドインの識別子をレジストリに追加する必要があります。  
  
#### <a name="to-display-your-tab-first-in-the-list-of-tabs"></a>タブの一覧でユーザー タブを最初に表示するには  
  
1.  参照コンピューターで、 **[スタート]** ボタンをクリックし、「**regedit**」と入力して、**Enter** キーを押します。  
  
2.  左のウィンドウで、 **[HKEY_LOCAL_MACHINE]** 、 **[SOFTWARE]** 、 **[Microsoft]** 、 **[Windows Server]** の順に展開します。 **[OEM]** キーが存在しない場合は、キーを作成するために次の手順を完了する必要があります。  
  
    1.  **[Windows Server]** を右クリックし、 **[新規作成]** をクリックして、 **[キー]** をクリックします。  
  
    2.  キーの名前に「**OEM**」と入力します。  
  
3.  **[OEM]** を右クリックし、 **[新規]** をクリックし、 **[文字列値]** をクリックします。  
  
4.  文字列名として「**DashboardMainTabID**」と入力し、**Enter** キーを押します。  
  
5.  右側のウィンドウで、新しい文字列を右クリックし、 **[変更]** をクリックします。  
  
6.  最上位タブに対して定義された GUID を入力し、**Enter** キーを押します。  
  
     最上位タブの作成と識別の詳細については、Windows Server Solutions SDK の「 [最上位タブの作成](https://msdn.microsoft.com/library/gg513957) 」を参照してください。  
  
7.  レジストリに変更を保存します。  
  
8.  タブをグループ化するための識別子の一覧に、ユーザーのメイン最上位タブの GUID も含める必要があります。 これを行うには、「**ダッシュボードのタブのグループの変更**」に示された手順を実行します。  
  
## <a name="change-the-grouping-of-tabs-in-the-dashboard"></a>ダッシュボードのタブのグループの変更  
 識別子をレジストリに追加することで、ユーザーのタブがグループ化され、内蔵 Microsoft タブの一覧に含まれます。  
  
#### <a name="to-change-the-grouping-of-tabs"></a>タブのグループを変更するには  
  
1.  regedit が開いていない場合、 **[スタート]** ボタンをクリックして、「**regedit**」と入力し、**Enter** キーを押します。  
  
2.  左のウィンドウで、 **[HKEY_LOCAL_MACHINE]** 、 **[SOFTWARE]** 、 **[Microsoft]** 、 **[Windows Server]** の順に展開します。  
  
3.  **[OEM]** を右クリックし、 **[新規作成]** をクリックして、 **[キー]** をクリックします。  
  
4.  キー名として「**DashboardAddins**」と入力し、**Enter** キーを押します。  
  
5.  **[DashboardAddins]** を右クリックし、 **[新規]** をクリックし、 **[文字列値]** をクリックします。  
  
6.  タブの GUID 識別子を文字列名として入力します。 値は必要ありません。  
  
7.  タブおよびサブタブごとに、手順 5 と 6 を繰り返します。  
  
8.  レジストリの変更を保存します。  
  
## <a name="see-also"></a>参照  
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)