---
ms.assetid: 5728847d-dcef-4694-9080-d63bfb1fe24b
title: AD FS のアクセス制御ポリシー
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/05/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 13969958c9b4e0539993142d680cb6c34dc10750
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190255"
---
# <a name="access-control-policies-in-windows-server-2012-r2-and-windows-server-2012-ad-fs"></a>Windows Server 2012 R2 および Windows Server 2012 の AD FS でのアクセス制御ポリシー


この記事で説明されているポリシーの要求の 2 種類の使用  
  
1.  要求を AD FS は AD FS と Web アプリケーション プロキシが検査およびことを確認するか、AD FS と WAP に直接接続するクライアントの IP アドレスなどの情報に基づいて作成されます。  
  
2.  AD FS の要求が HTTP ヘッダーとして AD FS にクライアントによって転送される情報に基づいて作成します  
  
>**重要**: 以下に示すように、ポリシーは Windows 10 ドメイン参加をブロックし、次の追加のエンドポイントへのアクセスを必要とするシナリオのサインオン

Windows 10 ドメインに参加し、サインオンに必要な AD FS のエンドポイント
- [フェデレーション サービス名]/adfs/services/信頼/2005/windowstransport
- [フェデレーション サービス名]/adfs/services/信頼/13/windowstransport
- [フェデレーション サービス名]/adfs/services/信頼/2005/usernamemixed
- [フェデレーション サービス名]/adfs/services/信頼/13/usernamemixed 
- [フェデレーション サービス名]/adfs/services/信頼/2005/certificatemixed
- [フェデレーション サービス名]/adfs/services/信頼/13/certificatemixed

を解決するには、上記のエンドポイントは、例外を許可するエンドポイント要求に基づくを拒否するポリシーを更新します。

たとえば、以下の規則:

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  

