---
ms.assetid: 5728847d-dcef-4694-9080-d63bfb1fe24b
title: "AD FS のアクセス制御ポリシー"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0b4549192bc4dab9edf3b2a10421325144ed0cd2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="access-control-policies-in-windows-server-2012-r2-and-windows-server-2012-ad-fs"></a>Windows Server 2012 R2 および Windows Server 2012 AD FS のアクセス制御ポリシー

>適用対象: Windows Server 2012 R2 および Windows Server 2012 

この記事で説明されているポリシーの作成という 2 種類の信頼性情報の使用  
  
1.  AD FS を AD FS と Web アプリケーション プロキシを検査することを確認するか、AD FS と WAP に直接接続するクライアントの IP アドレスなどの情報に基づいて作成を要求します。  
  
2.  AD FS の要求を AD FS に、クライアントによって転送された as HTTP ヘッダー情報に基づいて作成します。  
  
>**重要な**以下に示すようにポリシーは Windows 10 ドメインへの参加をブロックし、次のその他のエンドポイントへのアクセスを必要とするシナリオにサインイン。

Windows 10 ドメインに参加し、サインアウトのために必要な AD FS エンドポイント
- [フェデレーション サービス名]、[ad fs/サービス/信頼/2005/windowstransport
- [フェデレーション サービス名]、[ad fs/サービス/信頼/13/windowstransport
- [フェデレーション サービス名]、[ad fs/サービス/信頼/2005/usernamemixed
- [フェデレーション サービス名]、[ad fs/サービス/信頼/13/usernamemixed 
- [フェデレーション サービス名]、[ad fs/サービス/信頼/2005/certificatemixed
- [フェデレーション サービス名]、[ad fs/サービス/信頼/13/certificatemixed

を解決するのには、上記のエンドポイントの例外を許可するようにエンドポイントの要求に基づくを拒否するポリシーを更新します。

たとえば、下の [ルール:

`c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  

更新されます。

`c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "(/adfs/ls/)|(/adfs/services/trust/2005/windowstransport)|(/adfs/services/trust/13/windowstransport)|(/adfs/services/trust/2005/usernamemixed)|(/adfs/services/trust/13/usernamemixed)|(/adfs/services/trust/2005/certificatemixed)|(/adfs/services/trust/13/certificatemixed)"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`



> [!NOTE]
>  信頼性情報がこのカテゴリは、ビジネス ポリシーの実装にのみ使用する必要があります、ネットワークへのアクセスを保護するセキュリティ ポリシーではなく。  承認されていないクライアントにアクセスする方法として偽りの情報のヘッダーを送信することができます。  
  
この記事で説明されているポリシーは、ユーザー名とパスワード、または多要素認証などの別の認証方法を常に使用する必要があります。  
  
## <a name="client-access-policies-scenarios"></a>クライアント アクセス ポリシーのシナリオ  
  
|**シナリオ**|**説明**| 
| --- | --- | 
|シナリオ 1: Office 365 へのすべての外部アクセスをブロックします。|企業内部ネットワーク上のすべてのクライアントから office 365 のアクセスが許可されているが、外部のクライアントの IP アドレスに基づいて外部のクライアントからの要求が拒否されました。|  
|シナリオ 2: Exchange ActiveSync を除く、Office 365 へのすべての外部アクセスをブロックします。|企業内部ネットワーク上のすべてのクライアントからだけでなく、Exchange ActiveSync を使用するスマート フォンなどの任意の外部のクライアント デバイスから、office 365 のアクセスが許可されます。 その他の外部、すべてのクライアントを利用した Outlook などがブロックされます。|  
|シナリオ 3: Office 365 にブラウザー ベースのアプリケーションを除くのすべての外部アクセス権をブロックします。|ブロック外部へのアクセス、Office 365 パッシブ Outlook Web Access または SharePoint Online などのアプリケーションの (ブラウザー ベースの) を除く。|  
|シナリオ 4: Office 365 に指定された Active Directory グループを除くのすべての外部アクセス権をブロックします。|このシナリオは、テスト、およびクライアントのアクセス ポリシーの展開の検証に使用されます。 1 つまたは複数の Active Directory グループのメンバーに対してのみ、Office 365 への外部アクセスをブロックします。 グループのメンバにのみ、外部アクセスを提供するも使用できます。|  
  
## <a name="enabling-client-access-policy"></a>クライアントのアクセス ポリシーを有効にします。  
 Windows Server 2012 R2 で AD FS でのクライアント アクセス ポリシーを有効にするには、証明書利用者の信頼 Microsoft Office 365 の Id プラットフォームを更新する必要があります。 要求規則を構成するのには、次のシナリオ例のいずれかを選択、 **Microsoft Office 365 の Id プラットフォーム**証明書利用者信頼、組織のニーズに最も合ったします。  
  
###  <a name="scenario1"></a>シナリオ 1: Office 365 へのすべての外部アクセスをブロックします。  
 このクライアントのアクセス ポリシーのシナリオでは、外部クライアントの IP アドレスに基づくすべての外部のクライアントすべての内部クライアントおよびブロックからのアクセスを許可します。 次の手順を使用して、証明書利用者の信頼、選択したシナリオを Office 365 に適切な発行承認規則を追加することができます。  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365"></a>Office 365 へのすべての外部アクセスをブロックする規則を作成するには  
  
1.  **サーバー マネージャー**、] をクリックして**ツール**、] をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで、下にある**AD fs \ 信頼関係**、] をクリックして**証明書利用者信頼**、右クリックし、 **Microsoft Office 365 の Id プラットフォーム**信頼は、クリックして**要求規則の編集**します。  
  
3.  **要求規則の編集**] ダイアログ ボックスで、**発行承認規則**タブをクリックし、をクリックして**規則の追加**要求規則のウィザードを開始します。  
  
4.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**カスタム規則を使用して要求を送信**、] をクリックし、 **[次へ]**します。  
  
5.  **規則の構成**ページで、**要求規則名**、たとえば、この規則の表示名「目的の範囲外の任意の IP 要求がある場合を拒否する」の種類。 **カスタム規則**、入力するか、次の要求規則言語構文 (上の"x-ms-転送-クライアントの ip"に有効な IP 式の値は、置換)) を貼り付けます。  
`c1:[Type == " https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");` </br>
6.  をクリックして**完了**します。 既定値にする前に、発行承認規則の一覧で、新しい規則が表示されていることを確認**すべてのユーザーへのアクセスを許可**ルール (拒否規則が優先リストの前に表示される場合でも)。  既定のアクセス ルールの許可を持っていない場合は、次のように、要求規則言語を使用して、一覧の最後に追加できます。  </br>
    
    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true"); ` 

7.  新しい規則を保存する、**要求規則の編集**ダイアログ ボックスで、をクリックして**OK**します。 結果の一覧は、次のようになります。  
  
     ![発行認証ルール](media/Access-Control-Policies-W2K12/clientaccess1.png "ADFS_Client_Access_1")  
  
###  <a name="scenario2"></a>シナリオ 2: Exchange ActiveSync を除く、Office 365 へのすべての外部アクセスをブロックします。  
 次の例では、Outlook などの内部クライアントから、Exchange Online を含め、すべての Office 365 アプリケーションにアクセスできるようにします。 スマート フォンなどの Exchange ActiveSync クライアントを除き、クライアントの IP アドレスによって示されている、企業のネットワークの外部に存在するクライアントからのアクセスをブロックします。  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-exchange-activesync"></a>Exchange active Sync を除く、Office 365 へのすべての外部アクセスをブロックする規則を作成するには  
  
1.  **サーバー マネージャー**、] をクリックして**ツール**、] をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで、下にある**AD fs \ 信頼関係**、] をクリックして**証明書利用者信頼**、右クリックし、 **Microsoft Office 365 の Id プラットフォーム**信頼は、クリックして**要求規則の編集**します。  
  
3.  **要求規則の編集**] ダイアログ ボックスで、**発行承認規則**タブをクリックし、をクリックして**規則の追加**要求規則のウィザードを開始します。  
  
4.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**カスタム規則を使用して要求を送信**、] をクリックし、 **[次へ]**します。  
  
5.  **規則の構成**ページで、**要求規則名**、例「目的の範囲外の任意の IP 要求がある場合は、要求を発行 ipoutsiderange」のこの規則の表示名を入力します。 **カスタム規則**、入力するか、次の要求規則言語構文 (上の"x-ms-転送-クライアントの ip"に有効な IP 式の値は、置換)) を貼り付けます。  
    
    `c1:[Type == " https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  をクリックして**完了**します。 新しい規則が表示されていることを確認、**発行承認規則**一覧します。  
  
7.  次に、**要求規則の編集**] ダイアログ ボックスで、**発行承認規則**] タブで、をクリックして**規則の追加**をもう一度要求規則のウィザードを開始します。  
  
8.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**カスタム規則を使用して要求を送信**、] をクリックし、 **[次へ]**します。  
  
9. **規則の構成**ページで、**要求規則名**、たとえば、この規則の表示名「ip が必要な範囲外と非 EAS x ms クライアント アプリケーションの信頼性情報がある場合を拒否する」の種類。 **カスタム規則**、入力するか、次の要求規則言語構文を貼り付けます。  
  

    `c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value != "Microsoft.Exchange.ActiveSync"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  
  
10. をクリックして**完了**します。 新しい規則が表示されていることを確認、**発行承認規則**一覧します。  
  
11. 次に、**要求規則の編集**] ダイアログ ボックスで、**発行承認規則**] タブで、をクリックして**規則の追加**をもう一度要求規則のウィザードを開始します。  
  
