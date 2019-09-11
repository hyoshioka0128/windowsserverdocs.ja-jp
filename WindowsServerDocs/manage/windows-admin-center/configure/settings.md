---
title: 設定
description: Windows 管理センター (Project ホノルル) での設定について説明します。 ユーザー設定を使用すると、ユーザーは言語や地域などの設定を変更できます。 ゲートウェイの設定により、管理者はゲートウェイを構成できます。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: e184064aa913bf4fb18cadd8ddbb08b5b97c59c6
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865322"
---
# <a name="windows-admin-center-settings"></a>Windows 管理センターの設定

> 適用先:Windows Admin Center

Windows 管理センターの設定は、ユーザーレベルとゲートウェイレベルの設定で構成されています。 ユーザーレベルの設定を変更しても、現在のユーザーのプロファイルにのみ影響します。一方、ゲートウェイレベルの設定を変更すると、その Windows 管理センターゲートウェイのすべてのユーザーに影響します。

## <a name="user-settings"></a>ユーザー設定

ユーザーレベルの設定は、次のセクションで構成されています。

- アカウント
- Personalization
- 言語/地域
- おすすめ
- 詳細設定

**[アカウント]** タブでは、ユーザーは Windows 管理センターでの認証に使用した資格情報を確認できます。 Azure AD が id プロバイダーとして構成されている場合、ユーザーはこのタブから Azure AD アカウントからログアウトできます。

**[個人用設定]** タブでは、ユーザーはダーク UI テーマに切り替えることができます。

**[言語/地域]** タブでは、ユーザーは Windows 管理センターで表示される言語と地域の形式を変更できます。

**[提案]** タブで、ユーザーは Azure サービスと新機能に関する提案を切り替えることができます。

**[詳細設定**] タブでは、Windows 管理センターの拡張機能の開発者は追加の機能を使用できます。

## <a name="gateway-settings"></a>ゲートウェイの設定

ゲートウェイレベルの設定は、次のセクションで構成されています。

- 拡張機能
- アクセス
- Azure
- 共有接続

これらの設定を表示および変更できるのは、ゲートウェイ管理者だけです。 これらの設定を変更すると、ゲートウェイの構成が変更され、Windows 管理センターゲートウェイのすべてのユーザーに影響します。

管理者は、 **[拡張]** タブでゲートウェイ拡張機能をインストール、アンインストール、または更新できます。 [拡張機能の詳細についてはこちらをご覧ください。](using-extensions.md)

**[アクセス]** タブでは、管理者は Windows 管理センターゲートウェイにアクセスできるユーザーと、ユーザーの認証に使用する id プロバイダーを構成できます。 [ゲートウェイへのアクセス制御の詳細については、こちらを参照してください。](user-access-control.md)

管理者は、 **[azure]** タブからゲートウェイを azure に登録して、Windows 管理センターで[azure 統合機能](azure-integration.md)を有効にすることができます。

管理者は、 **[共有接続]** タブを使用して、Windows 管理センターゲートウェイのすべてのユーザー間で共有する1つの接続の一覧を構成できます。 [ゲートウェイのすべてのユーザーに対して接続を1回構成する方法の詳細については、こちらをご覧ください。](shared-connections.md)