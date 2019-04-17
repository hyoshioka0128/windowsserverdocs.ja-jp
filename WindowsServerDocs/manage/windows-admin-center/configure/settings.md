---
title: 設定
description: Windows Admin Center (Project Honolulu) の設定について説明します。 ユーザーの設定では、ユーザーがその言語/地域およびその他の設定を変更できるようにします。 ゲートウェイの設定では、管理者は、ゲートウェイを構成することができます。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d67a2c743900792353141186112cd09dbf780309
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296624"
---
# Windows Admin Center の設定

> Windows Admin Center の適用対象:

Windows Admin Center の設定は、ユーザー レベルとゲートウェイ レベルの設定で構成されます。 ユーザー レベルの設定の変更では、ゲートウェイ レベルの設定の変更は、Windows Admin Center ゲートウェイ上のすべてのユーザーに影響中に、現在のユーザーのプロファイルのみ影響します。

## ユーザーの設定

ユーザー レベルの設定では、次のセクションで構成されます。

- Account
- Personalization
- 言語/地域
- おすすめ
- 詳細

[**アカウント**] タブで、ユーザーが Windows Admin Center への認証に使用がそれらの資格情報を確認できます。 Azure AD が id プロバイダーに構成されている場合は、ユーザーがこのタブで、Azure AD アカウントからログインできます。

**[パーソナル設定]** タブで、ユーザーは、濃色 UI テーマに切り替えることができます。

**言語/地域**] タブで、ユーザーは、Windows Admin Center で表示される言語と地域の形式を変更できます。

[**候補**] タブで、ユーザーは Azure サービスと新しい機能に関する提案を切り替えることができます。

**詳細設定**] タブは、追加の機能を Windows Admin Center 拡張機能の開発者に提供します。

## ゲートウェイの設定

ゲートウェイ レベルの設定では、次のセクションで構成されます。

- 拡張機能
- Access
- Azure
- 共有接続

ゲートウェイ管理者のみを確認し、これらの設定を変更できます。 これらの設定への変更は、ゲートウェイの構成を変更し、Windows Admin Center ゲートウェイのすべてのユーザーに影響します。

**拡張機能**] タブで、管理者できますインストール、アンインストール、またはゲートウェイの拡張機能を更新します。 [拡張機能について説明します。](using-extensions.md)

**アクセス**] タブには、管理者のユーザーを認証するために使用する id プロバイダーと同様に、Windows Admin Center ゲートウェイにアクセスできるユーザーを構成することができます。 [ゲートウェイへのアクセスを制御することについて説明します。](user-access-control.md)

**Azure** ] タブで、管理者は、Azure を Windows Admin Center での[Azure 統合機能](azure-integration.md)を有効にすると、ゲートウェイを登録できます。

**共有の接続**] タブを使用して、管理者は、Windows Admin Center ゲートウェイのすべてのユーザー間で共有への接続の 1 つの一覧を構成できます。 [ゲートウェイのすべてのユーザーに対して 1 回の接続の構成について説明します。](shared-connections.md)