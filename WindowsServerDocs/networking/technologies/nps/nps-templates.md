---
title: NPS テンプレート
description: このトピックでは、Windows Server 2016 でネットワーク ポリシー サーバー テンプレートの概要を示します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fdfc0df1-21c7-492c-9fad-38fe9c7d935a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0647dbf0f99a01e32ba68475b439501e2dbeebfe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823313"
---
# <a name="nps-templates"></a>NPS テンプレート

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

ネットワーク ポリシー サーバー \(NPS\)テンプレートでは、リモート認証ダイヤルイン ユーザー サービスなどの構成要素を作成できます\(RADIUS\)クライアントまたはローカルで再利用できる共有シークレットは、。NPS およびその他の NPSs で使用するためのエクスポート。

NPS テンプレートは、時間と 1 つまたは複数のサーバー上の NPS 構成にかかるコストを削減するために設計されています。 次の NPS テンプレートの種類は構成テンプレートの管理に使用できます。

- 共有シークレット
- RADIUS クライアント
- リモート RADIUS サーバー
- IP フィルター
- 修復サーバー グループ

テンプレートを構成することは、NPS を直接構成と異なります。 テンプレートを作成しても、NPS の機能には影響しません。 NPS コンソールで、テンプレートが NPS の機能に影響する適切な場所にテンプレートを選択する場合にのみになります。 

たとえば、NPS コンソールの RADIUS クライアントとサーバーの RADIUS クライアントを構成する場合、NPS の構成を変更して、ネットワーク アクセス サーバーのいずれかと通信するように NPS を構成する 1 つの手順を実行\(NAS の\). \(次の手順は、NPS と通信する NAS を構成することです。\)ただし、NPS コンソールで 新しい RADIUS クライアント テンプレートを構成するかどうかは**テンプレートの管理**新しい RADIUS クライアントを作成するのではなく**RADIUS クライアントとサーバー**、作成した、テンプレートではなくする変更いない NPS 機能まだします。 NPS の機能を変更するには、NPS コンソールで、正しい場所からテンプレートを選択する必要があります。

## <a name="creating-templates"></a>テンプレートの作成

テンプレートを作成するには、NPS コンソールを開きなど、テンプレートの種類を右クリックして**IP フィルター**、 をクリックし、**新規**します。 新しいテンプレートのプロパティ ダイアログ ボックスが開きますテンプレートを構成することができます。

## <a name="using-templates-locally"></a>テンプレートをローカルで使用します。

作成したテンプレートを使用する**テンプレートの管理**テンプレートを適用することができます、NPS コンソール内の場所に移動します。 たとえば、新しい共有シークレット テンプレートを作成する場合の RADIUS クライアントの構成に適用**RADIUS クライアントとサーバー**と**RADIUS クライアント**、RADIUS クライアントのプロパティを開きます。 **既存の共有シークレットのテンプレートを選択して**、使用可能なテンプレートの一覧から以前に作成したテンプレートを選択します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。
