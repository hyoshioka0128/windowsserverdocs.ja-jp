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
ms.openlocfilehash: 43a42c211557a41400fada17baaab6a0d5ab822a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866096"
---
# <a name="access-control-policies-in-windows-server-2012-r2-and-windows-server-2012-ad-fs"></a>Windows Server 2012 R2 および Windows Server 2012 の Access Control ポリシー AD FS


この記事で説明するポリシーでは、2種類の要求を使用します。  

1.  要求 AD FS は、AD FS または WAP に直接接続しているクライアントの IP アドレスなど、AD FS および Web アプリケーションプロキシが検査および検証できる情報に基づいて作成されます。  

2.  要求 AD FS は、HTTP ヘッダーとしてクライアントによって AD FS に転送される情報に基づいて作成されます。  

>**重要**: 以下に記載されているポリシーは、次の追加エンドポイントへのアクセスを必要とする Windows 10 ドメイン参加およびサインオンシナリオをブロックします。

Windows 10 のドメイン参加とサインオンに必要な AD FS エンドポイント
- [フェデレーションサービス名]/adfs/services/trust/2005/windowstransport
- [フェデレーションサービス名]/adfs/services/trust/13/windowstransport
- [フェデレーションサービス名]/adfs/services/trust/2005/usernamemixed
- [フェデレーションサービス名]/adfs/services/trust/13/usernamemixed 
- [フェデレーションサービス名]/adfs/services/trust/2005/certificatemixed
- [フェデレーションサービス名]/adfs/services/trust/13/certificatemixed

>**重要**:/adfs/services/trust/2005/windowstransport エンドポイントと/adfs/services/trust/13/windowstransport エンドポイントは、HTTPS で WIA バインドを使用するイントラネットに接続するエンドポイントであるため、イントラネットアクセスに対してのみ有効にする必要があります。 それらをエクストラネットに公開すると、これらのエンドポイントに対する要求によってロックアウトの保護がバイパスされる可能性があります。 これらのエンドポイントは、(エクストラネットから無効になっている) プロキシで無効にして、AD アカウントのロックアウトを保護する必要があります。 

解決するには、エンドポイント要求に基づいて拒否されたすべてのポリシーを更新して、上記のエンドポイントで例外を許可します。

たとえば、次の規則を使用します。

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  

