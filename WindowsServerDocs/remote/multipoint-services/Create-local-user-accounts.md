---
title: ローカル ユーザー アカウントを作成します。
description: MultiPoint Services での3種類のユーザーアカウントについて説明します。
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 33321932-4266-4961-9924-2cb4620bfcb4
author: evaseydl
ms.author: evas
manager: scottman
ms.openlocfilehash: d13ea5e6d28e6d4574f888aa30f257ec1fe3fe04
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942481"
---
# <a name="create-local-user-accounts"></a>ローカル ユーザー アカウントを作成します。
では、MultiPoint マネージャーを使用して、次の3つのレベルのローカルユーザーアカウントを作成できます。標準ユーザーアカウントMultiPoint ダッシュボードユーザーは、管理者権限が制限されています。および完全な管理ユーザーアカウント。

MultiPoint server でローカルユーザーアカウントを作成するには、次の手順に従います。 環境に複数の MultiPoint server が含まれており、ユーザーが任意のサーバー上の任意のステーションにログオンできるようにするには、各サーバーでローカルユーザーアカウントを作成する必要があります。 このセットアップにはいくつかの制限があります。 ドメイン環境では、ユーザーが自分のドメインアカウントを使用できるようにすることもできます。 オプションの概要については、「 [Windows MultiPoint Services 環境のユーザーアカウントを計画](Plan-user-accounts-for-your-MultiPoint-services-environment.md)する」を参照してください。

1.  管理者としてサーバーにログオンし、MultiPoint マネージャーを開きます。

2.  [**ユーザー** ] タブをクリックし、[**ユーザーアカウントの追加**] をクリックします。

    ユーザーアカウントの追加ウィザードが開きます。

3.  新しいユーザーアカウントのアカウント名とパスワードを入力し、[**次へ**] をクリックします。

4.  作成するユーザーアカウントの種類を選択します。

    -   **標準ユーザー** -ステーションにログオンしてユーザータスクを実行できますが、multipoint マネージャーまたは Multipoint Server ダッシュボードへのアクセス権がないため、システムをシャットダウンできません。

    -   **MultiPoint ダッシュボードユーザー** -管理者権限が制限されています。 ダッシュボードユーザーは、ダッシュボードを開き、システムからのユーザーのログ記録や MultiPoint Server コンピューターのシャットダウンなどのタスクを実行できますが、ユーザーには MultiPoint マネージャーへのアクセス権がありません。

    -   **管理ユーザー**には、MultiPoint Server の完全な管理者権限があります。 たとえば、管理ユーザーは、MultiPoint マネージャーを実行したり、ユーザーを追加および削除したり、システム設定を変更したり、ドライバーを更新したりできます。

5.  [**次へ**] をクリックし、[**完了**] をクリックしてユーザーアカウントを作成します。