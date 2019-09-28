---
title: USB ゼロ クライアント接続ステーションでセットアップ MultiPoint サービス
description: MultiPoint Services で USB ゼロクライアントステーションを作成する方法について説明します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d2908865-6be3-474d-88f1-995f40bb61d0
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 80a73065024e5c40f1ebf8efd64022ee6d48fbe8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395073"
---
# <a name="set-up-a-usb-zero-client-connected-station-in-multipoint-services"></a>USB ゼロ クライアント接続ステーションでセットアップ MultiPoint サービス
USB ゼロ クライアントを使用して MultiPoint サービス ステーションを作成すると、ステーションごとに、モニターは、次の図に示すように USB ゼロ クライアントのビデオ ポートに接続されます。 これと他のステーションの種類に関する詳細については、次を参照してください。 [MultiPoint ステーション](MultiPoint-services-Stations.md)します。
  
**1つの直接ビデオ接続ステーションと2つの USB ゼロクライアント接続ステーションを備えた MultiPoint Services システム**  
  
![USB ゼロ クライアント接続ステーション](./media/WMS11_diagram7.gif)  
  
> [!IMPORTANT]  
> セットアップする前に USB ゼロ クライアント接続ステーション、必ず、ビデオ カードや USB ゼロ クライアント用の最新のドライバーをインストールしてください。 古いドライバーには、正常に完了しない MultiPoint サービスの構成を防ぐことができます。 手順については、次を参照してください。 [更新プログラムが必要な場合は、デバイス ドライバーをインストールおよび](Update-and-install-device-drivers-if-needed.md)です。  
  
> [!IMPORTANT]  
> USB over Ethernet 0 クライアントを使用している場合、ベンダーから、この手順ではなく、イーサネット接続を使用して、ネットワーク上のデバイスを設定する手順してください。  
  
### <a name="to-set-up-a-usb-zero-client-connected-station"></a>設定可能な USB ゼロ クライアント接続ステーション  
  
1.  ビデオ モニター ケーブル、DVI または VGA ビデオ ディスプレイ上のポートに USB ゼロ クライアント接続、次の図に示すようにします。  
  
    ![USB ハブを使用するシステムにビデオが接続されているイメージ](./media/WMSVideoConnection.gif)  
  
2.  USB ゼロ クライアントをコンピューターで開かれた USB ポートに接続します。  
  
    ![MultiPoint サービス USB ハブ接続のイメージ](./media/WMSUSBHubConnection.gif)  
  
3.  USB ゼロ クライアントには、キーボードとマウスを接続します。  
  
    ![USB ハブ入力デバイス接続のイメージ](./media/WMSUSBDeviceConnection.gif)  
  
4.  外部からの電源の USB ゼロ クライアントを使用している場合は、USB ゼロ クライアントの電源ケーブルを電源コンセントに接続します。  
  
5.  電源コンセントにビデオ モニターの電源ケーブルを接続します。  
  
6.  ラジオ局にデバイスを関連付けるメッセージが表示されたら、セットアップを実行するモニターで手順してください。 (一般に、USB ゼロ クライアント接続ステーションはステーションと関連付けられている自動的にサーバーに追加するときです。)