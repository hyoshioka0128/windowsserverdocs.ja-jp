---
title: Azure 統合の構成
description: Azure 統合 Windows Admin Center (Project Honolulu) を構成します。 Windows Admin Center ゲートウェイを Azure に接続します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 38b973680463cdebc1b3168e447abfcf1caba6b5
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296994"
---
# Azure 統合の構成

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows Admin Center には、Azure サービスと統合されるいくつかのオプション機能がサポートされています。 [Windows Admin Center で利用できる Azure 統合オプションについて説明します。](../plan/azure-integration-options.md)

Azure、ゲートウェイ アクセス用の Azure Active Directory の認証を利用したり、(たとえば、Azure のサイトを使用して Windows Admin Center で管理されている Vm を保護するために、お客様に代わって Azure リソースを作成すると通信できるように Windows Admin Center ゲートウェイを許可するには回復)、まず、Windows Admin Center ゲートウェイを Azure に登録する必要があります。 新しいバージョンへのゲートウェイを更新するときに、設定を保持 - Windows Admin Center ゲートウェイの後に、これを行う必要があるだけです。

## ゲートウェイを Azure に登録します。

初めて Windows Admin Center で、Azure の統合機能を使用しようとしたが求められること、ゲートウェイを Azure に登録します。 Windows Admin Center の設定で、[ **Azure** ] タブに移動して、ゲートウェイを登録することもできます。

ガイド付きの製品の手順は、ディレクトリは、Azure との通信に Windows Admin Center は、Azure AD アプリケーションを作成します。 自動的に作成される Azure AD アプリケーションを表示するには、Windows Admin Center の設定の [ **Azure** ] タブに移動します。 **Azure でビュー**のハイパーリンクを使用して、Azure portal で Azure AD アプリケーションを表示できます。 

作成した Azure AD アプリケーションは、[ゲートウェイを Azure AD authentication](../configure/user-access-control.md#azure-active-directory)を含む、Windows Admin Center での Azure 統合のすべてのポイントに使用されます。