次のように更新されます。

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "(/adfs/ls/)|(/adfs/services/trust/2005/windowstransport)|(/adfs/services/trust/13/windowstransport)|(/adfs/services/trust/2005/usernamemixed)|(/adfs/services/trust/13/usernamemixed)|(/adfs/services/trust/2005/certificatemixed)|(/adfs/services/trust/13/certificatemixed)"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`



> [!NOTE]
>  このカテゴリからの要求は、ネットワークへのアクセスを保護するためのセキュリティポリシーとしてではなく、ビジネスポリシーを実装するためにのみ使用する必要があります。  不正なクライアントが、アクセスを取得する手段として、誤った情報を含むヘッダーを送信する可能性があります。  

この記事で説明されているポリシーは、ユーザー名、パスワード、多要素認証など、他の認証方法で常に使用する必要があります。  

## <a name="client-access-policies-scenarios"></a>クライアントアクセスポリシーのシナリオ  

|**Scenario**|**[説明]**| 
| --- | --- | 
|シナリオ 1:Office 365 への外部アクセスをすべてブロックする|Office 365 は社内ネットワークのすべてのクライアントからアクセスできますが、外部クライアントからの要求は外部クライアントの IP アドレスに基づいて拒否されます。|  
|例 2:Exchange ActiveSync 以外の Office 365 への外部アクセスをすべてブロックする|Office 365 のアクセスは、社内ネットワーク内のすべてのクライアント、および Exchange ActiveSync を使用する外部クライアントデバイス (スマートフォンなど) から許可されます。 Outlook を使用するような他のすべての外部クライアントはブロックされます。|  
|例 3:ブラウザーベースのアプリケーションを除く Office 365 への外部アクセスをすべてブロックする|Outlook Web アクセスや SharePoint Online などのパッシブ (ブラウザーベース) アプリケーションを除き、Office 365 への外部アクセスをブロックします。|  
|シナリオ 4:指定された Active Directory グループを除き、Office 365 への外部アクセスをすべてブロックする|このシナリオは、クライアントアクセスポリシーの展開をテストおよび検証するために使用されます。 1つ以上の Active Directory グループのメンバーに対してのみ、Office 365 への外部アクセスをブロックします。 また、グループのメンバーに対してのみ外部アクセスを提供するためにも使用できます。|  

## <a name="enabling-client-access-policy"></a>クライアントアクセスポリシーを有効にする  
 Windows Server 2012 R2 の AD FS でクライアントアクセスポリシーを有効にするには、Microsoft Office 365 Id プラットフォーム証明書利用者信頼を更新する必要があります。 次のシナリオ例のいずれかを選択して、組織のニーズに最も合った**Microsoft Office 365 Id プラットフォーム**証明書利用者信頼の要求規則を構成します。  

###  <a name="scenario1"></a>シナリオ 1:Office 365 への外部アクセスをすべてブロックする  
 このクライアントアクセスポリシーのシナリオでは、すべての内部クライアントからのアクセスを許可し、外部クライアントの IP アドレスに基づいてすべての外部クライアントをブロックします。 次の手順を使用して、適切な発行承認規則を、選択したシナリオの Office 365 証明書利用者信頼に追加できます。  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365"></a>Office 365 への外部アクセスをすべてブロックするルールを作成するには  

1.  **サーバーマネージャー**で、 **[ツール]** をクリックし、 **[AD FS の管理]** をクリックします。  

2.  コンソールツリーの **[AD Fs\ 信頼関係]** で、 **[証明書利用者信頼]** をクリックし、 **Microsoft Office 365 id プラットフォーム**信頼を右クリックして、 **[要求規則の編集]** をクリックします。  

3.  **[要求規則の編集]** ダイアログボックスで、 **[発行承認規則]** タブを選択し、 **[規則の追加]** をクリックして、要求規則ウィザードを開始します。  

4.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。  

5.  **[規則の構成]** ページの **[要求規則名]** の下に、この規則の表示名を入力します。たとえば、"目的の範囲外の IP 要求がある場合は拒否する" などです。 **[カスタムルール]** で、次の要求規則言語構文を入力するか貼り付けます ("x-y-forward-client-ip" の上の値を有効な ip 式に置き換えます)。  
`c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");` </br>
6.  **[完了]** をクリックします。 [発行承認規則] の一覧に新しい規則が表示されていることを確認してから、[**すべてのユーザーへのアクセスを許可**する] 規則に追加します (拒否規則は、一覧の前に表示されている場合でも優先されます)。  既定の許可アクセス規則がない場合は、次のように要求規則言語を使用して、リストの末尾に1つを追加できます。  </br>

    `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true"); ` 

7.  新しいルールを保存するには、 **[要求規則の編集]** ダイアログボックスで [ **OK]** をクリックします。 結果の一覧は次のようになります。  

     ![発行認証規則](media/Access-Control-Policies-W2K12/clientaccess1.png "ADFS_Client_Access_1")  

###  <a name="scenario2"></a>シナリオ 2:Exchange ActiveSync 以外の Office 365 への外部アクセスをすべてブロックする  
 次の例では、Outlook を含む社内クライアントから、Exchange Online を含むすべての Office 365 アプリケーションにアクセスできるようにします。 クライアントの IP アドレスで示されているように、企業ネットワークの外部に存在するクライアントからのアクセスをブロックします。ただし、スマートフォンなどの Exchange ActiveSync クライアントは除きます。  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-exchange-activesync"></a>Exchange ActiveSync 以外の Office 365 への外部アクセスをすべてブロックするルールを作成するには  

1.  **サーバーマネージャー**で、 **[ツール]** をクリックし、 **[AD FS の管理]** をクリックします。  

