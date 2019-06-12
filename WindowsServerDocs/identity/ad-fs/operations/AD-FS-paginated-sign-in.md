---
title: AD FS がサインインに改ページ調整されました。
description: このドキュメントでは、AD FS 2019 の新しいサインイン エクスペリエンスについて説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c528b9c4e944849b7ed9a2fc5213a7b263be70c7
ms.sourcegitcommit: ccc802338b163abdad2e53b55f39addcfea04603
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2019
ms.locfileid: "66687379"
---
# <a name="ad-fs-paginated-sign-in"></a>AD FS がサインインに改ページ調整されました。


Windows Server 2019、AD FS のサインイン UI 再設計しました。  ここで、AD FS サインインは、Azure AD の同じのルック アンド フィールがあります。  ユーザーより一貫したサインイン エクスペリエンスを中央揃えと改ページ調整されたユーザー フローを組み込むこれ提供されます。

## <a name="whats-changing"></a>変更点
Windows Server 2012 R2 および 2016 の AD FS では、サインイン画面は、このようなものを検索しました。

![oldsignin](media/AD-FS-paginated-sign-in/signin1.png)

画面の右側にある 1 つのフォームを表示するからに移行します。

Windows Server 2019、AD FS では、表示される主要な設計の変更。


- **A UI を中央揃え**します。 以前は、上記には、画面の右側にあるサインイン UI が存在しています。 UI の前面と経験を近代化するセンター移行しました。
- **改ページ調整**します。 長い形式の入力を提供する、代わりにステップ バイ ステップのエクスペリエンスにサインインを実行する新しいフローを反映します。 利用統計情報は、この方法でのお客様があるより成功したサインインを示します。さまざまな認証方法、このような米国の電話要素認証を組み込む柔軟性も提供します。

![newsignin](media/AD-FS-paginated-sign-in/signin2.png)

最初のページでは、ユーザー名を入力を求め。 「サインインしたまま」するオプションを選択することも可能性があります。 サインイン プロンプトが表示の頻度を減らすと、これを行うには安全ではときにサインインしたままにします。 (このオプションは既定で無効です)。

![newsignin](media/AD-FS-paginated-sign-in/signin3.png)

2 番目のページでは、するは、管理者によって構成の認証オプションを使用して表示されます。 プライマリと外部の認証が有効になっている場合は、これが含まれますも。

![newsignin](media/AD-FS-paginated-sign-in/signin4.png)

3 番目のページでは、(と仮定すると"Password"を選択した認証オプションとして) パスワードの入力を求め。

## <a name="how-to-get-the-new-experience"></a>新しいエクスペリエンスを取得する方法

### <a name="new-installation-of-ad-fs"></a>AD FS の新しいインストール
AD FS に新しい顧客の場合は、既定では、新しいデザインを受け取ります。

### <a name="upgrading-a-farm"></a>ファームのアップグレード
既存の顧客の AD FS 2012 R2 または 2016 の場合は、2019年に FBL になり、AD FS 2019 にサーバーのアップグレード後に、新しいデザインを受信する 2 つの方法があります。

- Powershell を使用して新しいサインインできます。 改ページ調整を有効にするのには、次のコマンドを実行します。 ``Set-AdfsGlobalAuthenticationPolicy -EnablePaginatedAuthenticationPages $true``

 - Powershell を使用または AD FS サーバー マネージャーでは主として、外部の認証を有効にします。 この機能が有効にすると、ページの改ページ調整されたサインインを有効になります。
AD FS に新しい顧客の場合は、既定では、新しいデザインを受け取ります。 ただし、既存の顧客と AD FS 2012 R2 または 2016 の場合は、いくつかの手順を新しいデザインを受信する必要があります。 ``Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true``

## <a name="customization"></a>カスタマイズ
カスタマイズするためのオプションは、AD FS 2019 の適用されます。
参照用の他のドキュメントへのリンクを次に示します。

AD FS 2019 に、サーバーをアップグレードする予定がないせずに、新しいデザイン場合方のため •:[Active Directory フェデレーション サービスで Azure AD のユーザー エクスペリエンスの Web テーマを使用します。](azure-ux-web-theme-in-ad-fs.md)

• カスタマイズの中央の場所:[AD FS のユーザー サインインのカスタマイズ](ad-fs-user-sign-in-customization.md)
