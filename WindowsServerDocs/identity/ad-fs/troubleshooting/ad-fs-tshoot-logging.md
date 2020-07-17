---
title: AD FS のトラブルシューティング-イベントとログの監査
description: このドキュメントでは、さまざまな AD FS ログを使用して問題をトラブルシューティングする方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e42c5b6d53cd3985fefc2c93ab10b59383a35af0
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950180"
---
# <a name="ad-fs-troubleshooting---events-and-logging"></a>AD FS のトラブルシューティング-イベントとログ
AD FS は、トラブルシューティングで使用できる2つの主要なログを提供します。  以下の説明を参照してください。

- 管理ログ
- トレースログ  
 
これらのログについては、以下で説明します。

## <a name="admin-log"></a>管理ログ
管理ログには、発生している問題に関する概要情報が既定で表示されます。

### <a name="to-view-the-admin-log"></a>管理ログを表示するには
1.  イベント ビューアーを開きます。
2.  **[アプリケーションとサービスログ] を**展開します。
3.  **[AD FS]** を展開します。
4.  **[管理]** をクリックします。

![監査の強化](media/ad-fs-tshoot-logging/event1.PNG)  

## <a name="trace-log"></a>トレース ログ
トレースログは、詳細なメッセージがログに記録される場所であり、トラブルシューティングを行うときに最も役に立つログになります。 トレースログ情報の多くは、システムのパフォーマンスに影響を与える可能性がある短い時間で生成される可能性があるため、既定ではトレースログが無効になっています。 

### <a name="to-enable-and-view-the-trace-log"></a>トレースログを有効にして表示するには
1.  イベント ビューアーを開きます。
2.  **[アプリケーションとサービスログ]** を右クリックし、表示 をクリックして、 **[分析およびデバッグログの表示]** をクリックします。  これにより、左側に追加のノードが表示されます。
![監査の機能強化](media/ad-fs-tshoot-logging/event2.PNG)  
3.  トレースの AD FS 展開
4.  デバッグ を右クリックし、**ログを有効にする** を選択します。
![監査の機能強化](media/ad-fs-tshoot-logging/event3.PNG)  


## <a name="event-auditing-information-for-ad-fs-on-windows-server-2016"></a>Windows Server 2016 での AD FS に関するイベント監査情報  
既定では、Windows Server 2016 の AD FS では、基本レベルの監査が有効になっています。  基本的な監査を使用すると、管理者は1つの要求に対して5つ以下のイベントを表示できます。  これは、1つの要求を表示するために、管理者が確認する必要があるイベントの数が大幅に減少することを示しています。   監査レベルを上げたり下げたりするには、PowerShell cmdlt を使用します。  

```PowerShell
Set-AdfsProperties -AuditLevel 
```

次の表は、使用可能な監査レベルを示しています。  

|監査レベル|PowerShell の構文|説明|  
|----- | ----- | ----- |
|None|Set-adfsproperties-AuditLevel None|監査は無効になり、イベントはログに記録されません。|  
|基本 (既定値)|Set-adfsproperties-AuditLevel Basic|1つの要求に対して記録されるイベントは5件までです|  
|Verbose|Set-adfsproperties-AuditLevel Verbose|すべてのイベントがログに記録されます。  これにより、要求ごとに膨大な量の情報がログに記録されます。|  
  
現在の監査レベルを表示するには、PowerShell の cmdlt: Set-adfsproperties を使用します。  
  
![監査の強化](media/ad-fs-tshoot-logging/ADFS_Audit_1.PNG)  
  
監査レベルは、PowerShell cmdlt: Set-adfsproperties-AuditLevel を使用して発生または減少させることができます。  
  
![監査の強化](media/ad-fs-tshoot-logging/ADFS_Audit_2.png)  
  
