---
title: 設定
description: Windows Admin Center (プロジェクト ホノルル) の設定について説明します。 ユーザー設定では、ユーザーの言語/地域およびその他の設定を変更できるようにします。 ゲートウェイの設定は、管理者は、ゲートウェイの構成を使用できます。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 1e1231500733f70ddfcbd4f8a847047b73f24a00
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882383"
---
# <a name="settings"></a>設定

> 適用先:Windows Admin Center

Windows Admin Center の設定は、ユーザー レベルおよびゲートウェイのレベルの設定で構成されます。 ユーザー レベルの設定の変更では、Windows Admin Center ゲートウェイ上のすべてのユーザーに影響を与えますゲートウェイ レベル設定に変更中に現在のユーザーのプロファイルのみ影響します。

## <a name="user-settings"></a>ユーザー設定

ユーザー レベルの設定は、次のセクションで構成されます。

- アカウント
- 言語/地域
- おすすめ

**アカウント** タブで、ユーザーには、Windows Admin Center の認証に使用した資格情報を確認できます。 Azure AD は、id プロバイダーとして構成されている場合、ユーザーがこのタブから、Azure AD アカウントからログインできます。

**言語/地域** タブで、ユーザーは、Windows Admin Center で表示される言語と地域の形式を変更できます。

**提案** タブで、ユーザーが Azure サービスと新機能に関する提案を切り替えることができます。

### <a name="dark-theme"></a>ダーク テーマ

> 適用先:Windows Admin Center Preview

Windows Admin Center プレビューでロックを解除できる追加**パーソナル化**セクションでは、ダーク UI テーマを切り替えるオプションが含まれています。 有効にする、**パーソナル化**セクションに、入力```msft.sme.shell.personalization```実験キーとして。

>[!IMPORTANT]
> ダーク テーマは進行中の作業で、この時点でバグを報告してください。

## <a name="gateway-settings"></a>ゲートウェイの設定

ゲートウェイのレベルの設定は、次のセクションで構成されます。

- 拡張機能
- アクセス権
- Azure

ゲートウェイの管理者のみが表示およびこれらの設定を変更できるようにします。 これらの設定を変更は、ゲートウェイの構成を変更し、Windows Admin Center ゲートウェイのすべてのユーザーに影響します。

**拡張** タブで、管理者は、インストール、アンインストール、またはゲートウェイの拡張機能を更新します。 [拡張機能について説明します。](using-extensions.md)

**アクセス** タブで管理者ユーザーを認証するために使用する id プロバイダーと同様に、Windows Admin Center ゲートウェイにアクセスできるユーザーを構成できます。 [ゲートウェイへのアクセス制御について説明します。](user-access-control.md)

**Azure**  タブで、管理者はゲートウェイを Azure に登録を有効にするのに[Azure との統合機能](azure-integration.md)Windows Admin Center でします。