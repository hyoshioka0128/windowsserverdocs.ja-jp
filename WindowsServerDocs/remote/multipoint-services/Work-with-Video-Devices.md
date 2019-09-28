---
title: ビデオ デバイスを使用する
description: ビデオモニターとプロジェクターが MultiPoint Services のステーションを操作する方法について説明します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b7019000c99295204f196ee918129cded02e084f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389252"
---
# <a name="work-with-video-devices"></a>ビデオ デバイスを使用する
モニターやプロジェクターなどのビデオ デバイスが MultiPoint Services システムのコンピューターまたは MultiPoint Services *ステーション*に接続されているときに、ビデオ デバイスがどのように機能するかについて説明します。  
  
## <a name="working-with-video-monitors"></a>ビデオ モニターの操作  
MultiPoint Services システムのハードウェアにより、ビデオ モニターを接続する 2 つの方法があります。  
  
-   *USB ハブベースのシステム*の場合は、次の図に示すように、コンピューター上の開いているビデオポートにビデオモニターケーブルを接続します。  
  
    ![USB ハブを使用するシステムにビデオが接続されているイメージ](./media/WMSVideoConnection.gif)  
  
-   ビデオサポートが組み込まれている*多機能ハブベースのシステム*では、マルチ機能ハブのビデオポートにビデオモニターケーブルを接続します。  
  
    ![多機能ハブとビデオ接続のイメージ](./media/WMSMultifunctionHubVideoConnection.gif)  
  
詳細については、「[ステーションのセットアップ](Set-Up-a-Station.md)」トピックを参照してください。  
  
## <a name="working-with-video-projectors"></a>ビデオ プロジェクターの操作  
ラボ環境などで大きな画像を他の人に見せたい場合は、ビデオ プロジェクターを MultiPoint Services システムに接続できます。 USB ハブベースのステーションと多機能ハブベースのステーションの両方について、プロジェクターをステーションに接続するための2つのオプションがあります。  
  
-   次の図に示すように、モニターをプロジェクターに置き換えて、そのステーションのディスプレイ デバイスとしてプロジェクターを使用します。  
  
    ![コンピューターに接続されたプロジェクターのイメージ](./media/WMSVideoProjectorConnection.gif)  
  
-   プロジェクターとモニターの両方をステーションのビデオポートに接続するビデオスプリッターデバイスを入手します。  
  
    MultiPoint Services は、両方のディスプレイ デバイスに同じイメージを表示します。 投影しないときはプロジェクターの電源をオフにして、ビデオ モニターだけを使用できます。  
  
どちらかのオプションを使用する場合は、次のことに注意してください。  
  
-   ビデオ ディスプレイを接続するときは、MultiPoint Services が新しいディスプレイを正しく認識できるようにするために、再度*ステーションの関連付け*が必要になる場合があります。 ステーションのビデオディスプレイデバイスに表示される指示に従います。  
  
-   DVI プラグと VGA プラグを変換するには、アダプターまたはコンバーター デバイスを使用する必要がある場合があります。  
  
-   "Y" スプリッター ケーブルを使用すると、両方のビデオ デバイスのビデオ品質が低下する可能性があります。  
  
-   "Y" スプリッター ケーブルを使用してプロジェクターとモニターの両方を使用する場合、MultiPoint Services は、両方のデバイスの画面解像度を、どちらか低い方の最大解像度 (通常はプロジェクター) に調整します。  
  
-   MultiPoint Services では、複数のモニター間での1つのステーションの表示の拡張はサポートされていません。  
  
## <a name="see-also"></a>関連項目  
[ステーション ハードウェアの管理](Manage-Station-Hardware.md)  
[ステーションをセットアップする](Set-Up-a-Station.md) 