12. **規則テンプレートの選択**ページで、**要求規則テンプレート、**選択**カスタム規則を使用して要求を送信**、] をクリックし、 **[次へ]**します。  
  
13. **規則の構成**ページで、**要求規則名**たとえば「チェック アプリケーション要求が存在するかどうかは」、この規則の表示名を入力します。 **カスタム規則**、入力するか、次の要求規則言語構文を貼り付けます。  
  
    ```  
    NOT EXISTS([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"]) => add(Type = "http://custom/xmsapplication", Value = "fail");  
    ```  
  
14. をクリックして**完了**します。 新しい規則が表示されていることを確認、**発行承認規則**一覧します。  
  
15. 次に、**要求規則の編集**] ダイアログ ボックスで、**発行承認規則**] タブで、をクリックして**規則の追加**をもう一度要求規則のウィザードを開始します。  
  
16. **規則テンプレートの選択**ページで、**要求規則テンプレート、**選択**カスタム規則を使用して要求を送信**、] をクリックし、 **[次へ]**します。  
  
17. **規則の構成**ページで、**要求規則名**たとえば「拒否 ipoutsiderange true とアプリケーションを持つユーザーは失敗」、この規則の表示名を入力します。 **カスタム規則**、入力するか、次の要求規則言語構文を貼り付けます。  
  
