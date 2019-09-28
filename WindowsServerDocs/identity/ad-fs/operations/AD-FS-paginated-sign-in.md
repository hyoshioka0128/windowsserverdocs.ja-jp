---
title: 改ページ調整されたサインインの AD FS
description: このドキュメントでは、AD FS 2019 の新しいサインインエクスペリエンスについて説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ca13ebe29b0a9260302599110f333d166681abdb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358563"
---
# <a name="ad-fs-paginated-sign-in"></a>改ページ調整されたサインインの AD FS


Windows Server 2019 の AD FS では、サインイン UI が再設計されました。  これで、AD FS のサインインのルックアンドフィールが Azure AD と同じになります。  これにより、ユーザーはより一貫したサインインエクスペリエンスを提供し、中央のユーザーフローと改ページ調整されたユーザーフローを組み込むことができます。

## <a name="whats-changing"></a>変更点
Windows Server 2012 R2 および2016の AD FS では、サインイン画面は次のようになります。

![oldsignin](media/AD-FS-paginated-sign-in/signin1.png)

画面の右側にある1つのフォームを表示しないようにしています。

Windows Server 2019 の AD FS では、次のような主な設計変更が表示されます。


- **中央の UI**。 以前は、上記のように、画面の右側にサインイン UI が存在していました。 UI フロントとセンターを移動して、エクスペリエンスを最新化しました。
- **ページ**割り当て。 長い形式のフォームを提供するのではなく、サインインエクスペリエンスを段階的に説明する新しいフローを導入しましたが、 製品利用統計情報は、このアプローチにより、お客様のサインインがより成功したことを示しています。また、米国の電話要因認証など、さまざまな認証方法を柔軟に組み込むことができます。

![newsignin](media/AD-FS-paginated-sign-in/signin2.png)

最初のページで、ユーザー名を入力するように求められます。 サインインプロンプトの頻度を下げ、安全にサインインしたままにしておくために、[サインインしたままにする] オプションを選択することもできます。 既定では、このオプションは無効になっています。

![newsignin](media/AD-FS-paginated-sign-in/signin3.png)

2番目のページには、管理者によって構成された認証オプションが表示されます。 [プライマリとして外部認証を許可する] が有効になっている場合は、これも含まれます。

![newsignin](media/AD-FS-paginated-sign-in/signin4.png)

3番目のページでは、パスワードを入力するように求められます (認証オプションとして [パスワード] を選択した場合)。

## <a name="how-to-get-the-new-experience"></a>新しいエクスペリエンスを得る方法

### <a name="new-installation-of-ad-fs"></a>AD FS の新規インストール
新しい顧客が AD FS する場合は、既定で新しいデザインを受け取ります。

### <a name="upgrading-a-farm"></a>ファームのアップグレード
既存の顧客 AD FS 2012 R2 または2016の場合は、サーバーを AD FS 2019 にアップグレードし、FBL を2019にするという2つの方法があります。

- Powershell を使用して新しいサインインを許可します。 次のコマンドを実行して、改ページ位置の自動修正を有効にします。``Set-AdfsGlobalAuthenticationPolicy -EnablePaginatedAuthenticationPages $true``

 - Powershell または AD FS サーバーマネージャーを使用して、外部認証をプライマリとして有効にします。 この機能を有効にすると、改ページ調整された新しいサインインページが有効になります。
新しい顧客が AD FS する場合は、既定で新しいデザインを受け取ります。 ただし、AD FS 2012 R2 または2016を使用している既存のお客様の場合、新しい設計を受けるにはいくつかの手順を実行する必要があります。``Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true``

## <a name="customization"></a>カスタマイズ
カスタマイズのオプションは、AD FS 2019 にも適用できます。
参照用の他のドキュメントへのリンクを次に示します。

•サーバーを AD FS 2019 にアップグレードする予定がなくても、新しい設計が必要な場合は、次のようになります。[Active Directory フェデレーションサービス (AD FS) での Azure AD UX Web テーマの使用](azure-ux-web-theme-in-ad-fs.md)

•カスタマイズのための一元的な場所:[AD FS のユーザー サインインのカスタマイズ](ad-fs-user-sign-in-customization.md)
