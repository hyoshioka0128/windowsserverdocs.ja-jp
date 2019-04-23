---
ms.assetid: ac6604b0-7459-4ff3-af1c-4936897f5d14
title: 既定のコンテナーと OU の管理を委任する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9d482854fd82b4bf0d0e61315d36e6222470ca55
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830893"
---
# <a name="delegating-administration-of-default-containers-and-ous"></a>既定のコンテナーと OU の管理を委任する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

すべての Active Directory ドメインには、コンテナーと Active Directory Domain Services (AD DS) のインストール中に作成された組織単位 (Ou) の標準セットが含まれています。 これには次のものがあります。  
  
-   階層にルート コンテナーとして機能するドメイン コンテナー  
  
-   サービス管理者アカウントの既定値を保持する、組み込みのコンテナー  
  
-   ドメインに新しいユーザー アカウントとグループの既定の場所は、[ユーザー] コンテナーを作成  
  
-   新しいコンピューター アカウントの既定の場所である computers コンテナーがドメインに作成  
  
-   ドメイン コント ローラー コンピューター アカウント用のコンピューター アカウントの既定の場所であるドメイン コント ローラー OU  
  
フォレストの所有者は、これらの既定のコンテナーと Ou を制御します。  
  
## <a name="domain-container"></a>ドメイン コンテナー  
ドメインのコンテナーは、ドメインの階層のルート コンテナーです。 ポリシーまたはこのコンテナーのアクセス制御リスト (ACL) への変更は、ドメイン全体に影響を持つことがあります。 このコンテナーの制御を委任しなかったこれは、サービス管理者によって制御する必要があります。  
  
## <a name="users-and-computers-containers"></a>ユーザーとコンピューターのコンテナー  
Windows Server 2003 から Windows Server 2008 にドメインのインプレース アップグレードを実行するときに既存のユーザーとコンピューターは、ユーザーとコンピューターのコンテナーに自動的に配置します。 作成する場合は、すべての新しいユーザー アカウントとドメイン内の非ドメイン コント ローラー コンピューター アカウントの既定の場所が、新しい Active Directory ドメイン、ユーザーとコンピューター コンテナー。  
  
> [!IMPORTANT]  
> ユーザーまたはコンピューターの制御を委任する必要がある場合、ユーザーとコンピューターの既定の設定は変更しないでくださいコンテナー。 代わりに、(必要に応じて) 新しい Ou を作成し、その既定のコンテナーから新しい Ou にユーザーとコンピューター オブジェクトを移動します。 必要に応じては、新しい Ou の制御を委任します。 変更しないで、既定のコンテナーを制御することをお勧めします。  
  
また、既定のユーザーとコンピューターにグループ ポリシー設定を適用することはできませんのコンテナー。 ユーザーとコンピューターには、グループ ポリシーを適用するには、新しい Ou を作成し、それらの Ou にユーザーとコンピューター オブジェクトを移動します。 新しい Ou にグループ ポリシー設定を適用します。  
  
必要に応じて、好みのコンテナーに配置する既定のコンテナーに配置されるオブジェクトの作成をリダイレクトできます。  
  
## <a name="well-known-users-and-groups-and-built-in-accounts"></a>既知のユーザーとグループ、および組み込みのアカウント  
既定では、いくつかのよく知られているユーザーとグループ、および組み込みアカウントは、新しいドメインで作成されます。 これらのアカウントの管理はサービス管理者の管理下にあることをお勧めします。 サービス管理者ではない個人にこれらのアカウントの管理を委任できません。 次の表には、よく知られているユーザーとグループ、サービス管理者の制御下に必要な組み込みアカウントが一覧表示します。  
  
|既知のユーザーとグループ|ビルトイン アカウント|  
|--------------------------------|----------------------|  
|Cert Publishers<br /><br />ドメイン コントローラー<br /><br />Group Policy Creator Owners<br /><br />KRBTGT<br /><br />ドメインのゲスト<br /><br />管理者<br /><br />Domain Admins<br /><br />スキーマ管理者 (フォレスト ルート ドメインのみ)<br /><br />Enterprise Admins (フォレスト ルート ドメインのみ)<br /><br />ドメイン ユーザー|管理者<br /><br />Guest<br /><br />Guests<br /><br />Account Operators<br /><br />管理者<br /><br />Backup Operators<br /><br />入力方向のフォレスト信頼ビルダー<br /><br />Print Operators<br /><br />Pre-Windows 2000 Compatible Access<br /><br />Server Operators<br /><br />Users|  
  
## <a name="domain-controller-ou"></a>ドメイン コント ローラーの OU  
ドメイン コント ローラーがドメインに追加されると、コンピューター オブジェクトに、自動的にドメイン コント ローラーの OU に追加されます。 この OU には、それに適用されるポリシーの既定セットがあります。 これらのポリシーがすべてのドメイン コント ローラーに一様に適用されることを確認しないこの OU からドメイン コント ローラーのコンピューター オブジェクトを移動することをお勧めします。 既定のポリシーの適用に失敗には、ドメイン コント ローラーが正常に機能するが失敗する可能性があります。  
  
既定では、サービス管理者は、この OU を制御します。 サービス管理者以外のユーザーにこの OU の制御を委任できません。  
  


