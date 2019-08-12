---
title: Web アクセスを制限する
description: MultiPoint Services でインターネットへのユーザーアクセスを制限する方法について説明します。
ms.custom: na
ms.date: 07/08/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 044f2fd5-5b87-42bb-ba0d-c06516ac48c8
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: cb91914608110d26ff2db8eff1cd28d26d04669b
ms.sourcegitcommit: 9f955be34c641b58ae8b3000768caa46ad535d43
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2019
ms.locfileid: "68590348"
---
# <a name="limit-web-access"></a>Web アクセスを制限する
個々のデスクトップ上のユーザーアクティビティを監視するだけでなく、管理ユーザーは、ユーザーのアクセスをブロックする web サイトや web サイトを指定することによって、特定の web サイトへのユーザーのアクセスを制限することができます。  
  
## <a name="to-limit-web-access-on-a-station"></a>ステーションの Web アクセスを制限するには  
  
1. MultiPoint ダッシュボードの [ **Web 制限**] タブで、[**構成**] をクリックします。 **[Web 制限の構成]** ページが開きます。 ユーザーがアクセスできるサイトが一覧表示されます。  
  
2. Web アクセスを制限するユーザー ステーションのサムネイル画像をクリックします。  
  
3. **[選択されている項目のタスク]** の **[このステーションの Web アクセスを制限する]** をクリックします。 **[Web 制限の構成]** ページが開きます。 ユーザーがアクセスできるサイトが一覧表示されます。  
  
4. アクセスを許可するサイトを追加するには、Web アドレスを入力し、**[追加]** をクリックします。  
  
   > [!NOTE]
   > たとえば、「Contoso.com」と入力すると、www\.contoso.com を基準とするサイトが許可またはブロックされます (たとえば、www\.newpage.contoso.com)。 「Contoso」と入力すると、すべての Contoso 関連サイト (contoso.com、contoso.uk など) が許可または制限されます。  
  
5. 許可するサイトの一覧から Web アドレスを削除するには、アクセスを削除する Web アドレスをクリックし、**[削除]** をクリックします。  
  
## <a name="to-limit-web-access-on-all-stations"></a>すべてのステーションの Web アクセスを制限するには  
  
1. MultiPoint ダッシュボードの [ **Web 制限**] タブで、[開始] ドロップ\-ダウンメニューをクリックし、[**すべてのデスクトップで Web アクセスを制限**する] をクリックします。  
  
   **[Web 制限の構成]** ページが開きます。 ユーザーがアクセスできるサイトが一覧表示されます。 次のいずれかの操作を行います。  
  
2. 許可するサイトを追加するには、**[これらのサイトのみを許可する]** をクリックし、許可する Web アドレスを入力し、**[追加]** をクリックします。  
  
   ユーザーのアクセスを禁止するサイトを追加するには、**[これらのサイトのみを禁止する]** をクリックし、ユーザーのアクセスを禁止する Web アドレスを入力し、**[追加]** をクリックします。  
  
   > [!NOTE]
   > たとえば、「Contoso.com」と入力すると、 [www.contoso.com](www.contoso.com) に対して相対的なサイトが許可またはブロックされます (たとえば、[www.newpage.contoso.com](www.newpage.contoso.com) )。 「Contoso」と入力すると、すべての Contoso 関連サイト (contoso.com、contoso.uk など) が許可または制限されます。  
  
3. 許可または禁止するサイトの一覧から Web アドレスを削除するには、Web アドレスを選択し、**[削除]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
[ユーザーデスクトップの管理](manage-user-desktops-using-multipoint-dashboard.md)  
