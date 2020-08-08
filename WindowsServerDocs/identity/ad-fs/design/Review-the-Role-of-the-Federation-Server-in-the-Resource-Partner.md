---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: リソース パートナー内のフェデレーション サーバーの役割を確認する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: b090384cebd5213ec10799f4b2c0d594de3a3fd6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972069"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>リソース パートナー内のフェデレーション サーバーの役割を確認する

リソースパートナー組織のフェデレーションサーバーは、アカウントフェデレーションサーバーによって送信された受信セキュリティトークンをインターセプトし、検証して署名した後、Web ベースのアプリケーション用の独自のセキュリティトークンを発行し \- ます。

> [!NOTE]
> フェデレーションユーザーが web ブラウザーを使用して Web ベースのアプリケーションにアクセスすると \- 、リソースパートナー組織のフェデレーションサーバーは新しい認証クッキーを作成し、ブラウザーに書き込みます。 この cookie はシングル \- サイン \- オン \( SSO 機能を有効に \) します。これにより、ユーザーが \- リソースパートナー内の別の Web ベースアプリケーションにアクセスしようとしたときに、アカウントパートナーのフェデレーションサーバーでユーザーが再度ログオンする必要がなくなります。

Web SSO 設計では、少なくとも1つのフェデレーションサーバーが境界ネットワークにインストールされている必要があります。 フェデレーション Web SSO 設計では、アカウントパートナー組織の企業ネットワークに少なくとも1つのフェデレーションサーバーがインストールされ、リソースパートナー組織の企業ネットワークに少なくとも1つのフェデレーションサーバーがインストールされている必要があります。

> [!NOTE]
> リソースパートナー組織でフェデレーションサーバーコンピューターをセットアップする前に、まず、そのコンピューターをリソースパートナー組織内の任意の Active Directory ドメインに参加させる必要があります。 詳細については、「 [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)」を参照してください。

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)