2.  コンソールツリーの **[AD Fs\ 信頼関係]** で、 **[証明書利用者信頼]** をクリックし、 **Microsoft Office 365 id プラットフォーム**信頼を右クリックして、 **[要求規則の編集]** をクリックします。  

3.  **[要求規則の編集]** ダイアログボックスで、 **[発行承認規則]** タブを選択し、 **[規則の追加]** をクリックして、要求規則ウィザードを開始します。  

4.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。  

5.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力します。たとえば、"目的の範囲外の IP 要求がある場合は、ipoutsiderange 要求を発行します" と表示されます。 **[カスタムルール]** で、次の要求規則言語構文を入力するか貼り付けます ("x-y-forward-client-ip" の上の値を有効な ip 式に置き換えます)。  

    `c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  **[完了]** をクリックします。 **[発行承認規則]** の一覧に新しい規則が表示されていることを確認します。  

7.  次に、 **[要求規則の編集]** ダイアログボックスの **[発行承認規則]** タブで、 **[規則の追加]** をクリックして、要求規則ウィザードを再び開始します。  

8.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。  

9. **[規則の構成]** ページの **[要求規則名]** の下に、この規則の表示名を入力します。たとえば、"目的の範囲外の IP があり、非 EAS-Ms-chap 要求がある場合、拒否" と表示されます。 **[カスタム規則]** で、次の要求規則言語構文を入力するか貼り付けます。  


~~~
`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value != "Microsoft.Exchange.ActiveSync"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  
~~~

10. **[完了]** をクリックします。 **[発行承認規則]** の一覧に新しい規則が表示されていることを確認します。  

11. 次に、 **[要求規則の編集]** ダイアログボックスの **[発行承認規則]** タブで、 **[規則の追加]** をクリックして、要求規則ウィザードを再び開始します。  

12. **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。  

13. **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力します。たとえば、"アプリケーション要求が存在するかどうかを確認する" などです。 **[カスタム規則]** で、次の要求規則言語構文を入力するか貼り付けます。  

   ```  
   NOT EXISTS([Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"]) => add(Type = "http://custom/xmsapplication", Value = "fail");  
   ```  

14. **[完了]** をクリックします。 **[発行承認規則]** の一覧に新しい規則が表示されていることを確認します。  

15. 次に、 **[要求規則の編集]** ダイアログボックスの **[発行承認規則]** タブで、 **[規則の追加]** をクリックして、要求規則ウィザードを再び開始します。  

16. **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。  

17. **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力します。たとえば、"deny users with ipoutsiderange true and application fail" などです。 **[カスタム規則]** で、次の要求規則言語構文を入力するか貼り付けます。  

`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/xmsapplication", Value == "fail"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`</br>  
18. **[完了]** をクリックします。 新しい規則が前の規則のすぐ下に表示され、[発行承認規則] の一覧の [すべてのユーザーにアクセスを許可する] 規則の前に表示されることを確認します (一覧の前に表示されている場合でも、拒否規則は優先されます)。  </br>既定の許可アクセス規則がない場合は、次のように要求規則言語を使用して、リストの末尾に1つを追加できます。</br></br>      `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`</br></br>
19. 新しいルールを保存するには、**要求規則の編集** ダイアログボックスで OK をクリックします。 結果の一覧は次のようになります。  

    ![発行承認ルール](media/Access-Control-Policies-W2K12/clientaccess2.png )  

###  <a name="scenario3"></a>シナリオ 3:ブラウザーベースのアプリケーションを除く Office 365 への外部アクセスをすべてブロックする  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>ブラウザーベースのアプリケーションを除く Office 365 への外部アクセスをすべてブロックするルールを作成するには  

1.  **サーバーマネージャー**で、 **[ツール]** をクリックし、 **[AD FS の管理]** をクリックします。  

2.  コンソールツリーの **[AD Fs\ 信頼関係]** で、 **[証明書利用者信頼]** をクリックし、 **Microsoft Office 365 id プラットフォーム**信頼を右クリックして、 **[要求規則の編集]** をクリックします。  