## <a name="types-of-events"></a>イベントの種類  
AD FS によって処理されたさまざまな種類の要求に基づいて、AD FS イベントの種類を変えることができます。 各種類のイベントには、特定のデータが関連付けられています。  イベントの種類は、ログイン要求 (つまり、トークン要求) とシステム要求 (構成情報のフェッチを含むサーバーサーバー呼び出し) の間で区別できます。    

次の表は、基本的なイベントの種類を示しています。  
  
|イベントの種類|イベント ID|説明| 
|----- | ----- | ----- | 
|新しい資格情報の検証の成功|1202|フェデレーションサービスによって、新しい資格情報が正常に検証される要求。 これには、WS-TRUST、WS-FEDERATION、SAML-P (SSO を生成する最初のレッグ)、OAuth 承認エンドポイントが含まれます。|  
|新しい資格情報の検証エラー|1203|フェデレーションサービスで新しい資格情報の検証が失敗した要求。 これには、WS-TRUST、WS-ATOMICTRANSACTION、SAML-P (SSO を生成する最初のレッグ)、OAuth 承認エンドポイントが含まれます。|  
|アプリケーショントークンの成功|1200|フェデレーションサービスによってセキュリティトークンが正常に発行される要求。 WS-FEDERATION の場合、これは SSO アーティファクトを使用して要求が処理されるときにログに記録されます。 (SSO cookie など)。|  
|アプリケーショントークンのエラー|1201|フェデレーションサービスでセキュリティトークンの発行に失敗した要求。 WS-FEDERATION の場合、これは SSO アーティファクトを使用して要求が処理されたときにログに記録されます。 (SSO cookie など)。|  
|パスワード変更要求の成功|1204|フェデレーションサービスによってパスワード変更要求が正常に処理されたトランザクション。|  
|パスワード変更要求エラー|1205|フェデレーションサービスによってパスワード変更要求を処理できなかったトランザクション。| 
|サインアウトの成功|1206|正常なサインアウト要求について説明します。|  
|サインアウトエラー|1207|失敗したサインアウト要求について説明します。|  

## <a name="security-auditing"></a>セキュリティ監査
AD FS サービスアカウントのセキュリティ監査では、パスワードの更新、要求/応答のログ、要求のヘッダー、デバイスの登録結果に関する問題を追跡する際に役立つ場合があります。  AD FS サービスアカウントの監査は、既定では無効になっています。

### <a name="to-enable-security-auditing"></a>セキュリティ監査を有効にするには
1. スタート をクリックし、**プログラム**、**管理ツール** の順にポイントして、**ローカルセキュリティポリシー** をクリックします。
2. **"セキュリティの設定\ローカル ポリシー\ユーザー権利の管理"** フォルダーに移動して、 **[セキュリティ監査の生成]** をダブルクリックします。
3. **[ローカル セキュリティの設定]** タブで、AD FS サービス アカウントが表示されていることを確認します。 表示されていない場合は、[ユーザーまたはグループの追加] クリックして一覧に追加し、[OK] をクリックします。
4. 昇格した特権でコマンドプロンプトを開き、次のコマンドを実行して、"アプリケーションが生成されました" または "エラー: 有効/成功: 有効にする" というコマンドを実行します。
5. **ローカルセキュリティポリシー**を閉じ、AD FS 管理スナップインを開きます。
 
AD FS 管理スナップインを開くには、[スタート] をクリックし、[プログラム]、[管理ツール] の順にポイントして、[AD FS の管理] をクリックします。
 
6. [操作] ウィンドウで、[フェデレーションサービスのプロパティの編集] をクリックします。
7. [フェデレーション サービスのプロパティ] ダイアログ ボックスで、[イベント] タブをクリックします。
8. **[成功の監査]** チェック ボックスと **[失敗の監査]** チェック ボックスをオンにします。
9. ［OK］をクリックします。

![監査の強化](media/ad-fs-tshoot-logging/event4.PNG)  
 