更新されます。

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "(/adfs/ls/)|(/adfs/services/trust/2005/windowstransport)|(/adfs/services/trust/13/windowstransport)|(/adfs/services/trust/2005/usernamemixed)|(/adfs/services/trust/13/usernamemixed)|(/adfs/services/trust/2005/certificatemixed)|(/adfs/services/trust/13/certificatemixed)"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`



> [!NOTE]
>  このカテゴリからの要求は、ビジネス ポリシーを実装するためにのみ使用する必要があります、ネットワークへのアクセスを保護するセキュリティ ポリシーではなく。  承認されていないクライアントにアクセスする方法として偽の情報でのヘッダーを送信することができます。  
  
この記事で説明されているポリシーは、ユーザー名とパスワード、または多要素認証などの別の認証方法を常に使用する必要があります。  
  
## <a name="client-access-policies-scenarios"></a>クライアント アクセス ポリシーのシナリオ  
  
|**Scenario**|**説明**| 
| --- | --- | 
|シナリオ 1:Office 365 へのすべての外部アクセスをブロックします。|企業内部ネットワーク上のすべてのクライアントから office 365 へのアクセスが許可されているが、外部クライアントの IP アドレスに基づいて外部クライアントからの要求が拒否されました。|  
|例 2:Exchange ActiveSync を除く Office 365 へのすべての外部アクセスをブロックします。|だけでなく、Exchange ActiveSync を使用するスマート フォンなど、任意の外部のクライアント デバイスから企業内部ネットワーク上のすべてのクライアントから office 365 のアクセスが許可されます。 すべての他の外部のクライアント、Outlook を使用しているがブロックされます。|  
|例 3:ブラウザー ベースのアプリケーションを除く Office 365 に対するすべての外部アクセスをブロックします。|ブロックへの外部アクセス、Office 365 Outlook Web Access や SharePoint Online などのパッシブ (ブラウザー ベースの) アプリケーションを除く。|  
|シナリオ 4:指定された Active Directory グループを除く Office 365 に対するすべての外部アクセスをブロックします。|このシナリオは、テストおよびクライアント アクセス ポリシーの展開を検証するために使用されます。 1 つまたは複数の Active Directory グループのメンバーに対してのみ、Office 365 への外部アクセスをブロックします。 グループのメンバーにのみ外部アクセスを提供することにも使用できます。|  
  
## <a name="enabling-client-access-policy"></a>クライアント アクセス ポリシーを有効にします。  
 Windows Server 2012 R2 で AD FS でクライアント アクセス ポリシーを有効にするには、信頼証明書利用者 Microsoft Office 365 Id プラットフォームを更新する必要があります。 要求規則を構成するのには、次のシナリオ例のいずれかを選択、 **Microsoft Office 365 Id プラットフォーム**組織のニーズに最も合った証明書利用者の信頼します。  
  
###  <a name="scenario1"></a> シナリオ 1:Office 365 へのすべての外部アクセスをブロックします。  
 このクライアント アクセス ポリシーのシナリオでは、外部のクライアントの IP アドレスに基づくすべての外部クライアントからすべての内部クライアントおよびブロックへのアクセスを許可します。 次の手順を使用するには、選択したシナリオの信頼証明書利用者、Office 365 に適した発行承認規則を追加します。  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365"></a>Office 365 へのすべての外部アクセスをブロックするルールを作成するには  
  
1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD fs \ 信頼関係**、] をクリックして**証明書利用者信頼**を右クリックし、 **Microsoft Office 365 Id プラットフォーム**信頼、および順にクリックします**要求規則の編集**します。  
  
3.  **要求規則の編集**ダイアログ ボックスで、**発行承認規則の**タブをクリックし、をクリックし、**規則の追加**要求規則のウィザードを開始します。  
  
4.  **規則テンプレートの選択**] ページ [**要求規則テンプレート**を選択します**をカスタム規則を使用して要求を送信**、順にクリックします**次**。  
  
5.  **規則の構成**] ページ [**要求規則名**、例では、この規則の表示名「場合、目的の範囲外の任意の IP 要求拒否」の種類。 **Custom rule**を入力するか、次の要求規則言語構文 ("x-ms-転送-クライアントの ip"IP の有効な式では、その上の値を置き換えてください) を貼り付けます。  
`c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");` </br>
6.  **[Finish]** (完了) をクリックします。 新しい規則が、既定値にする前に発行承認規則の一覧に表示されることを確認します。**にすべてのユーザー アクセスを許可**ルール (拒否規則が優先一覧の前に表示される場合でも)。  既定のアクセス規則の許可がない場合に、次のように、要求規則言語を使用して、一覧の最後に 1 つを追加できます。  </br>
    
    `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true"); ` 

7.  新しい規則を保存する、**要求規則の編集**ダイアログ ボックスで、をクリックして**OK**。 結果のリストは、次のようになります。  
  
     ![発行認証ルール](media/Access-Control-Policies-W2K12/clientaccess1.png "ADFS_Client_Access_1")  
  
###  <a name="scenario2"></a> シナリオ 2:Exchange ActiveSync を除く Office 365 へのすべての外部アクセスをブロックします。  
 次の例では、Outlook を含む内部のクライアントから Exchange Online を含むすべての Office 365 アプリケーションへのアクセスを許可します。 Exchange ActiveSync クライアントのスマート フォンなどを除き、クライアントの IP アドレスで示されている、企業ネットワークの外部に存在するクライアントからのアクセスをブロックします。  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-exchange-activesync"></a>Exchange ActiveSync を除く Office 365 へのすべての外部アクセスをブロックするルールを作成するには  
  
1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD fs \ 信頼関係**、] をクリックして**証明書利用者信頼**を右クリックし、 **Microsoft Office 365 Id プラットフォーム**信頼、および順にクリックします**要求規則の編集**します。  
  
3.  **要求規則の編集**ダイアログ ボックスで、**発行承認規則の**タブをクリックし、をクリックし、**規則の追加**要求規則のウィザードを開始します。  
  
