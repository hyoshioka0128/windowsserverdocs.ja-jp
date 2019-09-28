---
title: Azure 統合の構成
description: Azure 統合の構成 Windows 管理センター (Project ホノルル)。 Windows 管理センターゲートウェイを Azure に接続しています。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 448a8fb3e4340752b673b06f86d5d49211b6b147
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357363"
---
# <a name="configuring-azure-integration"></a>Azure 統合の構成

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センターでは、Azure サービスと統合されるいくつかのオプション機能がサポートされています。 [Windows 管理センターで利用できる Azure 統合オプションについて説明します。](../plan/azure-integration-options.md)

Windows 管理センターゲートウェイが Azure と通信して、ゲートウェイアクセスの Azure Active Directory 認証を利用したり、azure リソースをユーザーに代わって作成したりできるようにするには (たとえば、Azure サイトを使用して Windows 管理センターで管理されている Vm を保護する)回復) では、最初に Windows 管理センターゲートウェイを Azure に登録する必要があります。 これは、Windows 管理センターゲートウェイに対して1回だけ実行する必要があります。ゲートウェイを新しいバージョンに更新すると、設定が保持されます。

## <a name="register-your-gateway-with-azure"></a>Azure にゲートウェイを登録する

Windows 管理センターで Azure 統合機能を初めて使用しようとすると、Azure にゲートウェイを登録するように求められます。 Windows 管理センターの 設定 の  **Azure** タブに移動して、ゲートウェイを登録することもできます。

ガイド付きの製品内の手順に従って、ディレクトリに Azure AD アプリを作成します。これにより、Windows 管理センターが Azure と通信できるようになります。 自動的に作成された Azure AD アプリを表示するには、Windows 管理センターの設定 の  **Azure** タブにアクセスします。 **[Azure での表示]** ハイパーリンクを使用すると、Azure portal で Azure AD アプリを表示できます。 

作成された Azure AD アプリは、Windows 管理センターでの Azure 統合のすべてのポイント ([ゲートウェイへの Azure AD 認証](../configure/user-access-control.md#azure-active-directory)など) に使用されます。