`c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://custom/xmsapplication", Value == "fail"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`</br>  
18. をクリックして**完了**します。 新しい規則が表示されているすぐに前のルールの下を確認し、前に、既定のすべてのユーザーへのアクセスを許可する規則の (拒否規則が優先リストの前に表示される場合でも) 発行承認規則の一覧にします。  </br>既定のアクセス ルールの許可を持っていない場合は、次のように、要求規則言語を使用して、一覧の最後に追加できます。</br></br>      `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`</br></br>
19. 新しい規則を保存する、**要求規則の編集**] ダイアログ ボックスで、[ok] をクリックします。 結果の一覧は、次のようになります。  
  
     ![発行承認規則](media/Access-Control-Policies-W2K12/clientaccess2.png )  
  
###  <a name="scenario3"></a>シナリオ 3: Office 365 にブラウザー ベースのアプリケーションを除くのすべての外部アクセス権をブロックします。  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>Office 365 にブラウザー ベースのアプリケーションを除くのすべての外部アクセス権をブロックする規則を作成するには  
  
1.  **サーバー マネージャー**、] をクリックして**ツール**、] をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで、下にある**AD fs \ 信頼関係**、] をクリックして**証明書利用者信頼**、右クリックし、 **Microsoft Office 365 の Id プラットフォーム**信頼は、クリックして**要求規則の編集**します。  
  