4.  **規則テンプレートの選択**] ページ [**要求規則テンプレート**を選択します**をカスタム規則を使用して要求を送信**、順にクリックします**次**。  
  
5.  **規則の構成**] ページ [**要求規則名**例「、目的の範囲外の任意の IP 要求がある場合の問題を ipoutsiderange 要求」のこの規則の表示名を入力します。 **Custom rule**を入力するか、次の要求規則言語構文 ("x-ms-転送-クライアントの ip"IP の有効な式では、その上の値を置き換えてください) を貼り付けます。  
    
    `c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  **[Finish]** (完了) をクリックします。 新しい規則が表示されることを確認、**発行承認規則の**一覧。  
  
7.  次に、**要求規則の編集**] ダイアログ ボックスの [、**発行承認規則の**] タブで [**規則の追加**要求規則のウィザードをもう一度開始します。  
  
8.  **規則テンプレートの選択**] ページ [**要求規則テンプレート**を選択します**をカスタム規則を使用して要求を送信**、順にクリックします**次**。  
  
9. **規則の構成**] ページ [**要求規則名**型の例では、この規則の表示名"必要な範囲外の IP があるし、非 EAS x ms クライアント アプリケーションの要求がある場合を拒否します。"。 **Custom rule**を入力するか、次の要求規則言語構文貼り付けます。  
  

    `c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value != "Microsoft.Exchange.ActiveSync"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  
  
10. **[Finish]** (完了) をクリックします。 新しい規則が表示されることを確認、**発行承認規則の**一覧。  
  
11. 次に、**要求規則の編集**] ダイアログ ボックスの [、**発行承認規則の**] タブで [**規則の追加**要求規則のウィザードをもう一度開始します。  
  
12. **規則テンプレートの選択**] ページ [**要求規則テンプレートでは、** 選択**カスタム規則を使用して要求を送信する**、順にクリックします **[次へ]** します。  
  
13. **規則の構成**] ページ [**要求規則名**、この規則の表示名を入力、たとえば"アプリケーションの要求の存在をチェック"。 **Custom rule**を入力するか、次の要求規則言語構文貼り付けます。  
  
    ```  
    NOT EXISTS([Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"]) => add(Type = "http://custom/xmsapplication", Value = "fail");  
    ```  
  
14. **[Finish]** (完了) をクリックします。 新しい規則が表示されることを確認、**発行承認規則の**一覧。  
  
15. 次に、**要求規則の編集**] ダイアログ ボックスの [、**発行承認規則の**] タブで [**規則の追加**要求規則のウィザードをもう一度開始します。  
  
16. **規則テンプレートの選択**] ページ [**要求規則テンプレートでは、** 選択**カスタム規則を使用して要求を送信する**、順にクリックします **[次へ]** します。  
  
17. **規則の構成**] ページ [**要求規則名**、この規則の表示名を入力、たとえば「拒否 ipoutsiderange true およびアプリケーションを持つユーザーの失敗」。 **Custom rule**を入力するか、次の要求規則言語構文貼り付けます。  
  
`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/xmsapplication", Value == "fail"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`</br>  
18. **[Finish]** (完了) をクリックします。 以前のルールの下、新しい規則がすぐに表示されますを確認し、(、この拒否規則が優先一覧の前に表示される場合でも) 発行承認規則の一覧でルールを既定値のすべてのユーザーにアクセスを許可する前にします。  </br>既定のアクセス規則の許可がない場合に、次のように、要求規則言語を使用して、一覧の最後に 1 つを追加できます。</br></br>      `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`</br></br>
19. 新しい規則を保存する、**要求規則の編集** ダイアログ ボックスで、ok をクリックします。 結果のリストは、次のようになります。  
  
     ![発行承認ルール](media/Access-Control-Policies-W2K12/clientaccess2.png )  
  
###  <a name="scenario3"></a> シナリオ 3:ブラウザー ベースのアプリケーションを除く Office 365 に対するすべての外部アクセスをブロックします。  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>ブラウザー ベースのアプリケーションを除く Office 365 に対するすべての外部アクセスをブロックするルールを作成するには  
  
1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD fs \ 信頼関係**、] をクリックして**証明書利用者信頼**を右クリックし、 **Microsoft Office 365 Id プラットフォーム**信頼、および順にクリックします**要求規則の編集**します。  
  
3.  **要求規則の編集**ダイアログ ボックスで、**発行承認規則の**タブをクリックし、をクリックし、**規則の追加**要求規則のウィザードを開始します。  
  
