---
title: AD FS のトラブルシューティング-要求規則
description: このドキュメントでは、AD FS で要求規則構文のトラブルシューティングを行う方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d0146ba7cfc736f4d37ca66d58d624cc2f7f9a23
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366280"
---
# <a name="ad-fs-troubleshooting---claims-rules-syntax"></a>AD FS のトラブルシューティング-要求規則の構文
クレームは、1つのサブジェクトがそれ自体または別のサブジェクトに対して行うステートメントです。  要求は証明書利用者によって発行され、1つまたは複数の値が与えられ、AD FS サーバーによって発行されたセキュリティトークンにパッケージ化されます。  この記事では、要求の構文と作成について説明します。  要求の発行の詳細については[、「AD FS のトラブルシューティング-要求の発行](ad-fs-tshoot-claims-issuance.md)」を参照してください。

>[!NOTE]  
>[ADFS ヘルプ](https://adfshelp.microsoft.com)サイトの[ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest)を使用して、要求の問題のトラブルシューティングを行うことができます。   

## <a name="how-claim-rules-are-processed"></a>要求規則の処理方法
要求規則は、要求[エンジン](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)を使用して要求[パイプライン](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)を通じて処理されます。 要求エンジンは、ユーザーによって提示される入力方向の要求のセットを調査し、各規則のロジックに応じて要求の出力セットを生成する、フェデレーション サービスの論理コンポーネントです。

## <a name="how-to-create-a-claim-rule"></a>要求規則の作成方法
要求規則は、フェデレーション サービス内のフェデレーションによる信頼関係ごとに作成され、複数の信頼間で共有されません。 [要求規則テンプレート](../../ad-fs/technical-reference/determine-the-type-of-claim-rule-template-to-use.md)から規則を作成するには、[要求規則言語](../../ad-fs/technical-reference/when-to-use-a-custom-claim-rule.md)を使用して規則を作成するか、Windows PowerShell を使用して規則をカスタマイズします。

## <a name="understanding-the-components-of-the-claim-rule-language"></a>要求規則言語のコンポーネントを理解する
要求規則言語は、次のコンポーネントで構成され、"= >" 演算子で区切られます。

- 条件-入力要求を確認し、規則の発行ステートメントを実行する必要があるかどうかを判断するために使用されます。  ルールのボディ部を実行するには、true に評価する必要がある論理式を表します。

- 発行ステートメント

例:

```c:[type == "Name", value == "domain user"] => issue(type = "Role", value = "employee");``` 

次の要求には、次のものがあります。
- 条件-`c:[type == "Name", value == "domain user"] `-windows アカウント名がドメインユーザーであるかどうかの入力要求を評価します。
- 発行-`issue(type = "Role", value = "employee")`-条件が true の場合、従業員の役割を持つ新しい要求を入力要求に追加します。

クレームと構文の詳細については、「[要求規則言語の役割](../../ad-fs/technical-reference/the-role-of-the-claim-rule-language.md)」を参照してください。

## <a name="claims-rule-editor"></a>要求規則エディター
要求を完了したら、要求規則エディターによって構文チェックが実行され、[ **OK]** をクリックします。  構文が正しくない場合は、エディターで通知されます。

![保険](media/ad-fs-tshoot-claims/claims1.png)

## <a name="event-logs"></a>イベント ログ
ログを使用して要求のトラブルシューティングを行う場合は、要求出力を探すことをお勧めします。  イベントログで1000イベントと1001イベントを検索できます。

![保険](media/ad-fs-tshoot-claims/claims2.png)

## <a name="creating-a-sample-application"></a>サンプルアプリケーションの作成
また、要求をエコーするサンプルアプリケーションを作成することもできます。  たとえば、サンプルアプリケーションを使用して、トラブルシューティングしようとしている要求と同じクレームを持つ証明書利用者を作成し、その要求に関してアプリに問題があるかどうかを確認することができます。

![保険](media/ad-fs-tshoot-claims/claim4.png)

適切なサンプル web アプリについては、こちらを参照してください。  このアプリは、証明書利用者から受信した要求をエコーバックする単純な web アプリです。  これを使用するには、次の方法で web.config アプリを編集する必要があります。
- https://app1.contoso.com/sampapp を、sampapp のホストに使用する URL に変更します。
- フェデレーションサーバー AD FS ポイントするように sts.contoso.com のすべてのインスタンスを変更する
- 拇印を拇印に置き換える

![保険](media/ad-fs-tshoot-claims/claims3.png)

次の[ブログ記事](https://blogs.technet.microsoft.com/tangent_thoughts/2015/02/20/install-and-configure-a-simple-net-4-5-sample-federated-application-samapp/)では、これを設定するための詳細な手順について説明しています。

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)