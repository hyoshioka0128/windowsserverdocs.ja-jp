---
title: Web アクセスを制限する
description: MultiPoint Services でインターネットへのユーザーアクセスを制限する方法について説明します。
ms.date: 07/08/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 044f2fd5-5b87-42bb-ba0d-c06516ac48c8
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 485c82284df4d77eea075d092fa08c820567f6c3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853685"
---
# <a name="limit-web-access"></a>Web アクセスを制限する
個々のデスクトップ上のユーザーアクティビティを監視するだけでなく、管理ユーザーは、ユーザーのアクセスをブロックする web サイトや web サイトを指定することによって、特定の web サイトへのユーザーのアクセスを制限することができます。  
  
## <a name="to-limit-web-access-on-a-station"></a>ステーションの Web アクセスを制限するには  
  
1. MultiPoint ダッシュボードの **[Web 制限]** タブで、 **[構成]** をクリックします。 **[Web 制限の構成]** ページが開きます。 ユーザーがアクセスできるサイトが一覧表示されます。  
  
2. Web アクセスを制限するユーザー ステーションのサムネイル画像をクリックします。  
  
3. **[選択されている項目のタスク]** の **[このステーションの Web アクセスを制限する]** をクリックします。 **[Web 制限の構成]** ページが開きます。 ユーザーがアクセスできるサイトが一覧表示されます。  
  
4. アクセスを許可するサイトを追加するには、Web アドレスを入力し、 **[追加]** をクリックします。  
  
   > [!NOTE]
   > たとえば、「Contoso.com」と入力すると、www\.contoso.com を基準とするサイトが許可またはブロックされます (たとえば、www\.newpage.contoso.com)。 「Contoso」と入力すると、すべての Contoso 関連サイト (contoso.com、contoso.uk など) が許可または制限されます。  
  
5. 許可するサイトの一覧から Web アドレスを削除するには、アクセスを削除する Web アドレスをクリックし、 **[削除]** をクリックします。  
  
## <a name="to-limit-web-access-on-all-stations"></a>すべてのステーションの Web アクセスを制限するには  
  
1. MultiPoint ダッシュボードの **[Web 制限]** タブで、開始 ドロップダウンメニューをクリックし、 **[すべてのデスクトップで Web アクセスを制限]** する をクリックし\-ます。  
  
   **[Web 制限の構成]** ページが開きます。 ユーザーがアクセスできるサイトが一覧表示されます。 以下のいずれかを実行します。  
  
2. 許可するサイトを追加するには、 **[これらのサイトのみを許可する]** をクリックし、許可する Web アドレスを入力し、 **[追加]** をクリックします。  
  
   ユーザーがアクセスできないようにするサイトを追加するには、 **[これらのサイトのみを許可]** する をクリックし、ユーザーにアクセスしない web アドレスを入力して、 **[追加]** をクリックします。  
  
   > [!NOTE]
   > たとえば、「Contoso.com」と入力すると、 www.contoso.com に対して相対的なサイトが許可または ブロックされます (たとえば、www\.newpage.contoso.com)。 「Contoso」と入力すると、すべての Contoso 関連サイト (contoso.com、contoso.uk など) が許可または制限されます。  
  
3. 許可または禁止するサイトの一覧から Web アドレスを削除するには、Web アドレスを選択し、 **[削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
[ユーザーデスクトップの管理](manage-user-desktops-using-multipoint-dashboard.md)  
