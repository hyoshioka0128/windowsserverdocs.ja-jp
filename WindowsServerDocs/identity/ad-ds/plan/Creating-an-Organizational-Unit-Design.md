---
ms.assetid: b8df1828-5ead-4c90-b0fe-95c675116b7c
title: 組織単位の設計を作成する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9ecd0228b50a4e597c3fa1dbd3fdaf1f84ca1d3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830403"
---
# <a name="creating-an-organizational-unit-design"></a>組織単位の設計を作成する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

フォレストの所有者とは、それらのドメインの組織単位 (OU) の設計を作成する責任を負います。 OU 設計を作成するには、OU の所有者ロール、および作成するアカウントとリソース Ou を割り当て、OU 構造を設計する必要があります。  
  
最初に、管理の委任を有効にする OU 構造を設計します。 OU 設計が完了したら、ユーザーとコンピューターに、オブジェクトの可視性を制限するグループ ポリシーのアプリケーションの追加の OU 構造を作成できます。 詳細については、グループ ポリシー インフラストラクチャの設計を参照してください ([https://go.microsoft.com/fwlink/?LinkId=106655](https://go.microsoft.com/fwlink/?LinkId=106655))。  
  
## <a name="ou-owner-role"></a>OU の所有者のロール  
フォレストの所有者は、各 OU 設計では、ドメインの OU 所有者を指定します。 OU の所有者は、データ管理者が Active Directory Domain Services (AD DS) 内のオブジェクトのサブツリーを制御します。 OU の所有者には、管理を委任する方法と、その OU 内のオブジェクトにポリシーを適用する方法を制御できます。 新しいサブツリーを作成し、そのサブツリー内の Ou の管理を委任することもできます。  
  
OU の所有者が所有または、ディレクトリ サービスの動作の制御はいない、ためから分離できます所有権とディレクトリ サービスの管理所有権と管理、オブジェクトの高レベルを持つサービス管理者の数を減らすアクセス。  
  
Ou は、自律的な管理とディレクトリ内のオブジェクトの表示を制御するための手段を提供します。 Ou が他のデータ管理者からの分離を提供しますが、サービス管理者からの分離は提供されません。 OU の所有者には、オブジェクトのサブツリーに制御がありますが、フォレストの所有者は、すべてのサブツリーを完全に制御を保持します。 これにより、フォレストの所有者のアクセス制御リスト (ACL) エラーなどの誤りを修正し、データ管理者が終了した場合に、委任されたサブツリーを再利用します。  
  
## <a name="account-ous-and-resource-ous"></a>アカウント Ou とリソース Ou  
アカウント Ou には、ユーザー、グループ、およびコンピューター オブジェクトが含まれます。 フォレストの所有者は、これらのオブジェクトを管理し、OU の所有者に、構造の制御を委任し、OU 構造を作成する必要があります。 新しい AD DS ドメインを展開する場合は、ドメイン内のアカウントの制御を委任できるように、OU、ドメインのアカウントを作成します。  
  
リソース Ou には、リソースとそれらのリソースを管理する責任を持っているアカウントが含まれます。 フォレストの所有者は、これらのリソースを管理する OU 構造を作成して、OU の所有者にその構造の制御を委任するための責任もあります。 リソース作成 Ou に応じてのデータおよび設備の管理を自律的に、組織内のグループごとの要件に基づいてください。  
  
## <a name="documenting-the-ou-design-for-each-domain"></a>各ドメインの OU 設計を文書化  
フォレスト内のリソースの制御を委任するために使用する OU 構造を設計するチームを編成します。 フォレストの所有者は、設計プロセスに関連する可能性があり、OU 設計を承認する必要があります。 デザインが有効であることを確認するには少なくとも 1 つのサービス管理者もあります。 設計チームの他の参加者には、ユーザーはそれらの管理を担当する所有者 Ou と、OU で作業するデータ管理者が含まれます。  
  
OU 設計を文書化に重要です。 作成する予定の Ou の名前を一覧表示します。 また、各 OU では、OU、OU の所有者、親 (該当する) 場合は、OU、および OU の配信元の型を文書化します。  
  
OU 設計を文書化するために、ワークシートでは、ジョブ エイドの Windows Server 2003 展開キットから Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードして ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) を開くと"各ドメインの Ou を特定する"(DSSLOGI_9.doc)。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [OU 設計の概念を確認します。](../../ad-ds/plan/Reviewing-OU-Design-Concepts.md)  
  
-   [OU オブジェクトを使用して管理を委任します。](../../ad-ds/plan/Delegating-Administration-by-Using-OU-Objects.md)  
  