3.  **[要求規則の編集]** ダイアログボックスで、 **[発行承認規則]** タブを選択し、 **[規則の追加]** をクリックして、要求規則ウィザードを開始します。  

4.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。  

5.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力します。たとえば、"目的の範囲外の IP 要求がある場合は、ipoutsiderange 要求を発行します" と表示されます。 **[カスタムルール]** で、次の要求規則言語構文を入力するか貼り付けます ("x-y-forward-client-ip" の上の値を有効な ip 式に置き換えます)。  </br>
`c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`   
6.  **[完了]** をクリックします。 **[発行承認規則]** の一覧に新しい規則が表示されていることを確認します。  

7.  次に、 **[要求規則の編集]** ダイアログボックスの **[発行承認規則]** タブで、 **[規則の追加]** をクリックして、要求規則ウィザードを再び開始します。  

8.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。  

9. **[規則の構成]** ページの **[要求規則名]** の下に、この規則の表示名を入力します。たとえば、"目的の範囲外の IP があり、エンドポイントが/Adfs/ls ではない場合、拒否します。" と表示されます。 **[カスタム規則]** で、次の要求規則言語構文を入力するか貼り付けます。  


~~~
`c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  
~~~

10. **[完了]** をクリックします。 [発行承認規則] の一覧に新しい規則が表示されていることを確認してから、[**すべてのユーザーへのアクセスを許可**する] 規則に追加します (拒否規則は、一覧の前に表示されている場合でも優先されます)。  </br></br> 既定の許可アクセス規則がない場合は、次のように要求規則言語を使用して、リストの末尾に1つを追加できます。  

   `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`

11. 新しいルールを保存するには、 **[要求規則の編集]** ダイアログボックスで [ **OK]** をクリックします。 結果の一覧は次のようになります。  

    ![発行](media/Access-Control-Policies-W2K12/clientaccess3.png)  

###  <a name="scenario4"></a>シナリオ 4:指定された Active Directory グループを除き、Office 365 への外部アクセスをすべてブロックする  
 次の例では、IP アドレスに基づいて内部クライアントからのアクセスを有効にします。 これは、指定された Active Directory グループ内の個人を除き、外部クライアント IP アドレスを持つ企業ネットワークの外部にあるクライアントからのアクセスをブロックします。次の手順を使用して、**正しい発行承認規則を**要求規則ウィザードを使用して 365 Id プラットフォーム証明書利用者信頼を Microsoft Office:  

##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a>指定された Active Directory グループを除き、Office 365 への外部アクセスをすべてブロックするルールを作成するには  

1.  **サーバーマネージャー**で、 **[ツール]** をクリックし、 **[AD FS の管理]** をクリックします。  

2.  コンソールツリーの **[AD Fs\ 信頼関係]** で、 **[証明書利用者信頼]** をクリックし、 **Microsoft Office 365 id プラットフォーム**信頼を右クリックして、 **[要求規則の編集]** をクリックします。  

3.  **[要求規則の編集]** ダイアログボックスで、 **[発行承認規則]** タブを選択し、 **[規則の追加]** をクリックして、要求規則ウィザードを開始します。  

4.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。  

5.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力します。たとえば、「必要な範囲外の IP 要求がある場合は、ipoutsiderange 要求を発行します」と入力します。 **[カスタムルール]** で、次の要求規則言語構文を入力するか貼り付けます ("x-y-forward-client-ip" の上の値を有効な ip 式に置き換えます)。  


~~~
`c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] && c2:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  
~~~

6. **[完了]** をクリックします。 **[発行承認規則]** の一覧に新しい規則が表示されていることを確認します。  

7. 次に、 **[要求規則の編集]** ダイアログボックスの **[発行承認規則]** タブで、 **[規則の追加]** をクリックして、要求規則ウィザードを再び開始します。  

8. **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。  

