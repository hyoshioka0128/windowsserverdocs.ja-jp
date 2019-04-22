---
title: 物理コンピューターとプライマリ ステーションをセットアップする
description: 最初のシステム、MultiPoint Services で、プライマリ ステーションを設定する方法について説明します
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e83b126-ce9a-4cd7-a0bd-6627c9e0f81b
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 6569c4963d31b72216943bf29b71411e702caf84
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812013"
---
# <a name="set-up-the-physical-computer-and-primary-station"></a>物理コンピューターとプライマリ ステーションをセットアップする
MultiPoint Services をインストールする前に、MultiPoint Services システムのプライマリ ステーションを設定する必要があります。 ローカル エリア ネットワーク (LAN) を使用する場合は、コンピューターを LAN に接続します。  
  
A*ステーション*は MultiPoint Services にアクセスされるエンドポイントです。 *プライマリ ステーション*は最初のステーションを MultiPoint Services が起動時に開始します。 管理者をスタートアップ メニューにアクセスし、設定を使用できます。 プライマリ ステーションがシステムの構成へのアクセスを提供し、システムが実行されているスタートアップ中に、MultiPoint Services の前に利用可能な情報だけをトラブルシューティングします。 開始の後、その他のすべてのステーションと同様にプライマリ ステーションを使用できます。  
  
プライマリ ステーションでは、直接ビデオ接続ステーションをする必要があります。 次の手順では、MultiPoint Services コンピューターに必要なハードウェアを接続する方法について説明します。  
  
ステーションの詳細については、次を参照してください。 [MultiPoint ステーション](multipoint-services-stations.md)します。 ハードウェアの選択を行う方法の詳細については、次を参照してください。 [MultiPoint Services システムのハードウェアを選択すると](Selecting-Hardware-for-Your-MultiPoint-services-System.md)します。 接続については他のステーション MultiPoint サービスの種類を参照してください。[その他の局を MultiPoint Services コンピューターに接続](Attach-additional-stations-to-your-MultiPoint-services-computer.md)します。  
  
> [!NOTE]  
> ビデオ接続ステーションを作成するには、(英語またはスペイン語キーボードの場合) などのラテン語キーボードを使用する必要があります。  
  
## <a name="to-set-up-your-primary-station"></a>プライマリ ステーションを設定するには  
  
1.  MultiPoint Services を実行しているコンピューターが無効になり、電源が入っていないことを確認してください。  
  
2.  モニターの電源コードを電源コンセントに接続し、次に示すように、コンピューターのビデオ ディスプレイ ポート モニター ケーブルを接続します。  
  
    ![USB ハブを使用するシステムにビデオが接続されているイメージ](./media/WMSVideoConnection.gif)  
  
3.  ステーションで USB キーボードとマウスを使用する場合は、次の手順を完了します。  
  
    1.  次に示すように、コンピューターの空いている USB ポートに外部 USB ハブを接続します。  
  
        ![MultiPoint サービス USB ハブ接続のイメージ](./media/WMSUSBHubConnection.gif)  
  
    2.  USB ハブに USB キーボードとマウスを接続します。  
  
        ![USB ハブ入力デバイス接続のイメージ](./media/WMSUSBDeviceConnection.gif)  
  
        > [!NOTE]  
        > MultiPoint Services コンピューター ps/2 ポートにある場合、必要な場合、使用できます ps/2 キーボードとマウスをコンピューターに直接接続します。 ただし、このセットアップでは、重要な制限があります。 ユーザーは、web カメラ、オーディオ デバイスを使用し、フラッシュ ドライブで ps/2 ステーションことはできません。  
  
    3.  電源が投入されて外部ハブを使用している場合は、ハブの電源ケーブルを電源コンセントに接続します。  
  
        > [!IMPORTANT]  
        > 電源のハブの使用をお勧めします。 過小の現在の状態が不安定になるシステムの動作に発生します。  
        >   
        > ユーザーを割り当てないでくださいマウスとキーボードでは、コンピューターの USB ポートに直接します。 これは、複数のキーボードとマウスを同じステーションまたはステーションがないの不適切な関連付けがまったく発生する可能性があります。  
  
        > [!NOTE]  
        > システムのマザーボード上のホストのオーディオ デバイスは、MultiPoint Services がコンソール モード中にのみ使用できます。 外部 USB ハブを使用するステーションの中断のないオーディオを確保するには、ハブに接続する USB オーディオ デバイスを使用する必要があります。  
  
## <a name="to-connect-the-computer-to-the-lan"></a>コンピューターを LAN に接続するには  
  
-   LAN があれば、コンピューターをネットワーク ケーブルを使用して、ネットワークに接続します。