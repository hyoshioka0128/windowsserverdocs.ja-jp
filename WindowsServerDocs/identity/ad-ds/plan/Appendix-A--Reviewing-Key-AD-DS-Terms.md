---
ms.assetid: 87196b65-a356-409f-9af0-b5950797d668
title: 付録 A - 重要な AD DS の用語の確認
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5434db4124c471c613f159dec28e27dee70e7086
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852023"
---
# <a name="appendix-a-reviewing-key-ad-ds-terms"></a>付録 A:重要な AD DS の用語を確認します。

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

次の用語は、Windows Server 2008 Active Directory Domain Services (AD DS) の展開プロセスに関連します。  
  
## <a name="active-directory-domain"></a>Active Directory ドメイン  
管理の利便性のため、次を含む、いくつかの機能をグループ化するコンピューター ネットワークでの管理単位:  
  
-   **ネットワーク全体のユーザー id**します。 ドメインでは、ユーザー id を 1 回作成およびドメインが配置されているフォレストに参加している任意のコンピューターで参照されます。 ドメインを構成するドメイン コント ローラーは、ユーザー アカウントとパスワードまたは証明書など、ユーザーの資格情報を安全に格納します。  
  
-   **認証**。 ドメイン コント ローラーは、ユーザーの認証サービスを提供します。 また、ユーザー グループ メンバーシップなど、追加の承認データを指定します。 管理者は、これらのサービスを使用して、ネットワーク上のリソースへのアクセスを制御することができます。  
  
-   **信頼関係**します。 ドメインは、自動双方向の信頼を使用して、独自のフォレストの他のドメイン内のユーザーに認証サービスを拡張します。 ドメインも、フォレスト信頼または外部の信頼を手動で作成したのかを使用して、他のフォレスト内のドメイン内のユーザーに認証サービスを拡張します。  
  
-   **ポリシーの管理**します。 パスワードの複雑さとパスワードは、ルールを再利用など、ドメイン管理のポリシーのスコープとは。  
  
-   **レプリケーション**。 ドメインは、必要なサービスを提供するための適切なドメイン コント ローラー間でレプリケートされるデータを提供するディレクトリ ツリーのパーティションを定義します。 これにより、すべてのドメイン コント ローラーは、ドメイン内のピアとの単位として管理されています。  
  
## <a name="active-directory-forest"></a>Active Directory フォレスト  
自動、双方向で推移的な信頼関係に加え、共通の論理構造、ディレクトリ スキーマ、およびネットワークの構成を共有する 1 つまたは複数の Active Directory ドメインのコレクション。 各フォレストは、ディレクトリの 1 つのインスタンスと、セキュリティの境界を定義します。  
  
## <a name="active-directory-functional-level"></a>Active Directory 機能レベル  
設定を AD DS では、ドメイン全体またはフォレスト全体の高度な AD DS 機能できるようにします。  
  
## <a name="migration"></a>Migration  
保持または新しいドメインにアクセスできるようにするオブジェクトの特性の変更中に、ターゲット ドメインにソース ドメインからオブジェクトを移動するプロセス。  
  
## <a name="domain-restructure"></a>ドメインの再構築  
移行のプロセスで、フォレストのドメイン構造を変更する必要があります。 ドメインの再構築は、統合や、ドメインの追加のいずれかが含まれることができ、フォレスト間またはフォレスト内の場所がかかることができます。  
  
## <a name="domain-consolidation"></a>ドメインの統合  
再構築プロセスの他のドメインの内容とその内容をマージすることで、AD DS ドメインを排除することです。  
  
## <a name="domain-upgrade"></a>ドメインのアップグレード  
以降のバージョンのディレクトリ サービスにドメインのディレクトリ サービスをアップグレードするプロセス。 これには、すべてのドメイン コント ローラー上のオペレーティング システムをアップグレードして、該当する場合は、AD DS の機能レベルを上げるが含まれます。  
  
## <a name="in-place-domain-upgrade"></a>ドメインのインプレース アップグレード  
たとえば、指定されたドメイン内のすべてのドメイン コント ローラーのオペレーティング システムをアップグレードに Windows Server 2008、Windows Server 2003 をアップグレードしてユーザーなどのドメイン オブジェクトはそのまま該当する場合に、ドメインの機能レベルを上げるのプロセスグループ、場所にします。  
  
## <a name="forest-root-domain"></a>フォレスト ルート ドメイン  
最初のドメインを Active Directory フォレストに作成されます。 このドメインは、フォレスト ルート ドメインとして自動的に指定します。 Active Directory フォレストのインフラストラクチャの基盤を提供します。  
  
## <a name="regional-domain"></a>地域別のドメイン  
レプリケーション トラフィックを最適化するために地理的リージョンに作成される子ドメインを指定します。  
  


