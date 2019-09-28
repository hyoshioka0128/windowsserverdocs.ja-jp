---
title: ステーションをセットアップする
description: MultiPoint Services でステーションを設定する方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dce05b6c-795e-43b2-9920-026550b873c5
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 95a332a3d15e82047b46cc19f168f945cdb334d2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389448"
---
# <a name="set-up-a-station"></a>ステーションをセットアップする
通常、MultiPoint Services の*ステーション*は、*ステーション ハブ*、マウス、キーボード、およびビデオ モニターで構成されています。 このトピックでは、MultiPoint Services ステーションを作成するためにステーション ハブにハードウェア デバイスを接続する方法について説明します。  
  
ステーション ハブとは、MultiPoint Services システムのコンピューターに周辺機器を接続するハードウェア デバイスです。 MultiPoint Services では、次の 2 種類のステーション ハブがサポートされています。  
  
-   **USB ハブ:** ユニバーサルシリアルバス2.0 以降の仕様に準拠する汎用のマルチポート USB 拡張ハブ。 通常このようなハブには、コンピューター上の単一の USB ポートに複数の USB デバイスを接続できる、USB ポートが 2つ、4つ、またはそれ以上あります。 USB ハブは、外部電源またはバス供給できる一般的な別々 のデバイスです。 MultiPoint Services のステーション ハブとして使用する場合は、ポートが 4 つ以上あるハブを使用することをお勧めします。  
  
    > [!IMPORTANT]  
    > キーボードとマウス以外の USB デバイスをハブに接続する場合に最適なパフォーマンスを得るには、外部電源のハブを使用することをお勧めします。  
  
-   **多機能ハブ:** USB ポートを介してコンピューターに接続し、ビデオモニターなどのさまざまな USB 以外のデバイスをハブに接続できる拡張ハブ。 多機能ハブでは、特定のハードウェアの製造元によって生成され、デバイス固有ドライバーをインストールする必要があります。  
  
ステーションを MultiPoint Services システムに追加する場合は、使用するステーション ハードウェアで利用できる十分な数の接続ポートがあることを最初に確認する必要があります。 さらに、適切な数を保護する必要があります *クライアント アクセス ライセンス (Cal)* MultiPoint サービス システムにします。  
  
## <a name="setting-up-station-hardware"></a>ステーション ハードウェアの設定  
このセクションの手順では、さまざまな種類のステーション ハブに MultiPoint Services ステーション ハードウェアを接続する方法について説明します。  
  
### <a name="to-set-up-a-station-with-a-usb-hub"></a>ステーションに USB ハブをセットアップするには  
  
1.  新しいステーションを接続する前に、すべてのユーザー *セッション*を*終了*し、MultiPoint Services システム内のコンピューターとその他のデバイスをシャットダウンします。  
  
2.  次の図のように、コンピューターのビデオ ディスプレイ ポートに新しいビデオ モニター ケーブルを接続します。  
  
    ![USB ハブを使用するシステムにビデオが接続されているイメージ](./media/WMSVideoConnection.gif)  
  
3.  コンピューターの空いている USB ポートに新しい USB ハブを接続します。  
  
    ![MultiPoint Server USB ハブ接続のイメージ](./media/WMSUSBHubConnection.gif)  
  
4.  USB ハブにキーボードとマウスを接続します。  
  
    ![USB ハブ入力デバイス接続のイメージ](./media/WMSUSBDeviceConnection.gif)  
  
5.  電源コンセントにビデオ モニターの電源ケーブルを接続します。  
  
6.  コンピューターを起動します。  
  
7.  MultiPoint Services が開始されます。 新しいステーションのビデオモニターに表示される指示に従って、デバイスを新しいステーションに関連付けます。  
  
### <a name="to-set-up-a-station-with-a-multifunction-hub"></a>ステーションに多機能ハブをセットアップするには  
  
1.  新しいステーションを接続する前に、すべてのユーザー セッションを終了し、MultiPoint Services システム内のコンピューターとその他のデバイスをシャットダウンします。  
  
2.  次の図のように、多機能ハブの DVI または VGA ビデオ ディスプレイ ポートに新しいビデオ モニター ケーブルを接続します。  
  
    ![多機能ハブとビデオ接続のイメージ](./media/WMSMultifunctionHubVideoConnection.gif)  
  
3.  コンピューターの空いている USB ポートに新しい多機能ハブを接続します。  
  
    ![多機能ハブ接続のイメージ](./media/WMSMultifunctionHubConnection.gif)  
  
4.  多機能ハブの PS2 または USB コネクタに、キーボードとマウスを接続します。  
  
    ![多機能ハブと PS2 コネクタのイメージ](./media/WMSMultifunctionHubPS2Connection.gif)  
  
5.  電源コンセントにビデオ モニターの電源ケーブルを接続します。  
  
6.  コンピューターを起動します。  
  
7.  MultiPoint Services が開始されます。 メッセージが表示されたら、新しいステーションのビデオモニターに表示される指示に従って、デバイスを新しいステーションに*関連付け*ます。  
  
## <a name="see-also"></a>関連項目  
[ユーザー セッションを終了する](End-a-User-Session.md)  
[再起動またはシャットダウンする](Restart-or-Shut-Down.md)  
[ステーション ハードウェアの管理](Manage-Station-Hardware.md)  
[USB デバイスを使用する](Work-with-USB-Devices.md)