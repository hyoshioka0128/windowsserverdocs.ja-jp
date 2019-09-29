---
title: Windows 管理センターの拡張機能を開発する
description: Windows 管理センター SDK (Project ホノルル) の拡張機能の開発
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 4b3d5b371a9ebec27dafa74610f8c6a87c404d82
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357122"
---
# <a name="develop-an-extension-for-windows-admin-center"></a>Windows 管理センターの拡張機能を開発する

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センターでは、ツール拡張機能、ソリューション拡張機能、ゲートウェイプラグインの3種類の拡張機能がサポートされています。 SDK には、さまざまな種類の拡張機能/プラグインを構築するためのガイドとなるコンテンツと例が含まれています。

> [!NOTE]
> さまざまな拡張機能の種類に慣れていない場合は、 拡張[機能のアーキテクチャと拡張機能の種類](understand-extensions.md)の詳細については、こちらを参照してください。

## <a name="development-step-by-step"></a>開発手順

- 開発環境を[準備](prepare-development-environment.md)する
- [ツール](develop-tool.md)の拡張機能の作成
- [ソリューション](develop-solution.md)の拡張機能の作成
- [ゲートウェイのプラグイン](develop-gateway-plugin.md)の作成
- [ガイド](guides.md)での詳細の確認

## <a name="sdk-design-toolkit"></a>SDK design toolkit

Windows 管理センター [SDK design toolkit](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)をご覧ください。 このツールキットは、Windows 管理センターのスタイル、コントロール、およびページテンプレートを使用して、PowerPoint の拡張機能を迅速にモックアップできるように設計されています。 コーディングを開始する前に、Windows 管理センターで拡張機能がどのように表示されるかを確認してください。
