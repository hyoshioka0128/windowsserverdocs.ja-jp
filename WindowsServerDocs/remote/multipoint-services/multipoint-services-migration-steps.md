---
title: MultiPoint Services の移行の手順を実行します。
description: Windows Server 2016 で MultiPoint Services に移行する手順について説明します
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ee77efa-7cc5-4ddf-aaff-b5634a717014
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: b63ef4bf63ce990aa0b0ba7624905ba8f14dde98
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854813"
---
# <a name="migrate-to--multipoint-services-in-windows-server-2016"></a>MultiPoint Services in Windows Server 2016 への移行します。

>適用先:Windows Server 2016

次の手順と Windows Server 2016 で MultiPoint Services に移行する移行の計画ワークシートで収集した情報を使用します。

## <a name="transfer-server-settings"></a>サーバーの設定を転送します。
移行先サーバーでは、MultiPoint マネージャーを開きます。 クリックして**サーバー設定の編集**します。 移行の計画ワークシートに従って設定を適用します。

> [!NOTE]
> 移行先サーバーでディスク保護を有効にする必要がある場合は、MultiPoint Services を構成した後まで待機します。

## <a name="transfer-station-settings"></a>ステーションの設定を転送します。
ステーションはステーションの設定を適用する前にマップされているすべての移行先サーバーに接続されていることを確認します。 ステーションが自動的に検出されます。 ユーザー ステーションの USB デバイスが接続されているサーバーのマッピングを定義するには、各ステーション画面の指示に従います。 移行の計画ワークシート」の説明に従って、ステーションの優先設定を適用します。

## <a name="migrate-the-vdi-template"></a>VDI のテンプレートを移行します。

VDI のテンプレートをインポートするには、移行元サーバーから、前に、移行先サーバー上の仮想デスクトップで MultiPoint マネージャーを使用して有効です。

1. 移動して、**仮想デスクトップ**MultiPoint マネージャー タブ。
2. クリックして**仮想デスクトップを有効になっている**します。 サーバーは、HYPER-V の役割をインストールしを再起動します。
3. MultiPoint マネージャーを開きに戻る**仮想デスクトップ**します。
4. クリックして**仮想デスクトップ テンプレートのインポート**します。 指示に従って、移行元サーバーからテンプレートをインポートします。

> [!NOTE]
> 仮想デスクトップ テンプレートをインポートするときに、テンプレートに適用されたカスタマイズがリセットされます。 

## <a name="next-step"></a>次の手順
[新しい MultiPoint Services デプロイを検証します。](multipoint-services-post-migration-steps.md)