---
ms.assetid: d8e61aa4-8e4b-4097-83ca-70cf61366b75
title: OU オブジェクトを使用して管理を委任する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 39c4278270e4ab4fba9ff1062d2aa043d203a74b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886943"
---
# <a name="delegating-administration-by-using-ou-objects"></a>OU オブジェクトを使用して管理を委任する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

指定した個人またはグループに OU 内のユーザーやコンピューターなどのオブジェクトの管理を委任するのに組織単位 (Ou) を使用できます。 OU を使用して管理を委任するに個人またはグループに管理者権限を委任する先のグループに配置し、ou に制御するオブジェクトのセットを配置し、そのグループに OU の管理タスクを委任します。  
  
Active Directory Domain Services (AD DS) では、非常に詳細なレベルでの委任可能な管理タスクを制御することができます。 たとえば、; OU 内のすべてのオブジェクトのフル コントロールに 1 つのグループを割り当てることができます。別のグループの作成、削除、および OU; 内のユーザー アカウントの管理にのみ権限を割り当てる割り当て 3 グループ化して権限がユーザー アカウントのパスワードのリセットのみです。 行うことができますこれらのアクセス許可継承可能な元の OU のサブツリーに配置されているすべての Ou に適用されるようにします。  
  
既定の Ou とコンテナーは、AD DS のインストール中に作成され、サービス管理者によって制御されます。 これらのコンテナーを制御するサービス管理者の続行を用意することをお勧めします。 ディレクトリ内のオブジェクトの制御を委任する必要がある場合は、追加の Ou を作成し、これらの Ou に、オブジェクトを配置します。 適切なデータ管理者には、これらの Ou の制御を委任します。 これにより、サービス管理者に指定された既定のコントロールを変更することがなく、ディレクトリ内のオブジェクトの制御を委任します。  
  
フォレストの所有者は、組織単位の所有者に委任された権限のレベルを決定します。 機能を作成し、OU 内のオブジェクトの 1 つの型の 1 つの属性の制御のみ許可されている OU 内のオブジェクトを操作する範囲で指定できます。 暗黙的に、OU 内のオブジェクトを作成する機能をユーザーに与えることと、ユーザーを作成する任意のオブジェクトのすべての属性を操作する権限、そのユーザーが付与されます。 さらに、作成されるオブジェクトが、コンテナーの場合は、ユーザーは暗黙的に作成し、コンテナーに配置されているすべてのオブジェクトを操作する機能を持ちます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [既定のコンテナーと Ou の管理を委任します。](../../ad-ds/plan/Delegating-Administration-of-Default-Containers-and-OUs.md)  
  
-   [アカウント Ou とリソース Ou の管理を委任します。](../../ad-ds/plan/Delegating-Administration-of-Account-OUs-and-Resource-OUs.md)  
  