>[!NOTE]
>上記の手順は、AD FS がスタンドアロンメンバーサーバーにある場合にのみ使用されます。  ローカルセキュリティポリシーではなく、ドメインコントローラー上で AD FS が実行されている場合は、**グループポリシー管理/フォレスト/ドメイン/ドメインコントローラー**にある**既定のドメインコントローラーポリシー**を使用します。  編集 をクリックし、 **Computer Configuration\Policies\Windows の Rights Management 権利**に移動します。

## <a name="windows-communication-foundation-and-windows-identity-foundation-messages"></a>Windows Communication Foundation と Windows Identity Foundation のメッセージ
トレースログに加えて、問題のトラブルシューティングを行うために、Windows Communication Foundation (WCF) および Windows Identity Foundation (WIF) メッセージの表示が必要になる場合があります。 これを行うには、AD FS サーバー上の**Microsoft サービスの ServiceHost. .config**ファイルを変更します。 

このファイルは **<% システムルート% > \Windows\ADFS**にあり、XML 形式です。 ファイルの関連部分を以下に示します。 
```
<!-- To enable WIF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="Microsoft.IdentityModel" switchValue="Off"> … </source>

<!-- To enable WCF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="System.ServiceModel" switchValue="Off" > … </source>
```


これらの変更を適用した後、構成を保存し、AD FS サービスを再起動します。 適切なスイッチを設定してこれらのトレースを有効にすると、Windows イベントビューアーの AD FS トレースログに表示されます。

## <a name="correlating-events"></a>イベントの関連付け
トラブルシューティングを行う最も難しいことの1つは、大量のエラーまたはデバッグイベントを生成するアクセスの問題です。

この問題を解決するには、管理ログとデバッグログの両方で、イベントビューアーに記録されたすべてのイベントを AD FS 関連付けます。このログは、アクティビティ ID と呼ばれる一意のグローバル一意識別子 (GUID) を使用して、特定の要求に対応します。 この ID は、トークン発行要求が最初に web アプリケーションに提示されたとき (パッシブリクエスタープロファイルを使用するアプリケーションの場合)、または要求プロバイダーに直接送信された要求 (WS-TRUST を使用するアプリケーションの場合) に生成されます。 

![activityid](media/ad-fs-tshoot-logging/activityid1.png)

このアクティビティ ID は、要求の期間全体にわたって同じままで、その要求のイベントビューアーに記録されたすべてのイベントの一部として記録されます。 これは、以下を意味します。
 - このアクティビティ ID を使用してイベントビューアーをフィルター処理または検索すると、トークン要求に対応するすべての関連イベントを追跡するのに役立ちます。
 - 同じアクティビティ ID が異なるコンピューターに記録されます。これにより、フェデレーションサーバープロキシ (FSP) などの複数のコンピューターにわたるユーザー要求のトラブルシューティングを行うことができます。
 - AD FS 要求が何らかの方法で失敗すると、ユーザーのブラウザーにもアクティビティ ID が表示されるため、ユーザーはこの ID をヘルプデスクまたは IT サポートに伝えることができます。

![activityid](media/ad-fs-tshoot-logging/activityid2.png)

トラブルシューティングプロセスを支援するために、AD FS サーバーでトークン発行プロセスが失敗するたびに、AD FS 呼び出し元 ID イベントもログに記録します。 このイベントには、この情報がトークン要求の一部としてフェデレーションサービスに渡されたと仮定した場合の、次のいずれかの要求の種類と値が含まれます。
- https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountnameh
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upnh
- https://schemas.microsoft.com/ws/2008/06/identity/claims/upn
- http://schemas.xmlsoap.org/claims/UPN
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddressh
- https://schemas.microsoft.com/ws/2008/06/identity/claims/emailaddress 
- http://schemas.xmlsoap.org/claims/EmailAddress
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name
- https://schemas.microsoft.com/ws/2008/06/identity/claims/name
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier 

呼び出し元 ID イベントは、アクティビティ ID をログに記録して、特定の要求のイベントログをフィルター処理または検索するためにアクティビティ id を使用できるようにします。




## <a name="next-steps"></a>次のステップ

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)