9. **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力します。たとえば、"check group SID" のように指定します。 **[カスタム規則]** で、次の要求規則言語構文を入力するか貼り付けます ("groupsid" は、使用している AD グループの実際の sid に置き換えます)。  

    `NOT EXISTS([Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-100"]) => add(Type = "http://custom/groupsid", Value = "fail");`  

10. **[完了]** をクリックします。 **[発行承認規則]** の一覧に新しい規則が表示されていることを確認します。  

11. 次に、 **[要求規則の編集]** ダイアログボックスの **[発行承認規則]** タブで、 **[規則の追加]** をクリックして、要求規則ウィザードを再び開始します。  

12. **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[カスタム規則を使用して要求を送信]** する を選択し、 **[次へ]** をクリックします。  

13. **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力します。たとえば、"deny users with ipoutsiderange true and groupsid fail" のように指定します。 **[カスタム規則]** で、次の要求規則言語構文を入力するか貼り付けます。  

   `c1:[Type == "http://custom/ipoutsiderange", Value == "true"] && c2:[Type == "http://custom/groupsid", Value == "fail"] => issue(Type = "http://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  

14. **[完了]** をクリックします。 新しい規則が前の規則のすぐ下に表示され、[発行承認規則] の一覧の [すべてのユーザーにアクセスを許可する] 規則の前に表示されることを確認します (一覧の前に表示されている場合でも、拒否規則は優先されます)。  </br></br>既定の許可アクセス規則がない場合は、次のように要求規則言語を使用して、リストの末尾に1つを追加できます。  

   `c:[] => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");`  

15. 新しいルールを保存するには、**要求規則の編集** ダイアログボックスで OK をクリックします。 結果の一覧は次のようになります。  

     ![発行](media/Access-Control-Policies-W2K12/clientaccess4.png)  

##  <a name="buildingip"></a>IP アドレス範囲の作成  
 HTTP ヘッダーは、現在 Exchange Online によってのみ設定されています。これにより、認証要求を AD FS に渡すときにヘッダーが設定されます。 要求の値には、次のいずれかを指定できます。  

> [!NOTE]
>  現在、Exchange Online では IPV6 以外の IPV4 アドレスのみがサポートされています。  

-   1つの IP アドレス:Exchange Online に直接接続されているクライアントの IP アドレス  

> [!NOTE]
> - 企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイス IP アドレスとして表示されます。  
>   -   VPN または Microsoft DirectAccess (DA) によって企業ネットワークに接続されているクライアントは、VPN または DA の構成に応じて、内部の企業クライアントとして、または外部クライアントとして表示されることがあります。  

-   1つ以上の IP アドレス:接続しているクライアントの IP アドレスを Exchange Online が判別できない場合、その値は、HTTP ベースの要求に含めることができ、多くのクライアント、ロードバランサーでサポートされている非標準ヘッダーである、x 転送済みヘッダーの値に基づいて設定されます。そして、市場でのプロキシです。  

> [!NOTE]
> 1. クライアント IP アドレスと、要求を受けた各プロキシのアドレスを示す複数の IP アドレスは、コンマで区切られます。  
>    2. Exchange Online インフラストラクチャに関連する IP アドレスは、一覧に表示されません。  

### <a name="regular-expressions"></a>正規表現  
 IP アドレスの範囲を一致させる必要がある場合は、比較を実行するために正規表現を作成する必要があります。 次の一連の手順では、次のアドレス範囲に一致するような式を作成する方法の例を示します (パブリック IP の範囲に合わせてこれらの例を変更する必要があります)。  

- 192.168.1.1 –192.168.1.25  

