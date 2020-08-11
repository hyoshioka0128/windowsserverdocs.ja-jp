---
title: Settings
description: Windows Admin Center (Project Honolulu) の設定について説明します。 ユーザー設定を使用すると、ユーザーは言語や地域などの設定を変更できます。 ゲートウェイの設定により、管理者はゲートウェイを構成できます。
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: ff06a19d85858b8332412a51c029c9aeeba2af50
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997438"
---
# <a name="windows-admin-center-settings"></a>Windows Admin Center の設定

> 適用先:Windows Admin Center

Windows Admin Center の設定は、ユーザー レベルとゲートウェイ レベルの設定で構成されています。 ユーザー レベルの設定を変更しても、現在のユーザーのプロファイルにのみ影響します。一方、ゲートウェイ レベルの設定を変更すると、その Windows Admin Center ゲートウェイのすべてのユーザーに影響します。

## <a name="user-settings"></a>ユーザー設定

ユーザー レベルの設定は、次のセクションによって構成されています。

- アカウント
- 個人設定
- 言語/地域
- おすすめ
- [詳細設定]

**[アカウント]** タブで、ユーザーは Windows Admin Center での認証に使用した資格情報を確認できます。 Azure AD が ID プロバイダーとして構成されている場合、ユーザーはこのタブで Azure AD アカウントからログアウトできます。

**[個人設定]** タブでは、ユーザーはダーク UI テーマに切り替えることができます。

**[言語/地域]** タブでは、ユーザーは Windows Admin Center で表示される言語と地域の形式を変更できます。

**[おすすめ]** タブで、ユーザーは Azure サービスと新機能に関する提案を切り替えることができます。

**[詳細]** タブでは、Windows Admin Center の拡張機能の開発者が追加の機能を使用できます。

## <a name="gateway-settings"></a>ゲートウェイ設定

ゲートウェイ レベルの設定は、次のセクションによって構成されています。

- Extensions
- アクセス権
- Azure
- 共有接続

これらの設定を表示および変更できるのは、ゲートウェイ管理者だけです。 これらの設定を変更すると、ゲートウェイの構成が変更され、Windows Admin Center ゲートウェイのすべてのユーザーに影響します。

**[拡張機能]** タブでは、管理者はゲートウェイの拡張機能をインストール、アンインストール、または更新できます。 [拡張機能の詳細をご覧ください。](using-extensions.md)

**[アクセス]** タブでは、管理者は Windows Admin Center ゲートウェイにアクセスできるユーザーと、ユーザーの認証に使用する ID プロバイダーを構成できます。 [ゲートウェイへのアクセス制御の詳細については、こちらを参照してください。](user-access-control.md)

管理者は **[Azure]** タブからゲートウェイを Azure に登録して、Windows Admin Center で [Azure 統合機能](../azure/azure-integration.md)を有効にすることができます。

管理者は **[共有接続]** タブを使用して、Windows Admin Center ゲートウェイのすべてのユーザー間で共有する接続の一覧を構成できます。 [ゲートウェイのすべてのユーザーに対して接続をまとめて構成する方法の詳細については、こちらをご覧ください。](shared-connections.md)