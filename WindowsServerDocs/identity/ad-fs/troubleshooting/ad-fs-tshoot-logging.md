---
title: AD FS のトラブルシューティング - イベントの監査とログ記録
description: このドキュメントは、さまざまな AD FS ログを使用して問題をトラブルシューティングする方法を説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 20e2d0747b98e7c7728230d0768506261f5b0d50
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825123"
---
# <a name="ad-fs-troubleshooting---events-and-logging"></a>AD FS のトラブルシューティング - イベントとログ記録
AD FS では、トラブルシューティングに使用できる 2 つのプライマリ ログを提供します。  それらは以下のとおりです。

- 管理者のログイン
- トレース ログ  
 
これらのログは、以下をについてはします。

## <a name="admin-log"></a>管理者のログイン
管理者のログインは、問題が発生していると、既定で有効にする高レベルの情報を提供します。

### <a name="to-view-the-admin-log"></a>管理ログを表示するには
1.  イベント ビューアーを開きます。
2.  展開**アプリケーションとサービス ログ**します。
3.  展開**AD FS**します。
4.  をクリックして**管理者**します。

![audit の機能強化](media/ad-fs-tshoot-logging/event1.PNG)  

## <a name="trace-log"></a>トレース ログ
トレース ログは、詳細なメッセージがログに記録し、トラブルシューティングを行うときに、最も役に立つログになります。 システムのパフォーマンスに影響を与えることができます、時間の短時間で、多くのトレース ログ情報を生成できるため、トレース ログは既定で無効にします。 

### <a name="to-enable-and-view-the-trace-log"></a>有効にし、トレース ログの表示
1.  イベント ビューアーを開きます。
2.  右クリックして**アプリケーションとサービス ログ**ビューを選択し、をクリックして**分析およびデバッグ ログ**します。  これにより、左の他のノードが表示されます。
![audit の機能強化](media/ad-fs-tshoot-logging/event2.PNG)  
3.  AD FS トレースを展開します。
4.  デバッグ構成と選択を右クリックして**ログの有効化**します。
![audit の機能強化](media/ad-fs-tshoot-logging/event3.PNG)  


## <a name="event-auditing-information-for-ad-fs-on-windows-server-2016"></a>Windows Server 2016 で AD FS のイベントの監査情報  
既定では、Windows Server 2016 での AD FS は、基本的なレベルの監査が有効では。  基本的な監査では、管理者は 1 つの要求の 5 個以下のイベントに表示されます。  これは、管理者が参照、1 つの要求を表示するにはイベントの数が大幅に低下をマークします。   監査レベルが発生するまたは PowerShell コマンドレットを使用します。  

```PowerShell
Set-AdfsProperties -AuditLevel 
```

次の表では、利用可能な監査レベルについて説明します。  

|監査レベル|PowerShell の構文|説明|  
|----- | ----- | ----- |
|なし|Set-adfsproperties - AuditLevel なし|監査が無効になっているし、イベントは記録されません。|  
|Basic (既定値)|Set-adfsproperties - AuditLevel Basic|1 つの要求の 5 つ以上のイベントが記録されます。|  
|Verbose|Set-adfsproperties - AuditLevel 詳細|すべてのイベントが記録されます。  これにより、大量の要求ごとの情報が記録されます。|  
  
現在の監査レベルを表示するには、PowerShell コマンドレットを使用できます。Get-adfsproperties します。  
  
![audit の機能強化](media/ad-fs-tshoot-logging/ADFS_Audit_1.PNG)  
  
監査レベルが発生するまたは PowerShell コマンドレットを使用します。Set-adfsproperties-AuditLevel します。  
  
![audit の機能強化](media/ad-fs-tshoot-logging/ADFS_Audit_2.png)  
  
