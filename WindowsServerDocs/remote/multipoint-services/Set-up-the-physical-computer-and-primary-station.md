---
title: 物理コンピューターとプライマリ ステーションをセットアップする
description: MultiPoint Services で最初のシステム、プライマリステーションをセットアップする方法について説明します。
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 4e83b126-ce9a-4cd7-a0bd-6627c9e0f81b
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 0f52d3fa4aeca8fd4e036a93ee5a175bf1e96d0b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855625"
---
# <a name="set-up-the-physical-computer-and-primary-station"></a>物理コンピューターとプライマリ ステーションをセットアップする
MultiPoint Services をインストールする前に、MultiPoint Services システムのプライマリステーションをセットアップする必要があります。 ローカルエリアネットワーク (LAN) を使用する場合は、コンピューターを LAN に接続します。  
  
*ステーション*は、MultiPoint サービスへのアクセスに使用されるエンドポイントです。 *プライマリステーション*は、MultiPoint Services の開始時に最初に開始されるステーションです。 管理者はこれを使用して、スタートアップメニューと設定にアクセスできます。 プライマリステーションは、システム構成とトラブルシューティング情報へのアクセスを提供します。この情報は、起動時と MultiPoint サービスシステムの実行中にのみ使用できます。 起動後、他のステーションと同じようにプライマリステーションを使用できます。  
  
プライマリ ステーションでは、直接ビデオ接続ステーションをする必要があります。 次の手順では、必要なハードウェアを MultiPoint Services コンピューターに接続する方法について説明します。  
  
ステーションの詳細については、「 [MultiPoint ステーション](multipoint-services-stations.md)」を参照してください。 ハードウェアの選択の詳細については、「 [MultiPoint Services システムのハードウェアの選択](Selecting-Hardware-for-Your-MultiPoint-services-System.md)」を参照してください。 他のステーションの種類を MultiPoint Services に接続する方法については、「[追加のステーションを Multipoint services コンピューターに接続する](Attach-additional-stations-to-your-MultiPoint-services-computer.md)」を参照してください。  
  
> [!NOTE]  
> ビデオ接続ステーションを作成するには、ラテン語キーボード (英語やスペイン語のキーボードなど) を使用する必要があります。  
  
## <a name="to-set-up-your-primary-station"></a>プライマリステーションを設定するには  
  
1.  MultiPoint Services を実行しているコンピューターがオフになっていて、切断されていることを確認します。  
  
2.  次に示すように、モニターの電源コードを電源コンセントに接続し、モニターケーブルをコンピューターのビデオディスプレイポートに接続します。  
  
    ![USB ハブを使用するシステムにビデオが接続されているイメージ](./media/WMSVideoConnection.gif)  
  
3.  ステーションで USB キーボードとマウスを使用する場合は、次の手順を実行します。  
  
    1.  次に示すように、コンピューター上の開いている USB ポートに外部 USB ハブを接続します。  
  
        ![MultiPoint サービス USB ハブ接続のイメージ](./media/WMSUSBHubConnection.gif)  
  
    2.  Usb キーボードとマウスを USB ハブに接続します。  
  
        ![USB ハブ入力デバイス接続のイメージ](./media/WMSUSBDeviceConnection.gif)  
  
        > [!NOTE]  
        > MultiPoint Services コンピューターに PS/2 ポートがある場合は、必要に応じて、コンピューターに直接接続された PS/2 キーボードとマウスを使用します。 ただし、このセットアップには大きな制限があります。 PS/2 ステーションでは、ユーザーはオーディオデバイス、web カメラ、フラッシュドライブを使用できません。  
  
    3.  電源が投入されて外部ハブを使用している場合は、ハブの電源ケーブルを電源コンセントに接続します。  
  
        > [!IMPORTANT]  
        > 電源のハブの使用をお勧めします。 過小の現在の状態が不安定になるシステムの動作に発生します。  
        >   
        > ユーザーを割り当てないでくださいマウスとキーボードでは、コンピューターの USB ポートに直接します。 これは、複数のキーボードとマウスを同じステーションまたはステーションがないの不適切な関連付けがまったく発生する可能性があります。  
  
        > [!NOTE]  
        > システムのマザーボード上のホストオーディオデバイスは、MultiPoint サービスがコンソールモードのときにのみ使用できます。 外部 USB ハブを使用するステーションのオーディオを中断しないようにするには、ハブに接続されている USB オーディオデバイスを使用する必要があります。  
  
## <a name="to-connect-the-computer-to-the-lan"></a>コンピューターを LAN に接続するには  
  
-   LAN を使用している場合は、ネットワークケーブルでコンピューターをネットワークに接続します。