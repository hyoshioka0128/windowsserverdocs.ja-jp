---
title: 独自の新しいフォレストで、または既存の要塞フォレスト内では、HGS をインストールするかどうかを選択します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 4e02cd37391e629c9b947095fe32626bd15726ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827503"
---
# <a name="choose-whether-to-install-hgs-in-its-own-dedicated-forest-or-in-an-existing-bastion-forest"></a>独自の専用フォレストで、または既存の要塞フォレスト内では、HGS をインストールするかどうかを選択します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016


HGS の Active Directory フォレストは、その管理者はコントロールにシールドされた Vm のキーにアクセスするために機密性の高い。 既定のインストールを設定する新しいフォレスト専用 HGS を他の依存関係を構成します。 このオプションは、環境は自己完結型であるために、推奨され、既知の作成時に、セキュリティで保護します。 

HGS を既存のフォレストにインストールするためだけに技術的な要件は、ルート ドメインに追加することルート以外のドメインがサポートされていません。 運用要件と既存のフォレストを使用するためのセキュリティ関連のベスト プラクティスもがあります。 使用されるフォレストなどの 1 つの重要な機能を処理するために適切なフォレストが組み込まれて意図的に[AD DS の Privileged Access Management](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services)または[Enhanced Security Administrative Environment (ESAE) フォレスト](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access-reference-material#ESAE_BM). 通常、このようなフォレストが、次の特性があります。

- いくつかの管理者 (ファブリック管理者から独立した) があります。
- ログオンの数が少ないがあります。
- 汎用本質的には 

実稼働フォレストなどの一般的な用途のフォレストでは、HGS が使用には適しません。 Fabric フォレスト適さないも HGS がファブリック管理者から分離する必要があるためです。

## <a name="next-step"></a>次の手順

お客様の環境に最適なインストール オプションを選択します。

- [独自の専用フォレストでの HGS をインストールします。](guarded-fabric-install-hgs-default.md)
- [既存の要塞フォレスト内での HGS をインストールします。](guarded-fabric-install-hgs-in-a-bastion-forest.md)