## <a name="types-of-events"></a>イベントの種類  
AD FS イベントには、AD FS によって処理された要求の種類に基づいて、さまざまな種類を指定できます。 イベントのそれぞれの種類では、関連付けられている特定のデータを持ちます。  イベントの種類は、システムの要求 (サーバーの呼び出しの構成情報のフェッチなど) と、ログイン要求 (つまりトークン要求) の間で区別できます。    

次の表では、基本的な種類のイベントについて説明します。  
  
|イベントの種類|イベント ID|説明| 
|----- | ----- | ----- | 
|新しい資格情報の検証の成功|1202|場所、新しい資格情報は、フェデレーション サービスによって正常に検証の要求です。 これには、Ws-trust、Ws-federation、SAML-p が含まれます (SSO を生成する最初の段階) と OAuth 承認エンドポイント。|  
|新しい資格情報の検証エラー|1203|フェデレーション サービスで新しい資格情報の検証が失敗した場所の要求です。 Ws-trust、これが含まれています、Ws-fed、SAML P (SSO を生成する最初の段階) と OAuth 承認エンドポイント。|  
|アプリケーション トークンの成功率|1200|セキュリティ トークンが正常にフェデレーション サービスによってに発行された場所の要求です。 Ws-federation、SAML P SSO アーティファクトを要求が処理されるときに記録されます。 (、SSO cookie など)。|  
|アプリケーション トークンのエラー|1201|フェデレーション サービスでセキュリティ トークンの発行要求が失敗しました。 Ws-federation、SAML P SSO アーティファクトを要求の処理時に記録されます。 (、SSO cookie など)。|  
|パスワード変更要求の成功|1204|パスワード変更要求、トランザクションが、フェデレーション サービスによって正常に処理します。|  
|パスワードの変更要求エラー|1205|フェデレーション サービスによって処理されるパスワードの変更要求、トランザクションが失敗しました。| 
|成功をサインアウトします。|1206|サインアウト要求が成功した場合について説明します。|  
|サインインに失敗しました|1207|サインアウト要求の失敗について説明します。|  

## <a name="security-auditing"></a>セキュリティ監査
AD FS サービス アカウントのセキュリティの監査もパスワードの更新、要求/応答のログ記録、接続の要求ヘッダーおよびデバイス登録の結果に関する問題を追跡に役立ちます。  既定では、AD FS サービス アカウントの監査を無効になっています。

### <a name="to-enable-security-auditing"></a>セキュリティ監査を有効にするには
1.       スタート、 をポイント**プログラム**、 をポイント**管理ツール**、 をクリックし、**ローカル セキュリティ ポリシー**します。
2.        **"セキュリティの設定\ローカル ポリシー\ユーザー権利の管理"** フォルダーに移動して、**[セキュリティ監査の生成]** をダブルクリックします。
3.       **ローカル セキュリティ設定** タブで、AD FS サービス アカウントが表示されていることを確認します。 存在しない場合は、追加のユーザーまたはグループをクリックし、一覧に追加しし、[ok] をクリックします。
4。       昇格した特権でコマンド プロンプトを開き、有効監査 auditpol.exe/set/subcategory に次のコマンドを実行します:"Application Generated"/failure:enable/success:enable 5。       閉じる**ローカル セキュリティ ポリシー**、AD FS 管理スナップインを開きます。
 
AD FS 管理スナップインを開く 開始 をクリックしてのプログラム、管理ツール をポイントし、AD FS の管理 をクリックします。
 
6。       [操作] ウィンドウには、フェデレーション サービス プロパティ 7 の編集をクリックします。       フェデレーション サービスのプロパティ ダイアログ ボックスで、イベント タブをクリックします。8.       選択、**成功の監査**と**失敗の監査**チェック ボックス。
9.       [OK] をクリックします。

![audit の機能強化](media/ad-fs-tshoot-logging/event4.PNG)  
 
