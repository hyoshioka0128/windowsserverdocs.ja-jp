---
ms.assetid: 208928eb-bb17-4984-a312-23fff43133e3
title: Windows Server 2016 での AD FS の監査機能の強化
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/25/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4eb93513d12b2bba2620ff16be24f62ace5dee85
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407251"
---
# <a name="auditing-enhancements-to-ad-fs-in-windows-server-2016"></a>Windows Server 2016 での AD FS の監査機能の強化


現時点では、Windows Server 2012 R2 の AD FS には、1つの要求に対して生成される監査イベントが多数あり、ログインまたはトークンの発行アクティビティに関する関連情報が存在しない (一部のバージョンの AD FS) か、複数の監査イベントに分散されています。 既定では、AD FS 監査イベントは、詳細な性質のために無効になっています。  
    Windows Server 2016 の AD FS のリリースにより、監査が効率化され、詳細が少なくなりました。  
  
## <a name="auditing-levels-in-ad-fs-for-windows-server-2016"></a>Windows Server 2016 の AD FS の監査レベル  
既定では、Windows Server 2016 の AD FS には、基本的な監査が有効になっています。  基本的な監査を使用すると、管理者は1つの要求に対して5つ以下のイベントを表示できます。  これは、1つの要求を表示するために、管理者が確認する必要があるイベントの数が大幅に減少することを示しています。   監査レベルを上げたり下げたりするには、PowerShell cmdlt を使用します。Set-adfsproperties-AuditLevel を設定します。  次の表は、使用可能な監査レベルを示しています。  
  
||||  
|-|-|-|  
|監査レベル|PowerShell の構文|説明|  
|なし|Set-adfsproperties-AuditLevel None|監査は無効になり、イベントはログに記録されません。|  
|基本 (既定値)|Set-adfsproperties-AuditLevel Basic|1つの要求に対して記録されるイベントは5件までです|  
|Verbose|Set-adfsproperties-AuditLevel Verbose|すべてのイベントがログに記録されます。  これにより、要求ごとに膨大な量の情報がログに記録されます。|  
  
現在の監査レベルを表示するには、PowerShell cmdlt を使用します。Set-adfsproperties。  
  
![監査の強化](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_1.PNG)  
  
監査レベルを上げたり下げたりするには、PowerShell cmdlt を使用します。Set-adfsproperties-AuditLevel を設定します。  
  
![監査の強化](media/Auditing-Enhancements-to-AD-FS-in-Windows-Server-2016/ADFS_Audit_2.png)  
  
## <a name="types-of-audit-events"></a>監査イベントの種類  
AD FS によって処理されたさまざまな種類の要求に基づいて、AD FS の監査イベントを異なる種類にすることができます。 各種類の監査イベントには、特定のデータが関連付けられています。  監査イベントの種類は、ログイン要求 (つまり、トークン要求) とシステム要求 (構成情報のフェッチを含むサーバーサーバー呼び出し) の間で区別できます。    
  次の表では、基本的な種類の監査イベントについて説明します。  
  
||||  
|-|-|-|  
|監査イベントの種類|イベント ID|説明|  
|新しい資格情報の検証の成功|1202|フェデレーションサービスによって、新しい資格情報が正常に検証される要求。 これには、WS-TRUST、WS-FEDERATION、SAML-P (SSO を生成する最初のレッグ)、OAuth 承認エンドポイントが含まれます。|  
|新しい資格情報の検証エラー|1203|フェデレーションサービスで新しい資格情報の検証が失敗した要求。 これには、WS-TRUST、WS-ATOMICTRANSACTION、SAML-P (SSO を生成する最初のレッグ)、OAuth 承認エンドポイントが含まれます。|  
|アプリケーショントークンの成功|1200|フェデレーションサービスによってセキュリティトークンが正常に発行される要求。 WS-FEDERATION の場合、これは SSO アーティファクトを使用して要求が処理されるときにログに記録されます。 (SSO cookie など)。|  
|アプリケーショントークンのエラー|1201|フェデレーションサービスでセキュリティトークンの発行に失敗した要求。 WS-FEDERATION の場合、これは SSO アーティファクトを使用して要求が処理されたときにログに記録されます。 (SSO cookie など)。|  
|パスワード変更要求の成功|1204|フェデレーションサービスによってパスワード変更要求が正常に処理されたトランザクション。|  
|パスワード変更要求エラー|1205|フェデレーションサービスによってパスワード変更要求を処理できなかったトランザクション。| 
|サインアウトの成功|1206|正常なサインアウト要求について説明します。|  
|サインアウトエラー|1207|失敗したサインアウト要求について説明します。|  

  


