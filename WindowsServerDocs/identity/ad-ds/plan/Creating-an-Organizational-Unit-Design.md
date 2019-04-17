---
ms.assetid: b8df1828-5ead-4c90-b0fe-95c675116b7c
title: "組織単位設計を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3a74770a4558c79d1f9250f37181562e1d235d34
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="creating-an-organizational-unit-design"></a>組織単位設計を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォレストの所有者は、それらのドメインの組織単位 (OU) の設計を作成します。 OU 設計の作成、OU の所有者ロールおよび作成のアカウントとリソース Ou の割り当て、OU 構造を設計する必要があります。  
  
最初に、管理の委任を有効にできるように OU 構造を設計します。 OU 設計が完了したら、ユーザーとコンピューターに、オブジェクトの表示を制限するグループ ポリシーの適用の他の OU 構造を作成できます。 詳細については、グループ ポリシー インフラストラクチャの設計を参照してください ([https://go.microsoft.com/fwlink/?LinkId=106655](https://go.microsoft.com/fwlink/?LinkId=106655))。  
  
## <a name="ou-owner-role"></a>OU の所有者の役割  
フォレストの所有者は、各設計では、ドメイン OU の組織単位の所有者を指定します。 OU の所有者とは、Active Directory ドメイン サービス (AD DS) 内のオブジェクトのサブツリーを制御するデータ管理者です。 OU の所有者には、管理を委任する方法と、その OU 内のオブジェクトにポリシーを適用する方法を制御できます。 新しいサブツリーを作成し、それらのサブツリー内の Ou の管理を委任することができますもします。  
  
OU の所有者を所有またはしないで、ディレクトリ サービスの操作を制御、ためにを分離できますの所有権とディレクトリ サービスの管理から、オブジェクトの所有権と管理高レベルのアクセスを持つサービス管理者の数を減らします。  
  
Ou は、自律的な管理とディレクトリ内のオブジェクトの可視性を制御するための手段を提供します。 Ou は、他のデータ管理者からの分離を提供しますが、サービス管理者から分離を提供しません。 OU の所有者には、オブジェクトのサブツリーの制御がありますが、フォレストの所有者には、すべてのサブツリーを完全に制御が保持されます。 これにより、フォレストの所有者のアクセス制御リスト (ACL) エラーなどのミスを修正して、データ管理者が終了されるときは、委任されたサブツリーを再利用します。  
  
## <a name="account-ous-and-resource-ous"></a>アカウント Ou とリソース Ou  
アカウント Ou には、ユーザー、グループ、およびコンピューター オブジェクトが含まれます。 フォレストの所有者は、これらのオブジェクトを管理し、OU の所有者に構造体の制御を委任する OU 構造を作成する必要があります。 新しい AD DS ドメインを展開する場合は、ドメイン内のアカウントの制御を委任できるようにドメインのアカウント OU を作成します。  
  
リソース Ou には、リソースとそれらのリソースを管理する責任者であるアカウントが含まれます。 フォレストの所有者は、これらのリソースを管理する OU 構造を作成するため、および OU の所有者にその構造体の制御を委任する責任もできます。 リソース Ou 必要に応じて作成機器とデータの管理を自律的に、組織内の各グループの要件に基づきします。  
  
## <a name="documenting-the-ou-design-for-each-domain"></a>各ドメインの OU の設計を文書化  
フォレスト内のリソースの制御を委任するために使用する OU 構造を設計するチームを構成します。 フォレストの所有者は、設計プロセスに携わる可能性があるし、OU の設計を承認する必要があります。 設計が有効であることを確認するには、少なくとも 1 つのサービス管理者もあります。 設計チームの他の参加者には、それらを管理する責任を負う所有者 Ou と OU で作業するデータの管理者が含まれます。  
  
OU 設計のドキュメントに重要です。 作成する Ou の名前を一覧表示します。 各 OU の OU、OU の所有者、親 OU (該当する場合)、およびその OU の原点の種類を文書化します。  
  
Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip).  
  
## <a name="in-this-section"></a>このセクションで  
  
-   [OU 設計の概念を確認します。](../../ad-ds/plan/Reviewing-OU-Design-Concepts.md)  
  
-   [OU オブジェクトを使用して管理を委任します。](../../ad-ds/plan/Delegating-Administration-by-Using-OU-Objects.md)  
  