4.  **規則テンプレートの選択**] ページ [**要求規則テンプレート**を選択します**をカスタム規則を使用して要求を送信**、順にクリックします**次**。  
  
5.  **規則の構成**] ページ [**要求規則名**例「、目的の範囲外の任意の IP 要求がある場合の問題を ipoutsiderange 要求」のこの規則の表示名を入力します。 **Custom rule**を入力するか、次の要求規則言語構文 ("x-ms-転送-クライアントの ip"IP の有効な式では、その上の値を置き換えてください) を貼り付けます。  </br>
`c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`   
6.  **[Finish]** (完了) をクリックします。 新しい規則が表示されることを確認、**発行承認規則の**一覧。  
  
7.  次に、**要求規則の編集**] ダイアログ ボックスの [、**発行承認規則の**] タブで [**規則の追加**要求規則のウィザードをもう一度開始します。  
  
8.  **規則テンプレートの選択**] ページ [**要求規則テンプレートでは、** 選択**カスタム規則を使用して要求を送信する**、順にクリックします **[次へ]** します。  
  
9. **規則の構成**] ページ [**要求規則名**、例では、この規則の表示名「場合は、必要な範囲を ip アドレスがあるし、エンドポイントがない/adfs/ls、拒否」の種類。 **Custom rule**を入力するか、次の要求規則言語構文貼り付けます。  
  
 
    `c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  
  
10. **[Finish]** (完了) をクリックします。 新しい規則が、既定値にする前に発行承認規則の一覧に表示されることを確認します。**にすべてのユーザー アクセスを許可**ルール (拒否規則が優先一覧の前に表示される場合でも)。  </br></br> 既定のアクセス規則の許可がない場合に、次のように、要求規則言語を使用して、一覧の最後に 1 つを追加できます。  
  
    `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`
  
11. 新しい規則を保存する、**要求規則の編集**ダイアログ ボックスで、をクリックして**OK**。 結果のリストは、次のようになります。  
  
     ![発行](media/Access-Control-Policies-W2K12/clientaccess3.png)  
  
###  <a name="scenario4"></a> シナリオ 4:指定された Active Directory グループを除く Office 365 に対するすべての外部アクセスをブロックします。  
 次の例では、IP アドレスに基づく内部のクライアントからアクセスできるようにします。 企業ネットワークの外部に存在する外部のクライアント IP アドレスを持つクライアントからのアクセスをブロック、指定した Active Directory Group.Use で人を除く、に規則を次の手順に従って、適切な発行の承認を追加します。**Microsoft Office 365 Id プラットフォーム**要求規則のウィザードを使用して証明書利用者の信頼。  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a>Active Directory グループを指定を除き、Office 365 へのすべての外部アクセスをブロックするルールを作成するには  
  
1.  **サーバー マネージャー**、 をクリックして**ツール**、 をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD fs \ 信頼関係**、] をクリックして**証明書利用者信頼**を右クリックし、 **Microsoft Office 365 Id プラットフォーム**信頼、および順にクリックします**要求規則の編集**します。  
  
3.  **要求規則の編集**ダイアログ ボックスで、**発行承認規則の**タブをクリックし、をクリックし、**規則の追加**要求規則のウィザードを開始します。  
  
4.  **規則テンプレートの選択**] ページ [**要求規則テンプレート**を選択します**をカスタム規則を使用して要求を送信**、順にクリックします**次**。  
  
5.  **規則の構成**] ページ [**要求規則名**例「、目的の範囲外の任意の IP 要求がある場合は、要求を発行 ipoutsiderange」には、この規則の表示名を入力。 **Custom rule**を入力するか、次の要求規則言語構文 ("x-ms-転送-クライアントの ip"IP の有効な式では、その上の値を置き換えてください) を貼り付けます。  
  
      
    `c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] && c2:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  **[Finish]** (完了) をクリックします。 新しい規則が表示されることを確認、**発行承認規則の**一覧。  
  
