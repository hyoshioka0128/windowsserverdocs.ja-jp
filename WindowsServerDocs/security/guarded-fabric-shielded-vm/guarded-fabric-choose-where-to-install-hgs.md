---
title: HGS を独自の新しいフォレストと既存の要塞フォレストのどちらにインストールするかを選択します。
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 28c7eceefa4747a35d1b989df4a2c5e43a8d6a42
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386800"
---
# <a name="choose-whether-to-install-hgs-in-its-own-dedicated-forest-or-in-an-existing-bastion-forest"></a>HGS を独自の専用フォレストまたは既存の要塞フォレストのどちらにインストールするかを選択します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016


HGS の Active Directory フォレストは、管理者がシールドされた Vm を制御するキーにアクセスできるため、機密性が高いと言えます。 既定のインストールでは、HGS 専用の新しいフォレストがセットアップされ、他の依存関係が構成されます。 このオプションは、環境が自己完結型であり、作成時に安全であることがわかっている場合に推奨されます。 

既存のフォレストに HGS をインストールするための技術的な要件は、ルートドメインに追加されることだけです。ルート以外のドメインはサポートされていません。 ただし、既存のフォレストを使用するための運用上の要件とセキュリティ関連のベストプラクティスもあります。 適切なフォレストは、AD DS または強化された[セキュリティ管理環境 (ESAE) フォレスト](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access-reference-material#ESAE_BM)[の Privileged Access Management](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services)によって使用されるフォレストなど、1つの重要な機能を提供するように意図的に構築されています。 通常、このようなフォレストには次の特性があります。

- 管理者が少ない (ファブリック管理者とは別の)
- ログオン数が少ない
- 汎用的な目的ではありません。 

運用フォレストなどの汎用フォレストは、HGS での使用に適していません。 また、HGS はファブリック管理者から分離する必要があるため、ファブリックフォレストも適していません。

## <a name="next-step"></a>次の手順

環境に最も適したインストールオプションを選択します。

- [独自の専用フォレストに HGS をインストールする](guarded-fabric-install-hgs-default.md)
- [既存の要塞フォレストに HGS をインストールする](guarded-fabric-install-hgs-in-a-bastion-forest.md)