- 10.0.0.1 –10.0.0.14  

  まず、1つの IP アドレスに一致する基本的なパターンは次のようになります\\。 \b # #\\#. # #\\#. # # #. # # # \b  

  これを拡張すると、2つの異なる IP アドレスを OR 式と一致させることが\\できます。 \b\\# # #.\\# # #. #&#124;# #.\\# # # \b \b\\# # #.\\# # #. # # #. # # # \b  

  そのため、2つのアドレス (192.168.1.1、10.0.0.1 など) のみを照合する例は、\\次のよう\\になります。 \b192\\.\\\\168 .1 .1 \ b&#124;\b10\\.0 .0. 1 \ b  

  これにより、任意の数のアドレスを入力できるようになります。 アドレスの範囲を許可する必要がある場合 (例: 192.168.1.1 – 192.168.1.25)、一致の文字は \b192\\. 168\\.1\\. ([1-9]&#124;1 [0-9]&#124;2 [0-5]) \b  

  以下の点に注意してください。  

- IP アドレスは、数値ではなく文字列として扱われます。  

- このルールは、\b192\\. 168\\.1\\のように分類されます。  

- これは、192.168.1 から始まる任意の値と一致します。  

- 次の例では、最後の小数点の後のアドレス部分に必要な範囲に一致します。  

  -   ([1-9] は、1-9 で終了するアドレスと一致します  

  -   &#124;1 [0-9] は、10-19 で終わるアドレスと一致します  

  -   &#124;2 [0-5]) は、20-25 で終わるアドレスと一致します  

- かっこは、IP アドレスの他の部分との照合を開始しないように、正しく配置されている必要があることに注意してください。  

- 192ブロックが一致すると、10個のブロックに対して同様の式を\\記述\\でき\\ます。 \b10 .0 .0。 ([1-9]&#124;1 [0-4]) \b  

- これらをまとめると、次の式は、"192.168.1.1 ~ 25" および "10.0.0.1 ~ 14" のすべてのアドレスと一致\\する必要\\が\\あります: \b192. 168 .1. ([1-9]&#124;1 [0-9]&#124;2 [0-5]) \b&#124;\b10\\.0\\.0\\。 ([1-9]&#124;1 [0-4]) \b  

### <a name="testing-the-expression"></a>式のテスト  
 Regex 式は非常に複雑になる可能性があるため、regex 検証ツールを使用することを強くお勧めします。 "オンライン正規表現ビルダー" のインターネット検索を実行すると、サンプルデータに対して式を試すことができる便利なオンラインユーティリティがいくつか用意されています。  

 式をテストするときは、どのようなものを一致させる必要があるかを理解することが重要です。 Exchange online システムは、コンマで区切られた多数の IP アドレスを送信する場合があります。 上記の式は、このに対して機能します。 ただし、regex 式をテストするときは、この点を考慮することが重要です。 たとえば、次のサンプル入力を使用して上記の例を確認できます。  

 192.168.1.1、192.168.1.2、192.169.1.1。 192.168.12.1、192.168.1.10、192.168.1.25、192.168.1.26、192.168.1.30、1192.168.1.20  

 10.0.0.1、10.0.0.5、10.0.0.10、10.0.1.0、10.0.1.1、110.0.0.1、10.0.0.14、10.0.0.15、10.0.0.10、10、0.0.1  

## <a name="claim-types"></a>信頼性情報の種類  
 Windows Server 2012 R2 の AD FS では、次の要求の種類を使用して要求コンテキスト情報を提供します。  

### <a name="x-ms-forwarded-client-ip"></a>X-ミリ秒-クライアント-IP  
 要求の種類:`http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`  

 この AD FS 要求は、要求を行っているユーザー (Outlook クライアントなど) の IP アドレスを突き止めるに "最適な試行" を表します。 この要求には、要求を転送したすべてのプロキシのアドレスを含む、複数の IP アドレスを含めることができます。  この要求は、HTTP から設定されます。 要求の値には、次のいずれかを指定できます。  

-   単一の IP アドレス-Exchange Online に直接接続されているクライアントの IP アドレス  

> [!NOTE]
>  企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイス IP アドレスとして表示されます。  

-   1つ以上の IP アドレス  

    -   接続しているクライアントの IP アドレスを Exchange Online が特定できない場合は、HTTP ベースの要求に含めることができ、多くのクライアント、ロードバランサー、およびでサポートされている非標準ヘッダーの x 転送済みヘッダーの値に基づいて値が設定されます。市場のプロキシ。  

    -   クライアント IP アドレスを示す複数の IP アドレスと、要求に合格した各プロキシのアドレスは、コンマで区切られます。  

> [!NOTE]
>  Exchange Online インフラストラクチャに関連する IP アドレスは、一覧に表示されません。  

> [!WARNING]
>  現在、Exchange Online は IPV4 アドレスのみをサポートしています。IPV6 アドレスはサポートされていません。  

### <a name="x-ms-client-application"></a>X-MS-クライアント-アプリケーション  
 要求の種類:`http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`  

 この AD FS 要求は、エンドクライアントが使用するプロトコルを表します。このプロトコルは、使用されているアプリケーションに対して弱くなります。  この要求は、現在 Exchange Online によって設定されている HTTP ヘッダーから作成されます。これは、認証要求を AD FS に渡すときに、ヘッダーを入力します。 アプリケーションによっては、この要求の値は次のいずれかになります。  

-   Exchange Active Sync を使用するデバイスの場合、値は "Microsoft. Exchange. ActiveSync" になります。  

-   Microsoft Outlook クライアントを使用すると、次のいずれかの値が返される場合があります。  

    -   Microsoft. Exchange. 自動検出  

    -   OfflineAddressBook  

    -   Microsoft. Exchange. Exchange...  

    -   Microsoft. Exchange. Exchange...  

-   このヘッダーには、次のような値を指定できます。  

    -   Microsoft. Exchange. Powershell  

    -   Microsoft. Exchange. SMTP  

    -   Microsoft. Exchange. Pop  

    -   Microsoft. Exchange. Imap  

### <a name="x-ms-client-user-agent"></a>X-MS-クライアント-ユーザーエージェント  
 要求の種類:`http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`  

 この AD FS 要求は、クライアントがサービスにアクセスするために使用しているデバイスの種類を表す文字列を提供します。 これは、特定のデバイス (特定の種類のスマートフォンなど) へのアクセスをユーザーが禁止する場合に使用できます。  この要求の値の例には、以下の値が含まれます (ただし、これらに限定されません)。  

 次に示すのは、x-ms クライアントアプリケーションが "Microsoft. Exchange. ActiveSync" であるクライアントに対して、ユーザーエージェントの値に含まれる可能性のある例です。  

- 渦/1.0  

- IPad1C1/812.1  

- IPhone3C1/811.2  

- Apple iPhone/704.11  

- Moto-DROID2/4.5.1  

- SAMSUNGSPHD700/100.202  

- Android/0.3  

  この値が空である可能性もあります。  

### <a name="x-ms-proxy"></a>X-MS-プロキシ  
 要求の種類:`http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`  

 この AD FS 要求は、要求が Web アプリケーションプロキシを経由して渡されたことを示します。  この要求は、Web アプリケーションプロキシによって作成されます。これにより、バックエンドフェデレーションサービスに認証要求を渡すときにヘッダーが設定されます。 AD FS は、それをクレームに変換します。  

 要求の値は、要求を受けた Web アプリケーションプロキシの DNS 名です。  

### <a name="insidecorporatenetwork"></a>InsideCorporateNetwork  
 要求の種類:`http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`  

 上記のように、この要求の種類は、要求が web アプリケーションプロキシを経由して渡されたかどうかを示します。 Insidecorporatenetwork とは異なり、このブール値は True で、企業ネットワーク内からフェデレーションサービスに直接要求を示します。  

### <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-エンドポイント-絶対パス (アクティブとパッシブ)  
 要求の種類:`http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`  

 この要求の種類を使用して、"アクティブ" (リッチ) クライアントと "パッシブ" (web ブラウザーベース) クライアントからの要求を特定できます。 これにより、Outlook Web アクセス、SharePoint Online、Office 365 ポータルなどのブラウザーベースのアプリケーションからの外部要求が許可されますが、Microsoft Outlook などのリッチクライアントからの要求はブロックされます。  

 要求の値は、要求を受信した AD FS サービスの名前です。  

## <a name="see-also"></a>関連項目  
 [AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