7.  次に、**要求規則の編集**] ダイアログ ボックスの [、**発行承認規則の**] タブで [**規則の追加**要求規則のウィザードをもう一度開始します。  
  
8.  **規則テンプレートの選択**] ページ [**要求規則テンプレートでは、** 選択**カスタム規則を使用して要求を送信する**、順にクリックします **[次へ]** します。  
  
9. **規則の構成**] ページ [**要求規則名**例「グループの SID を確認」、この規則の表示名を入力します。 **Custom rule**を入力するか、次の要求規則言語構文 (置換"groupsid"お使いの AD グループの実際の sid) を貼り付けます。  
   
    `NOT EXISTS([Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-100"]) => add(Type = "http://custom/groupsid", Value = "fail");`  

10. **[Finish]** (完了) をクリックします。 新しい規則が表示されることを確認、**発行承認規則の**一覧。  
  
11. 次に、**要求規則の編集**] ダイアログ ボックスの [、**発行承認規則の**] タブで [**規則の追加**要求規則のウィザードをもう一度開始します。  
  
12. **規則テンプレートの選択**] ページ [**要求規則テンプレートでは、** 選択**カスタム規則を使用して要求を送信する**、順にクリックします **[次へ]** します。  
  
13. **規則の構成**] ページ [**要求規則名**、この規則の表示名を入力、たとえば「拒否 ipoutsiderange true および groupsid を持つユーザーの失敗」。 **Custom rule**を入力するか、次の要求規則言語構文貼り付けます。  
   
    `c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/groupsid", Value == "fail"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  

14. **[Finish]** (完了) をクリックします。 以前のルールの下、新しい規則がすぐに表示されますを確認し、(、この拒否規則が優先一覧の前に表示される場合でも) 発行承認規則の一覧でルールを既定値のすべてのユーザーにアクセスを許可する前にします。  </br></br>既定のアクセス規則の許可がない場合に、次のように、要求規則言語を使用して、一覧の最後に 1 つを追加できます。  
   
    `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`  

15. 新しい規則を保存する、**要求規則の編集** ダイアログ ボックスで、ok をクリックします。 結果のリストは、次のようになります。  
  
     ![発行](media/Access-Control-Policies-W2K12/clientaccess4.png)  
  
##  <a name="buildingip"></a> IP アドレス範囲の式の構築  
 X-ms-転送-クライアントの ip の要求は、AD FS を認証要求を渡すときに、ヘッダーを設定する Exchange Online でのみ設定されている HTTP ヘッダーから設定されます。 要求の値は、次のいずれかにあります。  
  
> [!NOTE]
>  Exchange Online の場合、現在、IPV4 と IPV6 はリッスンしませんアドレスのみをサポートします。  
  
-   1 つの IP アドレス:Exchange Online に直接接続されているクライアントの IP アドレス  
  
> [!NOTE]
>  -   企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイスの IP アドレスとして表示されます。  
> -   企業内部のクライアント、または VPN または DA の構成によっては外部のクライアントとして Microsoft DirectAccess (DA) によって、または VPN で企業ネットワークに接続されているクライアントが表示されます。  
  
-   1 つまたは複数の IP アドレス:接続するクライアントの IP アドレスは、Exchange Online の場合に特定することはできません、x のヘッダー、HTTP ベースの要求に含めることがあり、多くのクライアントでは、ロード バランサーでサポートされている非標準ヘッダーの値に基づいて値が設定されます。市場でのプロキシ。  
  
> [!NOTE]
>  1.  クライアントの IP アドレスと、要求が渡される各プロキシのアドレスを示す、複数の IP アドレスはコンマで区切られます。  
> 2.  Exchange Online のインフラストラクチャに関連する IP アドレスでは、一覧にないです。  
  
### <a name="regular-expressions"></a>正規表現  
 範囲の IP アドレスと一致するときに、比較を実行する正規表現を構築するために必要になります。 次の一連の手順では、次のアドレス範囲 (注、パブリック IP の範囲に一致するようにこれらの例を変更する必要があります) に一致するようにこのような式を作成する方法の例は、指定します。  
  
-   192.168.1.1 – 192.168.1.25  
  
-   10.0.0.1 – 10.0.0.14  
  
 単一の IP アドレスに一致する基本的なパターンが最初に、次に示します: \b###\\. ###\\. ###\\### \b。  
  
 これを拡張するには、照合できる 2 つの異なる IP アドレス、OR 式を次のように: \b###\\. ###\\. ###\\. ### \b&#124;\b###\\. ###\\. ###\\. ### \b  
  
 そのため、2 つのアドレス (192.168.1.1 10.0.0.1 など) に一致するように例があります: \b192\\.168\\.1\\. 1\b&#124;\b10\\.0\\.0\\. 1\b  
  
 これにより、手法を任意の数のアドレスを入力することができます。 アドレスの範囲ができる、たとえば 192.168.1.1 – 192.168.1.25、する必要がありますが、一致する必要があります文字が文字: \b192\\.168\\.1\\(。[1-9]&#124;1 [0-9]&#124;2 [0-5]) \b  
  
 以下の点に注意してください。  
  
-   IP アドレスは、文字列と数ではなくとして扱われます。  
  
-   このルールは次のように分割されます。 \b192\\.168\\.1\\します。  
  
-   これには、192. 168.1 始まる任意の値と一致します。  
  
-   範囲の最後の小数点より後に必要なアドレスの一部を次に一致します。  
  
    -   ([1-9] と一致するアドレス 1-9 で終わる  
  
    -   &#124;[0-9] 1 10 ~ 19 のアドレスと一致します。  
  
    -   &#124;20 ~ 25 で終わる 2[0-5]) と一致するアドレス  
  
-   IP アドレスの他の部分を照合を開始しないように、かっこを正しく配置する必要があることに注意してください。  
  
-   192 のブロックを照合して、10 個のブロックのような式を記述できます \b10\\.0\\.0\\。 (。[1-9]&#124;1 0 ~ 4) \b  
  
-   まとめて配置するには、次の式は「192.168.1.1~25」と「10.0.0.1~14」のすべてのアドレスを一致する必要があります: \b192\\.168\\.1\\(。[1-9]&#124;1 [0-9]&#124;2 [0-5]) \b&#124;\b10\\.0\\.0\\. ([1-9]&#124;1 0 ~ 4) \b  
  
### <a name="testing-the-expression"></a>式のテスト  
 正規表現の式はなる正規表現検証ツールの使用を強くお勧めので非常に複雑です。 「オンライン regex 式ビルダー」のインターネット検索を実行する場合は、サンプル データに対して、式を試用するために、いくつかの優れたオンライン ユーティリティが表示されます。  
  
 式をテストするときに、一致する必要がありますの注意点を理解する必要が。 Exchange online のシステムでは、コンマで区切られた多くの IP アドレスを送信できます。 上記の式は、この機能します。 ただし、これが、正規表現の式をテストするときに、これについて考える重要です。 たとえば、上記の例を確認する入力次のサンプルを使用していずれかの可能性があります。  
  
 192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20  
  
 10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1  
  
## <a name="claim-types"></a>信頼性情報の種類  
 Windows Server 2012 R2 で AD FS は、次の要求の種類を使用して要求コンテキスト情報を提供します。  
  
### <a name="x-ms-forwarded-client-ip"></a>X-MS-転送-クライアントの IP  
 要求の種類。 `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`  
  
 この AD FS の要求は、要求を行うユーザー (たとえば、Outlook クライアント) の IP アドレスを確認するのに「最適な試行」を表します。 この要求は、各要求を転送するプロキシのアドレスなど、複数の IP アドレスを含めることができます。  この要求は、HTTP から設定されます。 要求の値には、次のいずれかを指定できます。  
  
-   単一の IP アドレス - Exchange Online に直接接続されているクライアントの IP アドレス  
  
> [!NOTE]
>  企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイスの IP アドレスとして表示されます。  
  
-   1 つまたは複数の IP アドレス  
  
    -   HTTP ベースで含めることができる非標準ヘッダーを要求し、ロード バランサー、多数のクライアントでサポートされて、x-転送-のヘッダーの値に基づいて値を設定が Exchange Online を判断できない場合、接続するクライアントの IP アドレス、および市場でのプロキシ。  
  
    -   クライアントの IP アドレスと各要求が渡されるプロキシのアドレスを示す複数の IP アドレスはコンマで区切られます。  
  
> [!NOTE]
>  Exchange Online のインフラストラクチャに関連する IP アドレスをリストには表示されません。  
  
> [!WARNING]
>  Exchange Online の IPV4 アドレスのみが現在ではサポートします。IPV6 アドレスはサポートしません。  
  
### <a name="x-ms-client-application"></a>X MS クライアント アプリケーション  
 要求の種類。 `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`  
  
 この AD FS の要求は、使用されているアプリケーションに柔軟に対応する、エンド クライアントによって使用されるプロトコルを表します。  この要求のデータは、現在の HTTP ヘッダーを AD FS を認証要求を渡すときに、ヘッダーを設定する Exchange Online、によってのみ設定します。 アプリケーションによっては、この要求の値は、次のいずれかが指定されます。  
  
-   を Exchange Active Sync を使用するデバイスの場合は、値は、Microsoft.Exchange.ActiveSync です。  
  
-   次の値のいずれかで Microsoft Outlook クライアントの使用があります。  
  
    -   Microsoft.Exchange.Autodiscover  
  
    -   Microsoft.Exchange.OfflineAddressBook  
  
    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  
  
    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  
  
-   このヘッダーに指定できるその他の値を以下に示します。  
  
    -   Microsoft.Exchange.Powershell  
  
    -   Microsoft.Exchange.SMTP  
  
    -   Microsoft.Exchange.Pop  
  
    -   Microsoft.Exchange.Imap  
  
### <a name="x-ms-client-user-agent"></a>X-MS-クライアントのユーザー エージェント  
 要求の種類。 `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`  
  
 この AD FS の要求は、クライアントがサービスへのアクセスを使用してデバイスの種類を表す文字列を提供します。 これは、顧客 (特定の種類のスマート フォン) などの特定のデバイスのアクセスを禁止する場合に使用できます。  この要求の例の値が含まれます (ただしこれらに限定されません) 以下の値。  
  
 X-ms-クライアント アプリケーションは"Microsoft.Exchange.ActiveSync"クライアントの x ms ユーザー エージェント値を含めることがあります内容の例を次に示します  
  
-   渦流形/1.0  
  
-   Apple-iPad1C1/812.1  
  
-   Apple-iPhone3C1/811.2  
  
-   Apple-iPhone/704.11  
  
-   Moto-DROID2/4.5.1  
  
-   SAMSUNGSPHD700/100.202  
  
-   Android/0.3  
  
 この値が空であることもできます。  
  
### <a name="x-ms-proxy"></a>X-MS-プロキシ  
 要求の種類。 `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`  
  
 この AD FS の要求では、Web アプリケーション プロキシ経由の要求が成功したことを示します。  この要求は、ヘッダーをバック エンドのフェデレーション サービスに認証要求を渡すときに読み込まれる Web アプリケーション プロキシによって設定されます。 AD FS では、クレームに、し、変換します。  
  
 要求の値は、要求が渡される Web アプリケーション プロキシの DNS 名です。  
  
### <a name="insidecorporatenetwork"></a>InsideCorporateNetwork  
 要求の種類。 `http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`  
  
 上記の x-ms - プロキシと同様の要求の種類、この要求の種類では、要求が web アプリケーション プロキシを通過するかどうかを示します。 X-ms-プロキシとは異なり insidecorporatenetwork は、True で企業ネットワーク内からフェデレーション サービスに直接要求することを示すブール値です。  
  
### <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-エンドポイントの絶対パス-パス (アクティブまたはパッシブ)  
 要求の種類。 `http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`  
  
 「パッシブ」(web ブラウザー ベース) のクライアントとの「アクティブ」(リッチ) クライアントから送信された要求を決定するため、この要求の種類を使用できます。 これにより、外部からの Outlook Web Access、SharePoint Online、または Office 365 ポータル Microsoft Outlook などのリッチ クライアントからの要求がブロックされている間に許可するなどのブラウザー ベースのアプリケーションから要求できます。  
  
 要求の値は、要求を受信した AD FS サービスの名前です。  
  
## <a name="see-also"></a>関連項目  
 [AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
