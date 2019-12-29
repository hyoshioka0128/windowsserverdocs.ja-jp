---
title: MultiPoint サービスに直接ビデオ接続ステーションを設定します。
description: MultiPoint Services で直接ビデオ接続ステーションを作成する方法について説明します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82ba3517-9743-4cde-8eea-63a17edb016f
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: ab57f3d996cfe9196fd256a76516a44dc146043b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389362"
---
# <a name="set-up-a-direct-video-connected-station-in-multipoint-services"></a>MultiPoint サービスに直接ビデオ接続ステーションを設定します。
直接ビデオ接続ステーション、モニターが MultiPoint Server コンピューターのビデオ ポートに直接接続されています。 キーボードとマウス USB ハブにし、接続されているし、モニターに関連付けられました。  
  
次の図は、単一の MultiPoint Server コンピューターと 4 つの直接のビデオ接続ステーションを持つ MultiPoint Server 環境を示します。 詳細については、次を参照してください。 [MultiPoint Server ステーション](MultiPoint-services-Stations.md)します。  
  
**4つの直接ビデオ接続がある MultiPoint Services システム**  
  
![MultiPoint サービス USB ベース システム レイアウトのイメージ](./media/WMSMultiPointServerUSBSystemLayout.gif)  
  
> [!NOTE]  
> 直接ビデオ接続ステーションを構成するのには、(英語とスペイン語の言語のキーボード) などのラテン語キーボードを使用する必要があります。  
  
## <a name="to-set-up-a-direct-video-connected-station"></a>直接のビデオ接続ステーションを設定するには  
  
1.  次に示すように、コンピューターで、ビデオ ディスプレイ ポート モニター ケーブルを接続します。  
  
    ![USB ハブを使用するシステムにビデオが接続されているイメージ](./media/WMSVideoConnection.gif) 
  
2.  電源コンセントにビデオ モニターの電源ケーブルを接続します。  
  
3.  次のように、USB ハブをコンピューターで、オープンな USB ポートに接続します。  
  
    ![MultiPoint サービス USB ハブ接続のイメージ](./media/WMSUSBHubConnection.gif)  
  
4.  キーボードとマウスをステーションの USB ハブに接続します。  
  
    ![USB ハブ入力デバイス接続のイメージ](./media/WMSUSBDeviceConnection.gif)  
  
5.  USB ハブに、ヘッドホンなど、追加周辺機器を接続します。  
  
6.  電源が投入されて外部ハブを使用している場合は、ハブの電源ケーブルを電源コンセントに接続します。  
  
    > [!IMPORTANT]  
    > 電源のハブの使用をお勧めします。 過小の現在の状態が不安定になるシステムの動作に発生します。  
    >   
    > ユーザーを割り当てないでくださいマウスとキーボードでは、コンピューターの USB ポートに直接します。 これは、複数のキーボードとマウスを同じステーションまたはステーションがないの不適切な関連付けがまったく発生する可能性があります。  
  
7.  ラジオ局を作成するモニターに表示される指示に従います。  
  
MultiPoint サービス環境内に 2 つ以上の直接のビデオ接続ステーションを追加する場合、プライマリ ステーションは変更できます。 ビデオの接続されたステーションとは、プライマリ ステーションを直接調べることができます簡単にします。  
  
## <a name="to-find-out-which-direct-video-connected-station-is-the-primary-station"></a>確認するには、プライマリ ステーションは、ステーションのビデオ接続をダイレクトします。  
  
1.  コンピューターのディスプレイアダプター (ビデオカード) に直接接続されているすべてのモニターを有効にします。  
  
2.  開始 (または再開) MultiPoint サービス コンピューターおよびモニターの起動画面に表示を参照してください。 そのステーションとは、プライマリ ステーションです。  
  
    > [!NOTE]  
    > 場合によっては、BIOS のスタートアップの情報は複数のモニターに同時に表示されます。 その場合は、モニタの見なすことができます、「プライマリ ステーション」BIOS にアクセスするためにします。