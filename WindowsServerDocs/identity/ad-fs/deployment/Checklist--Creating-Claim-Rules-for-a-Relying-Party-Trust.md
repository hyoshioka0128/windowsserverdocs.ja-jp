---
ms.assetid: 44271f44-b50a-4bce-9375-4fcab9618048
title: チェックリスト - Creating Claim Rules for 証明書利用者の信頼します。
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 9c75cd4ccbafefdda83cba4551fd6b9af63c4822
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817403"
---
# <a name="checklist-creating-claim-rules-for-a-relying-party-trust"></a>チェックリスト:A Relying Party Trust の要求規則を作成します。

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このチェックリストには、設計、計画、必要なタスクが含まれています。 および要求 Active Directory フェデレーション サービスでの、証明書利用者信頼に関連付けられている規則を展開する\(AD FS\)します。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![要求規則を作成する](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。証明書利用者信頼の要求規則セットを作成します。**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![要求規則を作成します。](media/icon_checkboxo.gif)|要求に関する概念を確認、要求規則、要求規則のセット、および要求規則テンプレートおよびフェデレーションによる信頼関係に関連付けられている方法。|![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The Role of Claims](../../ad-fs/technical-reference/The-Role-of-Claims.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)|  
|![要求規則を作成します。](media/icon_checkboxo.gif)|要求発行パイプライン内のすべての段階で、要求のフローし、要求発行エンジンによってルールの処理方法に関する概念を確認します。|![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求パイプラインの役割](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求エンジンの役割](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)|  
|![要求規則を作成します。](media/icon_checkboxo.gif)|効果的に計画し、この証明書利用者信頼経由で発行される出力要求を実装する、1 つまたは複数の要求規則が必要かどうかと、ルールの信頼証明書利用者をこれを使用する必要がありますが、どの要求を確認します。|![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[決定、型の要求規則テンプレートを使用する](../../ad-fs/technical-reference/Determine-the-Type-of-Claim-Rule-Template-to-Use.md)|  
|![要求規則を作成します。](media/icon_checkboxo.gif)|ときに、1 つの要求を作成する別のルールおよび最適な出力に目的の結果を提供するために標準の規則よりも複雑なロジックを提供する要求規則言語を使用する方法クレーム セットについての概念を確認します。|![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[パススルーまたはフィルターの要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[変換要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Transform-Claim-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[as Claims Rule a Send LDAP Attributes を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Send-LDAP-Attributes-as-Claims-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求規則と送信のグループ メンバーシップを使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[カスタム要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Custom-Claim-Rule.md)<br /><br />![要求規則を作成する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求規則言語の役割](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)|  
|![要求規則を作成します。](media/icon_checkboxo.gif)|既に存在しない場合、クレームの説明を作成する必要があります、組織のニーズを満たします。 AD FS が公開されている要求記述の既定のセットが付属しています AD FS 管理スナップインで\-でします。|![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Add a Claim Description](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![要求規則を作成します。](media/icon_checkboxo.gif)|組織のニーズに応じて、要求が適切に発行されるようにこの証明書利用者信頼に関連付けられている規則セットの 1 つまたは複数の要求規則を作成します。|![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[パススルーするルールを作成または入力方向の要求をフィルター処理](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[要求として LDAP 属性を送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[グループ メンバーシップを要求として送信するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[入力方向の要求を変換する規則を作成](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[認証メソッド要求を送信するルールの作成](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[AD FS を送信するルールの作成要求の互換性のある 1.x](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[送信要求を使用するルールを作成するには、カスタム規則](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)|  
|![要求規則を作成します。](media/icon_checkboxo.gif)|組織のニーズに応じて発行承認規則のセットまたはユーザーに証明書利用者へのアクセスを許可するためにこの証明書利用者信頼に関連付けられている委任承認規則セットのいずれかの 1 つまたは複数の要求規則を作成します。パーティです。|![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[すべてのユーザーを許可するルールを作成](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)<br /><br />![要求規則を作成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[入力方向の要求を許可または拒否するユーザー ベースに規則を作成](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)|  
