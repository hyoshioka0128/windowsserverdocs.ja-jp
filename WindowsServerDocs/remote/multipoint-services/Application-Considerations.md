---
title: アプリケーションの考慮事項
description: MultiPoint Services でのアプリの互換性に関する情報
ms.topic: article
ms.assetid: 445e6184-4e1e-4f10-ad3c-042f2a6c2f5f
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: 6657e8d9f7c206cb5532eda3491af98f161ccb7a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944462"
---
# <a name="application-considerations"></a>アプリケーションの考慮事項

## <a name="application-compatibility"></a>アプリケーションの互換性

MultiPoint Services システム上で実行するすべてのアプリケーションは、次の要件を満たす必要があります。

- Windows Server 2016 にインストールして実行する必要があります。
- 各ユーザーが MultiPoint システムでアプリのインスタンスを実行できるように、セッションに対応している必要があります。

アプリケーションでこの要件が指定されている場合は、アプリケーションをインストールし、リモートデスクトップセッションで使用することをお勧めします。

## <a name="addressing-application-compatibility-problems"></a>アプリケーションの互換性の問題への対処
MultiPoint Services には、同じホストコンピューター上で実質的に実行されている Windows 10 Enterprise エディションの完全なインスタンスにステーションを関連付けるオプションが用意されています。 複数のユーザーに対して複数のインスタンスを実行しない重要なアプリケーションや、64ビットのオペレーティングシステムにインストールされない場合は、これが解決策になることがあります。 この方法でデスクトップを展開するには、MultiPoint マネージャーの [仮想デスクトップ] タブを使用して次のことを行う必要があります。

-   仮想デスクトップを有効にする
-   デスクトップテンプレートを作成する
-   問題アプリケーションを使用してテンプレートをカスタマイズする
-   カスタマイズしたテンプレートにステーションを関連付ける

各ステーションは同じテンプレートから開始されるので、コンピューターが起動するたびにすべての変更が消去されます。

>[!NOTE]
>MultiPoint で実行するアプリケーションのライセンス要件を確認することが重要です。 1つのコピーアプリケーションをインストールする場合でも、ユーザーごとのライセンスが必要になる場合があります。