3.  **要求規則の編集**] ダイアログ ボックスで、**発行承認規則**タブをクリックし、をクリックして**規則の追加**要求規則のウィザードを開始します。  
  
4.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**カスタム規則を使用して要求を送信**、] をクリックし、 **[次へ]**します。  
  
5.  **規則の構成**ページで、**要求規則名**、例「目的の範囲外の任意の IP 要求がある場合は、要求を発行 ipoutsiderange」のこの規則の表示名を入力します。 **カスタム規則**、入力するか、次の要求規則言語構文 (上の"x-ms-転送-クライアントの ip"に有効な IP 式の値は、置換)) を貼り付けます。  </br>
`c1:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`   
6.  をクリックして**完了**します。 新しい規則が表示されていることを確認、**発行承認規則**一覧します。  
  
7.  次に、**要求規則の編集**] ダイアログ ボックスで、**発行承認規則**] タブで、をクリックして**規則の追加**をもう一度要求規則のウィザードを開始します。  
  
8.  **規則テンプレートの選択**ページで、**要求規則テンプレート、**選択**カスタム規則を使用して要求を送信**、] をクリックし、 **[次へ]**します。  
  
9. **規則の構成**ページで、**要求規則名**、例では、この規則の表示名「必要な範囲外 IP があるし、エンドポイントが/adfs/ls、拒否する」の種類。 **カスタム規則**、入力するか、次の要求規則言語構文を貼り付けます。  
  
 
    `c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  
  
10. をクリックして**完了**します。 既定値にする前に、発行承認規則の一覧で、新しい規則が表示されていることを確認**すべてのユーザーへのアクセスを許可**ルール (拒否規則が優先リストの前に表示される場合でも)。  </br></br> 既定のアクセス ルールの許可を持っていない場合は、次のように、要求規則言語を使用して、一覧の最後に追加できます。  
  
    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`
  
11. 新しい規則を保存する、**要求規則の編集**ダイアログ ボックスで、をクリックして**OK**します。 結果の一覧は、次のようになります。  
  
     ![発行](media/Access-Control-Policies-W2K12/clientaccess3.png)  
  
###  <a name="scenario4"></a>シナリオ 4: Office 365 に指定された Active Directory グループを除くのすべての外部アクセス権をブロックします。  
 次の例では、IP アドレスに基づく内部クライアントからアクセスできるようにします。 外部のクライアント IP アドレスを持っている、企業ネットワークの外部に存在するクライアントからのアクセスがブロック、指定した Active Directory Group.Use でユーザーを除く、次の手順を正しく発行承認規則を追加する、 **Microsoft Office 365 の Id プラットフォーム**証明書利用者信頼の要求規則のウィザードを使用します。  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a>Active Directory グループを指定を除く、Office 365 へのすべての外部アクセスをブロックする規則を作成するには  
  
1.  **サーバー マネージャー**、] をクリックして**ツール**、] をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで、下にある**AD fs \ 信頼関係**、] をクリックして**証明書利用者信頼**、右クリックし、 **Microsoft Office 365 の Id プラットフォーム**信頼は、クリックして**要求規則の編集**します。  
  
3.  **要求規則の編集**] ダイアログ ボックスで、**発行承認規則**タブをクリックし、をクリックして**規則の追加**要求規則のウィザードを開始します。  
  
4.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**カスタム規則を使用して要求を送信**、] をクリックし、 **[次へ]**します。  
  
5.  **規則の構成**ページで、**要求規則名**、例「目的の範囲外の任意の IP 要求がある場合は、要求を発行 ipoutsiderange」のこの規則の表示名を入力。 **カスタム規則**、入力するか、次の要求規則言語構文 (上の"x-ms-転送-クライアントの ip"に有効な IP 式の値は、置換)) を貼り付けます。  
  
      
    `c1:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] && c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  をクリックして**完了**します。 新しい規則が表示されていることを確認、**発行承認規則**一覧します。  
  
7.  次に、**要求規則の編集**] ダイアログ ボックスで、**発行承認規則**] タブで、をクリックして**規則の追加**をもう一度要求規則のウィザードを開始します。  
  
8.  **規則テンプレートの選択**ページで、**要求規則テンプレート、**選択**カスタム規則を使用して要求を送信**、] をクリックし、 **[次へ]**します。  
  
9. **規則の構成**ページで、**要求規則名**たとえば「グループ SID の確認」、この規則の表示名を入力します。 **カスタム規則**、入力するか、次の要求規則言語構文 (置換"groupsid"を使用する AD グループの実際の SID を持つ) を貼り付けます。  
   
    `NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-100"]) => add(Type = "http://custom/groupsid", Value = "fail");`  

