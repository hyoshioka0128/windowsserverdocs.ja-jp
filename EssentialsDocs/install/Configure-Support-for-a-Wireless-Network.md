---
title: ワイヤレス ネットワークのサポートの構成
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d7020d4-fd46-4858-a406-de5c0f21ea06
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c5c98727b81bf37fdb3f90c612270462a51908c8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833113"
---
# <a name="configure-support-for-a-wireless-network"></a>ワイヤレス ネットワークのサポートの構成

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

ワイヤレス ネットワークをサポートするようにオペレーティング システムを構成できます。 サーバー上でワイヤレス サポートを有効にするには、次の要件を満たしている必要があります。  
  
-   サーバーにワイヤード (有線) ネットワーク アダプターがインストールされている必要があります。  
  
-   オペレーティング システムでネットワーク アダプターがサポートされていない場合、ワイヤレス ネットワーク アダプター用の適切なドライバーがプレインストールされている必要があります。  
  
-   ワイヤレス ネットワーク アダプターを有効および無効にする機能を使用できるようにする必要があります。 これを実行するための方法として、サーバー上の物理ボタンや、ダッシュボードのカスタム ユーザー インターフェイスがあります。 製品マニュアルに、ワイヤレス ネットワーク アダプターを有効および無効にするための手順が示されています。  
  
-   ワイヤレス ネットワークを選択し、ワイヤレス ネットワークに接続するための機能を使用できるようにする必要があります。 これを実行するには、カスタム ユーザー インターフェイスをダッシュボードに追加します。 製品マニュアルに、ワイヤレス ネットワークを選択し、ワイヤレス ネットワークに接続するための手順が示されています。  
  
-   ワイヤレス アドホック ネットワークをサポートするための機能が必要な場合、ダッシュボードで拡張ユーザー インターフェイスを提供する必要があります。 ユーザー インターフェイスは、Windows Server 2008 R2 のコントロール パネルのワイヤレス アドホック ネットワークのセットアップ ウィザードを起動する、ボタンまたはリンクである可能性があります。  
  
## <a name="additional-considerations"></a>その他の考慮事項  
 ワイヤレス ネットワークのサポートを構成するときには、次の情報も考慮する必要があります。  
  
-   セットアップを実行するには、サーバーを配線でネットワークに接続する必要があります。  
  
-   ベアメタル復元が実行されるネットワーク コンピューターは、ネットワークに配線で接続する必要があります。  
  
-   サーバーのベアメタル復元を実行するには、サーバーをネットワークに配線で接続する必要があります。  
  
-   サーバー上にアドホック ネットワークが作成されている場合、ワイヤレス ネットワーク アダプターをアドホック ネットワーク専用にして、ユーザーがインターネット接続を取得するためネットワーク ケーブルを常にサーバーに差し込めるようにする必要があります。  
  
> [!NOTE]
>  ネットワーク接続の構成の詳細については、「 [Preconfiguring a Router](Preconfiguring-a-Router.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)