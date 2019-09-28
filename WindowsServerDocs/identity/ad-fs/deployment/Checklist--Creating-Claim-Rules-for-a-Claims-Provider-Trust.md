---
ms.assetid: 503733f8-be0c-429c-81f0-cd4205e8b118
title: チェックリスト-要求プロバイダー信頼の要求規則を作成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: fb1e0dba5921a2f49452cab5cb622aed3e7eb57d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359963"
---
# <a name="checklist-creating-claim-rules-for-a-claims-provider-trust"></a>チェックリスト:要求プロバイダー信頼の要求規則を作成する


このチェックリストには、Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 の要求プロバイダー信頼に関連付けられている要求規則を計画、設計、および展開するためのタスクが含まれています。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
@no__t の要求規則の作成 @ no__t-1 チェックリスト:要求プロバイダー信頼の要求規則セットを作成する @ no__t-0  
  
||タスク|参照|  
|-|--------|-------------|  
|![要求規則の作成](media/icon_checkboxo.gif)|要求、要求規則、要求規則セット、要求規則テンプレート、およびそれらがフェデレーション信頼にどのように関連付けられているかに関する概念を確認します。|要求規則を作成する @no__t 要求](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)<br /><br />@no__t の要求規則の作成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|  
|![要求規則の作成](media/icon_checkboxo.gif)|要求発行パイプラインのすべてのステージを通じて要求がどのように流れ、要求発行エンジンによってルールがどのように処理されるかについての概念を確認します。|![ 要求](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[パイプラインの役割を](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)作成する<br /><br />要求規則を作成する @no__t、](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求エンジンの役割](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|  
|![要求規則の作成](media/icon_checkboxo.gif)|この要求プロバイダー信頼に対して発行される出力要求を効果的に計画および実装するには、1つまたは複数の要求規則が必要かどうか、およびこの要求プロバイダー信頼で使用する必要がある要求規則を確認します。|![creating 規則を作成し](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[て、使用する要求規則テンプレートの種類を決定](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md)する|  
|![要求規則の作成](media/icon_checkboxo.gif)|別の要求規則を作成するタイミングと、要求規則言語を使用して標準規則より複雑なロジックを提供する方法についての概念を確認して、理想的な出力要求セットに必要な結果を提供します。|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0Creating または Filter 要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)の要求規則の作成<br /><br />![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[変換要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md)の要求規則の作成<br /><br />@no__t-"](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[LDAP 属性を要求として送信する" 規則を使用する場合の](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)要求規則の作成<br /><br />要求規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[としてグループのメンバーシップを使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)に要求規則を作成する @no__t<br /><br />@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0Creating 要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md)の要求規則の作成<br /><br />![ 要求規則](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[言語の役割を](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)作成する|  
|![要求規則の作成](media/icon_checkboxo.gif)|要求の説明は、組織のニーズを満たすものが存在しない場合に作成する必要があります。 AD FS には、の AD FS 管理スナップインで公開される要求説明の既定のセットが付属しています。|![creating 規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[要求の説明を追加](../../ad-fs/operations/Add-a-Claim-Description.md)する|  
|![要求規則の作成](media/icon_checkboxo.gif)|組織のニーズに応じて、要求が適切に発行されるように、この要求プロバイダー信頼に関連付けられている受け入れ変換規則セットに対して1つまたは複数の要求規則を作成します。|![creating 規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[を作成する規則を作成して、入力方向の要求をパススルーまたはフィルター処理する](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)<br /><br />![creating 規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[を作成する規則を作成して、LDAP 属性を要求として送信する](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<br /><br />![creating 規則を作成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[する規則を作成して、グループメンバーシップを要求として送信する](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)<br /><br />![creating 規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[を作成する規則を作成して、入力方向の要求を変換する](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)<br /><br />![creating 規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[を作成する認証方法の要求を送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)<br /><br />![creating 要求規則](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[を作成する AD FS 1. x 互換の要求を送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)<br /><br />![creating 規則を作成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[するルールを作成して、カスタム規則を使用して要求を送信する](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)|  
  