>[!NOTE]
>上記の手順については、AD FS がスタンドアロンのメンバー サーバー上にある場合にのみ使用されます。  ドメイン コント ローラーで、ローカル セキュリティ ポリシーではなく、AD FS が実行されている場合は、使用、**既定のドメイン コント ローラー ポリシー**内にある**グループ ポリシーの管理/ドメイン/フォレスト/ドメイン コント ローラー**します。  [編集] をクリックしに移動します**コンピューター \policies\windows 設定 \ セキュリティ settings \local policies \user Rights Management**

## <a name="windows-communication-foundation-and-windows-identity-foundation-messages"></a>Windows Communication Foundation と Windows Identity Foundation のメッセージ
トレース ログ記録、に加えても必要がありますの問題をトラブルシューティングするために Windows Communication Foundation (WCF) および Windows Identity Foundation (WIF) のメッセージを表示します。 これを行う変更、 **Microsoft.IdentityServer.ServiceHost.Exe.Config** AD FS サーバー上のファイル。 

このファイルにある **< % のシステム ルート % > \Windows\ADFS**は XML 形式とします。 ファイルの関連する部分は、以下に示します。 
```
<!-- To enable WIF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="Microsoft.IdentityModel" switchValue="Off"> … </source>

<!-- To enable WCF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="System.ServiceModel" switchValue="Off" > … </source>
```


これらの変更を適用した後は、構成を保存し、AD FS サービスを再起動します。 適切なスイッチを設定してこれらのトレースを有効にした後は、Windows イベント ビューアーでの AD FS トレース ログに表示されます。

## <a name="correlating-events"></a>イベントの関連付け
多くのエラーを生成またはイベントをデバッグするアクセスの問題のトラブルシューティングを行う最も困難な作業の 1 つです。

このために、AD FS が、管理者と、一意なグローバル一意識別子 (GUID)、アクティビティの ID と呼ばれるを使用して、特定の要求に対応するデバッグ ログの両方で、イベント ビューアーに記録されるすべてのイベントを関連付ける トークン発行要求が (パッシブな要求側プロファイルを使用してアプリケーション) 用の web アプリケーションまたは (アプリケーションが Ws-trust を使用して) に対して、要求プロバイダーに直接送信される要求に最初に表示された場合、この ID が生成されます。 

![activityid](media/ad-fs-tshoot-logging/activityid1.png)

このアクティビティ ID はも同じ数、要求の期間全体とすべてのイベントが、その要求のビューアー記録イベントとして記録されます。 これは、以下を意味します。
 - フィルターやトークンの要求に対応するすべての関連イベントの追跡 ID に役立つことができます、このアクティビティを使用して、イベント ビューアーを検索します。
 - フェデレーション サーバー プロキシ (FSP) などの複数のコンピューターで、ユーザーの要求のトラブルシューティングに別のマシン間で、同じアクティビティ ID が記録されます。
 - アクティビティ ID も表示されます、ユーザーのブラウザーで、何らかの方法で AD FS の要求が失敗した場合ため、ユーザーはこの ID をヘルプ デスクや IT サポートと通信することができます。

![activityid](media/ad-fs-tshoot-logging/activityid2.png)

トラブルシューティングのプロセスを支援するために、AD FS は AD FS サーバーで、トークン発行プロセスが失敗したときに、呼び出し元 ID のイベントも記録します。 このイベントには、要求の種類とトークン要求の一部として、この情報が、フェデレーション サービスに渡されたことと仮定すると、次の要求タイプのいずれかの値が含まれています。
- http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountnameh
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upnh
- http://schemas.microsoft.com/ws/2008/06/identity/claims/upn
- http://schemas.xmlsoap.org/claims/UPN
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddressh
- http://schemas.microsoft.com/ws/2008/06/identity/claims/emailaddress 
- http://schemas.xmlsoap.org/claims/EmailAddress
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name
- http://schemas.microsoft.com/ws/2008/06/identity/claims/name
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier 

呼び出し元の ID のイベントでは、そのアクティビティ ID、特定の要求のイベント ログを検索またはフィルターを使用できるようにアクティビティ ID も記録します。




## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)
