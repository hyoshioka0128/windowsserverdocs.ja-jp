---
ms.assetid: d8e61aa4-8e4b-4097-83ca-70cf61366b75
title: OU オブジェクトを使用して管理を委任する
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: af13896c07c10710be6e087be5d31dbd4aec698f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822715"
---
# <a name="delegating-administration-by-using-ou-objects"></a>OU オブジェクトを使用して管理を委任する

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

組織単位 (Ou) を使用して、OU 内のユーザーやコンピューターなどのオブジェクトの管理を、指定された個人またはグループに委任することができます。 OU を使用して管理を委任するには、管理権限を委任する個人またはグループをグループに配置し、管理対象のオブジェクトのセットを OU に配置して、OU の管理タスクをそのグループに委任します。  
  
Active Directory Domain Services (AD DS) を使用すると、非常に詳細なレベルで委任できる管理タスクを制御できます。 たとえば、OU 内のすべてのオブジェクトに対してフルコントロールを持つ1つのグループを割り当てることができます。OU 内のユーザーアカウントを作成、削除、および管理するための権限のみを別のグループに割り当てます。次に、3番目のグループに、ユーザーアカウントのパスワードをリセットする権限を割り当てます。 元の OU のサブツリーに配置されている Ou に適用されるように、これらのアクセス許可を継承可能にすることができます。  
  
既定の Ou とコンテナーは、AD DS のインストール時に作成され、サービス管理者によって制御されます。 サービス管理者がこれらのコンテナーを引き続き制御する場合は、この方法をお勧めします。 ディレクトリ内のオブジェクトに対する制御を委任する必要がある場合は、追加の Ou を作成し、それらの Ou にオブジェクトを配置します。 これらの Ou に対する制御を適切なデータ管理者に委任します。 これにより、サービス管理者に与えられている既定のコントロールを変更することなく、ディレクトリ内のオブジェクトに対する制御を委任できます。  
  
フォレスト所有者は、OU 所有者に委任される機関のレベルを決定します。 これは、ou 内のオブジェクトを作成および操作する機能から、OU 内の1つの型のオブジェクトの1つの属性のみを制御できるようにする場合があります。 OU にオブジェクトを作成する権限をユーザーに付与すると、ユーザーが作成した任意のオブジェクトの任意の属性を操作できるようになります。 また、作成されたオブジェクトがコンテナーである場合、ユーザーは、コンテナーに配置されているすべてのオブジェクトを暗黙的に作成および操作することができます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [既定のコンテナーと OU の管理を委任する](../../ad-ds/plan/Delegating-Administration-of-Default-Containers-and-OUs.md)  
  
-   [アカウント OU とリソース OU の管理を委任する](../../ad-ds/plan/Delegating-Administration-of-Account-OUs-and-Resource-OUs.md)  
  


