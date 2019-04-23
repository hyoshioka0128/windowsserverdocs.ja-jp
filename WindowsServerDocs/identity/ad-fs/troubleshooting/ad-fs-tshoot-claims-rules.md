---
title: AD FS のトラブルシューティング - 要求規則
description: このドキュメントは、AD FS のクレーム規則の構文をトラブルシューティングする方法を説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 027b2afc9e580253ec820e7e5be14419387ddd44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837923"
---
# <a name="ad-fs-troubleshooting---claims-rules-syntax"></a>要求規則の構文の AD FS のトラブルシューティング
クレームは、ステートメント自体または別の方法により、その 1 つのサブジェクトが対象です。  要求は、証明書利用者のパーティによって発行し、1 つまたは複数の値が指定され、AD FS サーバーによって発行されるセキュリティ トークンにパッケージ化します。  この記事では、要求の構文と作成について説明します。  要求に関する情報の発行を参照してください[AD FS のトラブルシューティング - 要求の発行](ad-fs-tshoot-claims-issuance.md)します。

>[!NOTE]  
>使用することができます[ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest)上、 [ADFS ヘルプ](https://adfshelp.microsoft.com)要求の問題のトラブルシューティングに役立つサイト。   

## <a name="how-claim-rules-are-processed"></a>要求規則の処理方法
要求規則の処理は、[要求パイプライン](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md)を使用して、[要求エンジン](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)します。 要求エンジンは、ユーザーによって提示される入力方向の要求のセットを調査し、各規則のロジックに応じて要求の出力セットを生成する、フェデレーション サービスの論理コンポーネントです。

## <a name="how-to-create-a-claim-rule"></a>要求規則の作成方法
要求規則は、フェデレーション サービス内のフェデレーションによる信頼関係ごとに作成され、複数の信頼間で共有されません。 取得したルールを作成するか、[要求規則テンプレート](../../ad-fs/technical-reference/determine-the-type-of-claim-rule-template-to-use.md)を使用して、ルールを作成することにより、ゼロから始める、[要求規則言語](../../ad-fs/technical-reference/when-to-use-a-custom-claim-rule.md)または規則をカスタマイズする Windows PowerShell を使用します。

## <a name="understanding-the-components-of-the-claim-rule-language"></a>要求規則言語のコンポーネントを理解する
要求規則言語で区切られた、次のコンポーネントから成る、"= >"演算子。

- 入力方向の要求を確認し、規則の発行ステートメントを実行するかどうかを判断するために使用条件 - です。  評価する必要がある論理式を表す規則の本文部分を実行する場合は true にします。

- 発行ステートメント

以下に例を示します。

```c:[type == "Name", value == "domain user"] => issue(type = "Role", value = "employee");``` 

次の要求には、次があります。
- 条件 - `c:[type == "Name", value == "domain user"] ` -windows アカウント名がドメイン ユーザーであるかどうかの入力要求を評価します。
- 発行 -`issue(type = "Role", value = "employee")`条件が true の場合 - 従業員の役割を持つ入力要求への新しい要求を追加します。

信頼性情報と、構文の詳細については、次を参照してください。 [、要求規則言語の役割](../../ad-fs/technical-reference/the-role-of-the-claim-rule-language.md)します。

## <a name="claims-rule-editor"></a>要求ルール エディター
要求が完了し、クリックした後、要求規則のエディターによって実行されます構文チェック**OK**します。  不適切な構文がある場合、エディターを確認できます。

![要求](media/ad-fs-tshoot-claims/claims1.png)

## <a name="event-logs"></a>イベント ログ
ログを使用して要求のトラブルシューティングを行うを検索するときに最適な方法は、要求の出力を検索します。  イベント ログに 1000 および 1001 のイベントを検索することができます。

![要求](media/ad-fs-tshoot-claims/claims2.png)

## <a name="creating-a-sample-application"></a>サンプル アプリケーションを作成します。
作成することも、サンプル アプリケーションをエコー要求。  たとえばサンプル アプリケーションを使用でき、アプリが要求を問題のトラブルシューティングとしている同じクレームを含む証明書利用者のパーティを作成できます。

![要求](media/ad-fs-tshoot-claims/claim4.png)

優れたサンプルの web アプリはここで使用できます。  このアプリは、証明書利用者のパーティから受信した要求をエコー バックする単純な web アプリです。  これを使用するには、web.config のアプリを編集する必要があります。
- 変更する https://app1.contoso.com/sampappURL に、使用する、sampapp をホストするため
- AD FS フェデレーション サーバーをポイントする sts.contoso.com のすべてのインスタンスを変更します。
- 拇印に置き換えて、拇印

![要求](media/ad-fs-tshoot-claims/claims3.png)

次[ブログ記事](https://blogs.technet.microsoft.com/tangent_thoughts/2015/02/20/install-and-configure-a-simple-net-4-5-sample-federated-application-samapp/)が優れた、詳細な手順については、これを設定するためです。

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)