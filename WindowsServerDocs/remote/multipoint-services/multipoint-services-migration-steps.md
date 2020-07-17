---
title: MultiPoint Services を移行する手順
description: Windows Server 2016 の MultiPoint Services に移行する手順について説明します。
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 3ee77efa-7cc5-4ddf-aaff-b5634a717014
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: f2e293fafb8d6f5d84e9ea5a4ad8ef3b7fe2ba7d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858695"
---
# <a name="migrate-to--multipoint-services-in-windows-server-2016"></a>Windows Server 2016 の MultiPoint Services への移行

>適用対象: Windows Server 2016

次の手順に加えて、移行計画ワークシートで収集した情報を使用して、Windows Server 2016 の MultiPoint Services に移行します。

## <a name="transfer-server-settings"></a>転送サーバーの設定
移行先サーバーで、MultiPoint マネージャーを開きます。 **[サーバー設定の編集]** をクリックします。 移行計画ワークシートに従って設定を適用します。

> [!NOTE]
> 移行先サーバーでディスク保護を有効にする必要がある場合は、MultiPoint Services を構成してから待機します。

## <a name="transfer-station-settings"></a>ステーションの設定の転送
ステーションの設定を適用する前に、ステーションが移行先サーバーに接続されていて、すべてがマップされていることを確認します。 ステーションが自動的に検出されます。 各ステーション画面の指示に従って、ユーザーステーションと接続されている USB デバイスのサーバーマッピングを定義します。 移行計画ワークシートに記載されているように、優先ステーションの設定を適用します。

## <a name="migrate-the-vdi-template"></a>VDI テンプレートを移行する

移行元サーバーから VDI テンプレートをインポートする前に、MultiPoint マネージャーを使用して、移行先サーバーで仮想デスクトップを有効にします。

1. MultiPoint マネージャーの **[仮想デスクトップ]** タブにアクセスします。
2. **[有効な仮想デスクトップ]** をクリックします。 サーバーは Hyper-v の役割をインストールしてから、を再起動します。
3. MultiPoint マネージャーを開き、 **[仮想デスクトップ]** に戻ります。
4. **[仮想デスクトップテンプレートのインポート]** をクリックします。 手順に従って、移行元サーバーからテンプレートをインポートします。

> [!NOTE]
> 仮想デスクトップテンプレートをインポートすると、そのテンプレートに適用されたカスタマイズがすべてリセットされます。 

## <a name="next-step"></a>次の手順
[新しい MultiPoint サービスのデプロイを検証します。](multipoint-services-post-migration-steps.md)