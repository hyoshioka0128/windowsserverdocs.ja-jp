---
ms.assetid: 44271f44-b50a-4bce-9375-4fcab9618048
title: "チェックリスト - Creating Claim Rules for 証明書利用者の信頼します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 9c75cd4ccbafefdda83cba4551fd6b9af63c4822
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-creating-claim-rules-for-a-relying-party-trust"></a>チェックリスト: 証明書利用者のパーティ信頼の要求規則を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このチェックリストには、計画、設計、および Active Directory フェデレーション サービス \(AD FS\) で証明書利用者信頼に関連付けられている要求規則を展開するために必要なタスクが含まれます。  
  
> [!NOTE]  
> 順序でこのチェックリストのタスクを完了します。 参照リンクでは、手順には、このトピックに戻りできるように、このチェックリストの残りのタスクを続行することができます、その手順の手順を完了します。  
  
![要求規則を作成する](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: 証明書利用者信頼のセットを要求規則を作成します。**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![要求規則の作成](media/icon_checkboxo.gif)|信頼性情報に関する概念を確認、要求規則、要求規則セット、および要求規則テンプレートとフェデレーションの信頼に関連付けられている方法です。|![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of Claims](../../ad-fs/technical-reference/The-Role-of-Claims.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[、要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|  
|![要求規則の作成](media/icon_checkboxo.gif)|要求発行パイプライン内のすべてのステージを通過する要求のフローし、規則が、要求発行エンジンによってどのように処理されるかについての概念を確認します。|![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求パイプラインの役割](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of the Claims Engine](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|  
|![要求規則の作成](media/icon_checkboxo.gif)|効果的に計画して、この証明書利用者信頼を経由で発行される出力の信頼性情報の実装、1 つまたは複数の要求規則が必要かどうかと、証明書利用者の信頼これを使用するルールを要求するを確認します。|![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[決定、型の要求規則テンプレートを使用する](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md)|  
|![要求規則の作成](media/icon_checkboxo.gif)|1 つの要求を作成する別の規則および理想的な出力に期待どおりの結果を提供するために標準的な規則よりもさらに複雑なロジックを提供する要求規則言語を使用する方法要求セットとに関する概念を確認します。|![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[パススルーまたはフィルターの要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[変換要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[as Claims Rule a Send LDAP Attributes を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求規則として a Send Group Membership を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[カスタム要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求規則言語の役割](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)|  
|![要求規則の作成](media/icon_checkboxo.gif)|既に存在しない場合、要求記述を作成する必要があります、組織のニーズを満たすことができます。 AD FS は、の AD FS 管理スナップインで公開されている要求記述の既定のセットが付属します。|![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[要求記述の追加](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![要求規則の作成](media/icon_checkboxo.gif)|組織のニーズに応じて、信頼性情報が適切に発行できるように、この証明書利用者信頼に関連付けられている規則セットの 1 つまたは複数の要求規則を作成します。|![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[パススルーするルールを作成または入力方向の要求をフィルター処理](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[LDAP 属性を要求として送信する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[グループ メンバーシップを要求として送信する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[入力方向の要求を変換する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[、認証メソッドの要求を送信する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[、AD FS を送信する規則を作成する要求の互換性のある 1.x](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[信頼性情報を使用して送信する規則をカスタム規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)|  
|![要求規則の作成](media/icon_checkboxo.gif)|組織のニーズに応じて発行承認規則セットまたはユーザーが証明書利用者にアクセスを許可するように、この証明書利用者信頼に関連付けられている委任承認規則セットのいずれかの 1 つまたは複数の要求規則を作成します。|![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[すべてのユーザーを許可する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[入力方向の要求に基づく許可または拒否のユーザーにルールを作成します。](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)|  