10. をクリックして**完了**します。 新しい規則が表示されていることを確認、**発行承認規則**一覧します。  
  
11. 次に、**要求規則の編集**] ダイアログ ボックスで、**発行承認規則**] タブで、をクリックして**規則の追加**をもう一度要求規則のウィザードを開始します。  
  
12. **規則テンプレートの選択**ページで、**要求規則テンプレート、**選択**カスタム規則を使用して要求を送信**、] をクリックし、 **[次へ]**します。  
  
13. **規則の構成**ページで、**要求規則名**たとえば「拒否 ipoutsiderange true および groupsid を持つユーザーは失敗」、この規則の表示名を入力します。 **カスタム規則**、入力するか、次の要求規則言語構文を貼り付けます。  
   
    `c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://custom/groupsid", Value == "fail"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  

14. をクリックして**完了**します。 新しい規則が表示されているすぐに前のルールの下を確認し、前に、既定のすべてのユーザーへのアクセスを許可する規則の (拒否規則が優先リストの前に表示される場合でも) 発行承認規則の一覧にします。  </br></br>既定のアクセス ルールの許可を持っていない場合は、次のように、要求規則言語を使用して、一覧の最後に追加できます。  
   
    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`  

15. 新しい規則を保存する、**要求規則の編集**] ダイアログ ボックスで、[ok] をクリックします。 結果の一覧は、次のようになります。  
  
     ![発行](media/Access-Control-Policies-W2K12/clientaccess4.png)  
  
##  <a name="buildingip"></a>IP アドレスの範囲の式の作成  
 X-ms-転送-クライアントの ip アドレスの要求は、HTTP ヘッダー、認証要求を AD FS を渡す際に、ヘッダーを設定する Exchange Online、によってのみ現在設定されているから入力されます。 要求の値は、次のいずれかにあります。  
  
> [!NOTE]
>  Exchange Online の場合、現在、IPV4 と IPV6 ではないアドレスのみをサポートします。  
  
-   単一の IP アドレス: Exchange Online に直接接続されているクライアントの IP アドレス  
  
> [!NOTE]
>  -   企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイスの IP アドレスとして表示されます。  
> -   VPN または Microsoft DirectAccess (DA) によって、企業ネットワークに接続されているクライアントが企業内部のクライアント、または VPN または DA の構成によっては外部のクライアントとして表示可能性があります。  
  
-   1 つまたは複数の IP アドレス: ときに Exchange Online は接続中のクライアントの IP アドレスを調べることはできません、x-転送-のヘッダーの HTTP ベースの要求に含めることがあり、多くのクライアント、ロード バランサー、および市場でのプロキシでサポートされている標準的でないヘッダーの値に基づいた値が設定されます。  
  
> [!NOTE]
>  1.  クライアントの IP アドレスと、要求が渡される各プロキシのアドレスを示す、複数の IP アドレスが、コンマで区切られます。  
> 2.  Exchange Online のインフラストラクチャに関連する IP アドレスは、一覧にないされます。  
  
### <a name="regular-expressions"></a>正規表現  
 範囲の IP アドレスに一致するときに、正規表現の比較を実行するに必要になります。 次の一連の手順では、アドレスの範囲 (パブリック IP の範囲を一致するようにこれらの例を変更する必要があるに注意してください) と一致するような式を作成する方法の例は、指定します。  
  
-   192.168.1.1 – 192.168.1.25  
  
