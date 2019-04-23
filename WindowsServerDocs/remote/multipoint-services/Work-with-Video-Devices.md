---
title: ビデオ デバイスを使用する
description: プロジェクターが MultiPoint services ステーションを使用してビデオを監視する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f7f5a97-efd2-4184-8ad3-cf029d615eab
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: d828ea911aaff27a1df79d0380dfe92987c3d2aa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844203"
---
# <a name="work-with-video-devices"></a>ビデオ デバイスを使用する
モニターやプロジェクターなどのビデオ デバイスが MultiPoint Services システムのコンピューターまたは MultiPoint Services *ステーション*に接続されているときに、ビデオ デバイスがどのように機能するかについて説明します。  
  
## <a name="working-with-video-monitors"></a>ビデオ モニターの操作  
MultiPoint Services システムのハードウェアにより、ビデオ モニターを接続する 2 つの方法があります。  
  
-   *USB ハブ ベースのシステム*、次の図に示すように、コンピューターの空いているビデオ ポートにビデオ モニター ケーブルを接続します。  
  
    ![USB ハブを使用するシステムにビデオが接続されているイメージ](./media/WMSVideoConnection.gif)  
  
-   *多機能ハブ ベースのシステム*組み込みのビデオのサポートを備えた多機能ハブのビデオ ポートにビデオ モニター ケーブルを接続します。  
  
    ![多機能ハブとビデオ接続のイメージ](./media/WMSMultifunctionHubVideoConnection.gif)  
  
詳細については、「[ステーションのセットアップ](Set-Up-a-Station.md)」トピックを参照してください。  
  
## <a name="working-with-video-projectors"></a>ビデオ プロジェクターの操作  
ラボ環境などで大きな画像を他の人に見せたい場合は、ビデオ プロジェクターを MultiPoint Services システムに接続できます。 両方の USB ハブ ベースおよび多機能ハブ ベース ステーションには、プロジェクターをステーションに接続するための 2 つのオプションがあります。  
  
-   次の図に示すように、モニターをプロジェクターに置き換えて、そのステーションのディスプレイ デバイスとしてプロジェクターを使用します。  
  
    ![コンピューターに接続されたプロジェクターのイメージ](./media/WMSVideoProjectorConnection.gif)  
  
-   ビデオ スプリッター デバイスを使用して、プロジェクターとモニターの両方をステーションのビデオ ポートに接続します。  
  
    MultiPoint Services は、両方のディスプレイ デバイスに同じイメージを表示します。 投影しないときはプロジェクターの電源をオフにして、ビデオ モニターだけを使用できます。  
  
どちらかのオプションを使用する場合は、次のことに注意してください。  
  
-   ビデオ ディスプレイを接続するときは、MultiPoint Services が新しいディスプレイを正しく認識できるようにするために、再度*ステーションの関連付け*が必要になる場合があります。 ステーションのビデオ ディスプレイ デバイスに表示される指示に従ってください。  
  
-   DVI プラグと VGA プラグを変換するには、アダプターまたはコンバーター デバイスを使用する必要がある場合があります。  
  
-   "Y" スプリッター ケーブルを使用すると、両方のビデオ デバイスのビデオ品質が低下する可能性があります。  
  
-   "Y" スプリッター ケーブルを使用してプロジェクターとモニターの両方を使用する場合、MultiPoint Services は、両方のデバイスの画面解像度を、どちらか低い方の最大解像度 (通常はプロジェクター) に調整します。  
  
-   MultiPoint Services は、単一ステーションの表示の複数モニターへの拡張はサポートしていません。  
  
## <a name="see-also"></a>関連項目  
[ステーション ハードウェアを管理します。](Manage-Station-Hardware.md)  
[ステーションをセットアップします。](Set-Up-a-Station.md) 