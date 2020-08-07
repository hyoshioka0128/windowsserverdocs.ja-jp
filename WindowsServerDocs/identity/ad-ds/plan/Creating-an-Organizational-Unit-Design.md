---
ms.assetid: b8df1828-5ead-4c90-b0fe-95c675116b7c
title: 組織単位の設計を作成する
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 96fd3dd2d090ef6b39b99962e6b639bf2abdcb62
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947743"
---
# <a name="creating-an-organizational-unit-design"></a>組織単位の設計を作成する

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

フォレスト所有者は、ドメインの組織単位 (OU) 設計を作成します。 Ou 設計を作成するには、ou 構造の設計、OU 所有者ロールの割り当て、およびアカウントとリソース Ou の作成が必要になります。

最初に、OU 構造を設計して、管理の委任を有効にします。 OU の設計が完了したら、ユーザーとコンピューターにグループポリシーを適用するための追加の OU 構造を作成したり、オブジェクトの表示を制限したりすることができます。 詳細については、「[グループポリシーインフラストラクチャの設計](/previous-versions/windows/it-pro/windows-server-2003/cc786524(v=ws.10))」を参照してください。

## <a name="ou-owner-role"></a>OU 所有者ロール
フォレストの所有者は、ドメインに対して設計する OU ごとに OU 所有者を指定します。 OU の所有者は、Active Directory Domain Services (AD DS) 内のオブジェクトのサブツリーを制御するデータマネージャーです。 OU の所有者は、管理を委任する方法と、OU 内のオブジェクトにポリシーを適用する方法を制御できます。 また、新しいサブツリーを作成し、そのサブツリー内の Ou の管理を委任することもできます。

OU 所有者は、ディレクトリサービスの動作を所有または制御しないため、ディレクトリサービスの所有権と管理をオブジェクトの所有権と管理から分離することで、高いレベルのアクセス権を持つサービス管理者の数を減らすことができます。

Ou は、ディレクトリ内のオブジェクトの表示を制御するための管理自律性と手段を提供します。 Ou は、他のデータ管理者から分離されていますが、サービス管理者の分離を提供するものではありません。 OU 所有者は、オブジェクトのサブツリーを制御できますが、フォレスト所有者はすべてのサブツリーに対して完全な制御を保持します。 これにより、フォレスト所有者は、アクセス制御リスト (ACL) のエラーなどの誤りを修正したり、データ管理者が終了したときに委任されたサブツリーを再利用したりできます。

## <a name="account-ous-and-resource-ous"></a>アカウント Ou とリソース Ou
アカウント Ou には、ユーザー、グループ、およびコンピューターオブジェクトが含まれます。 フォレストの所有者は、これらのオブジェクトを管理する OU 構造を作成し、その構造の制御を OU 所有者に委任する必要があります。 新しい AD DS ドメインを展開する場合は、ドメインのアカウント OU を作成して、ドメイン内のアカウントの制御を委任できるようにします。

リソース Ou には、リソースと、それらのリソースの管理を担当するアカウントが含まれます。 また、フォレストの所有者は、これらのリソースを管理し、その構造の制御を OU 所有者に委任する OU 構造の作成も行います。 必要に応じて、組織内の各グループの要件に基づいてリソース Ou を作成し、データと機器の管理における自律性を求めます。

## <a name="documenting-the-ou-design-for-each-domain"></a>各ドメインの OU 設計を文書化する
フォレスト内のリソースの制御を委任するために使用する OU 構造を設計するチームを結成します。 フォレスト所有者は、設計プロセスに関与し、OU 設計を承認する必要があります。 また、設計が有効であることを確認するために、少なくとも1つのサービス管理者が必要になる場合があります。 その他の設計チームの参加者には、Ou を操作するデータ管理者と、それらの管理を担当する OU 所有者を含めることができます。

OU の設計を文書化することが重要です。 作成する Ou の名前を一覧表示します。 さらに、ou ごとに、ou の種類、OU 所有者、親 OU (該当する場合)、およびその OU の出所を文書化します。

OU 設計を文書化するのに役立つワークシートについては、 [Windows Server 2003 Deployment Kit のジョブエイド](https://microsoft.com/download/details.aspx?id=9608)から Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードし、「各ドメインの Ou を識別する」 (DSSLOGI_9.doc) を開いてください。

## <a name="in-this-section"></a>このセクションの内容

- [OU の設計概念を確認する](../../ad-ds/plan/Reviewing-OU-Design-Concepts.md)

- [OU オブジェクトを使用して管理を委任する](../../ad-ds/plan/Delegating-Administration-by-Using-OU-Objects.md)