-   10.0.0.1 – 10.0.0.14  
  
 最初に、単一の IP アドレスが一致する基本的なパターンは、次のように: \b###\\.###\\.###\\.###\b  
  
 これを拡張するには、マッチさせる 2 つの異なる IP アドレスまたは式を次のように: \b###\\.###\\.###\\.###\b & #124;\b###\\.###\\.###\\.###\b  
  
 そのため、2 つのアドレス (192.168.1.1 10.0.0.1 など) に一致する例があります: \b192\\.168\\.1\\.1\b & #124;\b10\\.0\\.0\\.1\b  
  
 これにより、手法を任意の数のアドレスを入力することができます。 アドレスの範囲が使用できるように、例 192.168.1.1 – 192.168.1.25、する必要がありますが、一致する行う必要があります文字で文字: \b192\\.168\\.1\\ します。([1-9] (& a) #124; 1 [0-9] & #124; 2 0 ~ 5) \b  
  
 次に注意してください。  
  
-   IP アドレスは、文字列と番号ではないと見なされます。  
  
-   このルールは次のように分けられます。 \b192\\.168\\.1\\ します。  
  
-   これには、任意の値から始まる 192.168.1 と一致します。  
  
-   次に、最終的な小数点後アドレスの部分に必要な範囲と一致します。  
  
    -   ([1-9] と一致するアドレス 1-9 で終わる  
  
    -   (& a) #124 文字です 1 [0-9] 10 ~ 19 で終わるアドレスと一致する。  
  
    -   & 20 ~ 25 で終わる #124;2[0-5]) と一致するアドレス  
  
-   IP アドレスの他の部分を照合を開始しないように、かっこを正しく配置する必要があることに注意してください。  
  
-   マッチング 192 ブロックは、10 個のブロックのような式を記述できます: \b10\\.0\\.0\\ します。([1-9] (& a) #124 文字です 1 0 ~ 4) \b。  
  
-   一緒に配置するには、次の式が一致している「192.168.1.1~25」および「10.0.0.1~14」のすべてのアドレスと: \b192\\.168\\.1\\ します。([1-9] & #124; 1 [0-9] & #124; 2 0 ~ 5) \b & #124;\b10\\.0\\.0\\ します。([1-9] (& a) #124 文字です 1 0 ~ 4) \b。  
  
### <a name="testing-the-expression"></a>式のテスト  
 正規表現の式を強くお勧め regex 検証ツールを使用するように非常に難しい場合になります。 「オンライン regex 式」でインターネットを検索する場合は、サンプル データに対して、式を試すことができるいくつかの優れたオンライン ユーティリティが表示されます。  
  
 式をテストする場合に一致する必要があることを期待できることを理解することが重要です。 Exchange のオンライン システムでは、コンマで区切って、多くの IP アドレスを送信できます。 上記の式は、この動作します。 ただし、これが、正規表現をテストするときに、これについて考えること重要です。 たとえば、上記の例を確認する入力次の例を使用していずれかの可能性があります。  
  
 192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20  
  
 10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1  
  
## <a name="claim-types"></a>要求の種類  
 Windows Server 2012 R2 の AD FS では、次の要求の種類を使用して要求のコンテキスト情報を提供します。  
  
### <a name="x-ms-forwarded-client-ip"></a>X-MS-転送-クライアントの ip アドレス  
 要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`  
  
 この AD FS のクレームでは、要求を行っているユーザー (たとえば、Outlook クライアント) の IP アドレスを突き止めるで「ベスト試行」を表します。 この要求の要求を転送するすべてのプロキシ アドレスなど、複数の IP アドレスを含めることができます。  この要求は、HTTP から入力されます。 要求の値には、次のいずれかを指定できます。  
  
-   単一の IP アドレス - Exchange Online に直接接続されているクライアントの IP アドレス  
  
> [!NOTE]
>  企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイスの IP アドレスとして表示されます。  
  
-   1 つまたは複数の IP アドレス  
  
    -   Exchange Online を判断できない場合、接続するクライアントの IP アドレス、HTTP ベースに含めることが標準でないヘッダーを要求し、多くのクライアント、ロード バランサー、および市場でのプロキシでは、x-転送-のヘッダーの値に基づいた値に設定されます。  
  
    -   クライアントの IP アドレスとの要求が渡される各プロキシ アドレスを示す複数の IP アドレスは、コンマで区切るされます。  
  
> [!NOTE]
>  Exchange Online のインフラストラクチャに関連する IP アドレスは、リスト内に存在できません。  
  
> [!WARNING]
>  Exchange Online 現在サポートされている IPV4 アドレスだけです。IPV6 アドレスはサポートされません。  
  
### <a name="x-ms-client-application"></a>X MS クライアント アプリケーション  
 要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`  
  
 この AD FS のクレームでは、使用されているアプリケーションを柔軟に対応する終了クライアントによって使用されるプロトコルを表します。  この要求は、現在の HTTP ヘッダーから入力される認証要求を AD FS を渡す際に、ヘッダーをあらかじめ設定 Exchange Online、によってのみ設定します。 アプリケーションに応じて、この要求の値は、次のいずれかになります。  
  
-   を Exchange Active Sync を使用するデバイスの場合は、値は、Microsoft.Exchange.ActiveSync です。  
  
-   次の値のいずれかで Microsoft Outlook クライアントの使用があります。  
  
    -   Microsoft.Exchange.Autodiscover  
  
    -   Microsoft.Exchange.OfflineAddressBook  
  
    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  
  
    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  
  
-   このヘッダーで使用できるその他の値は次のとおりです。  
  
    -   Microsoft.Exchange.Powershell  
  
    -   Microsoft.Exchange.SMTP  
  
    -   Microsoft.Exchange.Pop  
  
    -   Microsoft.Exchange.Imap  
  
### <a name="x-ms-client-user-agent"></a>X-MS-クライアントのユーザー エージェント  
 要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`  
  
 この AD FS のクレームでは、サービスにアクセスするクライアントが使用しているデバイスの種類を表す文字列を提供します。 これは、特定のデバイス (スマート フォンの特定の種類) などのアクセスを防ぐを作成するときに使用できます。  この要求の値の例が含まれます (ただし、これらに限定されません) 以下の値。  
  
 X-ms-クライアント-アプリケーションが"Microsoft.Exchange.ActiveSync"は、クライアントを含む可能性のある x ms ユーザー エージェント値の例を示します  
  
-   Vortex/1.0  
  
-   Apple-iPad1C1/812.1  
  
-   Apple-iPhone3C1/811.2  
  
-   Apple-iPhone/704.11  
  
-   Moto-DROID2/4.5.1  
  
-   SAMSUNGSPHD700/100.202  
  
-   Android/0.3  
  
 この値が空であることもできます。  
  
### <a name="x-ms-proxy"></a>X-MS-プロキシ  
 要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`  
  
 この AD FS のクレームでは、Web アプリケーション プロキシ経由の要求が渡されることを示します。  この要求は、Web アプリケーション プロキシは、バック エンドのフェデレーション サービスを認証要求を渡す際に、ヘッダーを設定して設定されます。 AD FS に変換を要求します。  
  
 要求の値は、要求が渡される Web アプリケーション プロキシの DNS 名です。  
  
### <a name="insidecorporatenetwork"></a>InsideCorporateNetwork  
 要求の種類。 `https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`  
  
 上記 x-ms-プロキシと同様の要求の種類、この要求の種類は、web アプリケーション プロキシは、要求に渡されたかどうかを示します。 X ms-プロキシ insidecorporatenetwork は True で企業ネットワーク内からフェデレーション サービスに直接要求することを示すブール値。  
  
### <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-エンドポイントの絶対パスのパス (アクティブまたはパッシブ)  
 要求の種類。 `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`  
  
 (Web ブラウザー ベース) クライアントを「パッシブ」と"active"(リッチ) クライアントから送信された要求を判別するため、この要求の種類を使用できます。 これにより、Outlook Web Access、SharePoint Online、または Office 365 ポータル Microsoft Outlook などのリッチ クライアントから送信された要求がブロックされている間に許可するなどのブラウザー ベースのアプリケーションからの要求を外部できます。  
  
 要求の値は、要求を受信した AD FS サービスの名前です。  
  
## <a name="see-also"></a>参照してください。  
 [AD FS の操作](../../ad-fs/AD-FS-2016-Operations.md)
