---
ms.assetid: 208928eb-bb17-4984-a312-23fff43133e3
title: Windows Server 2016 での AD FS の監査機能の強化
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/25/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2f6e4abb4255281be85b7fa928566f681bcf2de2
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188364"
---
# <a name="auditing-enhancements-to-ad-fs-in-windows-server-2016"></a>Windows Server 2016 での AD FS の監査機能の強化


現時点では、AD FS を Windows Server 2012 R2 は、1 つの要求と、ログ内の関連情報が生成された多数の監査イベントまたはトークンの発行アクティビティが存在しないか、(でいくつかのバージョンの AD FS) または複数のイベントの監査に分散します。 AD FS の既定で、詳細な性質により、イベントの監査が無効になっています。  
    Windows Server 2016 での AD FS のリリースでは、監査は効率となりに少なくなります。  
  
## <a name="auditing-levels-in-ad-fs-for-windows-server-2016"></a>Windows Server 2016 の AD FS の監査レベル  
既定では、Windows Server 2016 での AD FS が、基本的な監査を有効にします。  基本的な監査では、管理者は 1 つの要求の 5 個以下のイベントに表示されます。  これは、管理者が参照、1 つの要求を表示するにはイベントの数が大幅に低下をマークします。   監査レベルが発生するまたは PowerShell コマンドレットを使用します。Set-adfsproperties-AuditLevel します。  次の表では、利用可能な監査レベルについて説明します。  
  
||||  
|-|-|-|  
|監査レベル|PowerShell の構文|説明|  
|なし|Set-adfsproperties - AuditLevel なし|監査が無効になっているし、イベントは記録されません。|  
|Basic (既定値)|Set-adfsproperties - AuditLevel Basic|1 つの要求の 5 つ以上のイベントが記録されます。|  
|Verbose|Set-adfsproperties - AuditLevel 詳細|すべてのイベントが記録されます。  これにより、大量の要求ごとの情報が記録されます。|  
  
現在の監査レベルを表示するには、PowerShell コマンドレットを使用できます。Get-adfsproperties します。  
  
![audit の機能強化](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_1.PNG)  
  
監査レベルが発生するまたは PowerShell コマンドレットを使用します。Set-adfsproperties-AuditLevel します。  
  
![audit の機能強化](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_2.png)  
  
## <a name="types-of-audit-events"></a>監査イベントの種類  
AD FS の監査イベントは、AD FS によって処理された要求の種類に基づいて、さまざまな種類の指定できます。 それぞれの監査イベントの種類は、関連付けられている特定のデータを持ちます。  監査イベントの種類は、システムの要求 (サーバーの呼び出しの構成情報のフェッチなど) と、ログイン要求 (つまりトークン要求) の間で区別できます。    
  次の表では、監査イベントの基本型について説明します。  
  
||||  
|-|-|-|  
|監査イベントの種類|イベント ID|説明|  
|新しい資格情報の検証の成功|1202|場所、新しい資格情報は、フェデレーション サービスによって正常に検証の要求です。 これには、Ws-trust、Ws-federation、SAML-p が含まれます (SSO を生成する最初の段階) と OAuth 承認エンドポイント。|  
|新しい資格情報の検証エラー|1203|フェデレーション サービスで新しい資格情報の検証が失敗した場所の要求です。 Ws-trust、これが含まれています、Ws-fed、SAML P (SSO を生成する最初の段階) と OAuth 承認エンドポイント。|  
|アプリケーション トークンの成功率|1200|セキュリティ トークンが正常にフェデレーション サービスによってに発行された場所の要求です。 Ws-federation、SAML P SSO アーティファクトを要求が処理されるときに記録されます。 (、SSO cookie など)。|  
|アプリケーション トークンのエラー|1201|フェデレーション サービスでセキュリティ トークンの発行要求が失敗しました。 Ws-federation、SAML P SSO アーティファクトを要求の処理時に記録されます。 (、SSO cookie など)。|  
|パスワード変更要求の成功|1204|パスワード変更要求、トランザクションが、フェデレーション サービスによって正常に処理します。|  
|パスワードの変更要求エラー|1205|フェデレーション サービスによって処理されるパスワードの変更要求、トランザクションが失敗しました。| 
|成功をサインアウトします。|1206|サインアウト要求が成功した場合について説明します。|  
|サインインに失敗しました|1207|サインアウト要求の失敗について説明します。|  

  


