---
ms.assetid: 208928eb-bb17-4984-a312-23fff43133e3
title: "Windows Server 2016 の AD FS の監査機能強化"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/25/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3d622686a3cc34316f0cf5187839785195c2f104
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="auditing-enhancements-to-ad-fs-in-windows-server-2016"></a>Windows Server 2016 の AD FS の監査機能強化

>Windows Server 2016 の適用対象:

現時点では、AD FS Windows Server 2012 R2 があるは 1 つの要求の生成された多数の監査イベントおよび関連するログインまたはトークンの発行アクティビティについては、存在しないか、一部のバージョンの AD FS) の「または複数の監査イベントの間で分散します。 既定では、AD FS の詳細な性質、監査イベントが無効になります。  
    リリースでは、Windows Server 2016 での AD FS の監査になりより合理化された出力を少なくします。  
  
## <a name="auditing-levels-in-ad-fs-for-windows-server-2016"></a>Windows Server 2016 の AD FS の監査レベル  
既定では、Windows Server 2016 での AD FS には基本的な監査を有効にします。  基本の監査では、管理者に 1 つの要求の 5 つのイベントが表示されます。  これは、管理者を見て、1 つの要求を確認するためにイベントの数が大幅に低下をマークします。   監査レベルが発生する可能性がまたは PowerShell コマンドレットを使用して落とされました: Set-AdfsProperties AuditLevel します。  次の表では、利用可能な監査レベルについて説明します。  
  
||||  
|-|-|-|  
|監査レベル|PowerShell の構文|説明|  
|[なし]|Set-AdfsProperties - AuditLevel なし|監査が無効になっているし、イベントがログに記録されません。|  
|Basic (既定)|Set-AdfsProperties - AuditLevel Basic|1 つの要求の 5 つ以内のイベントが記録されます。|  
|詳細です|Set-AdfsProperties - Verbose AuditLevel|すべてのイベントをログに記録されます。  大量の要求ごとに情報を記録します。|  
  
表示するには、現在の監査レベルは、PowerShell コマンドレットを使用することができます: Get-AdfsProperties します。  
  
![監査の強化](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_1.PNG)  
  
監査レベルが発生する可能性がまたは PowerShell コマンドレットを使用して落とされました: Set-AdfsProperties AuditLevel します。  
  
![監査の強化](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_2.png)  
  
## <a name="types-of-audit-events"></a>監査イベントの種類  
AD FS の監査イベントには、AD FS によって処理された要求の種類に基づいて、さまざまな種類を指定できます。 監査イベントの種類ごとには、関連付けられている特定のデータがあります。  システムの要求 (サーバーの呼び出しがフェッチ構成情報など) とログイン要求 (つまりトークン要求) の間での監査イベントの種類を区別できます。    
  次の表では、基本的な種類の監査イベントについて説明します。  
  
||||  
|-|-|-|  
|監査イベントの種類|イベント ID|説明|  
|新しい資格情報の検証の成功|1202|ここで、新しい資格情報は、フェデレーション サービスによって正常に検証の要求。 これにより、Ws-trust、Ws-federation、SAML-p が含まれます (SSO を生成する最初の脚) と OAuth の承認エンドポイント。|  
|新しい資格情報の検証エラー|1203|フェデレーション サービスで新しい資格情報の検証が失敗した要求します。 Ws-trust、これが含まれています WS が取り込ま、SAML P (SSO を生成する最初の脚) と OAuth の承認エンドポイント。|  
|アプリケーション トークンの成功|1200|フェデレーション サービスによってのセキュリティ トークンの正常の発行要求します。 Ws-federation、SAML P この SSO 成果物に要求が処理されるときに記録されます。 (など、SSO の Cookie)。|  
|アプリケーション トークンの失敗|1201|フェデレーション サービスのセキュリティ トークンの発行要求に失敗しました。 Ws-federation、SAML P この SSO 成果物に要求が処理されるときに記録されます。 (など、SSO の Cookie)。|  
|パスワードの変更要求の成功|1204|パスワード変更要求のトランザクションは、フェデレーション サービスによって正常に処理されました。|  
|パスワードの変更要求エラー|1205|パスワード変更要求のトランザクションは、フェデレーション サービスによって処理に失敗しました。| 
|成功からサインアウトします。|1206|要求が成功するサインアウトについて説明します。|  
|サインインに失敗しました|1207|失敗したサインアウト要求をについて説明します。|  

  


