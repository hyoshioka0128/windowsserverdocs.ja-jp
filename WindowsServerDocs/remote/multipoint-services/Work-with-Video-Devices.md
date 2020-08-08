---
title: ビデオ デバイスの使用
description: ビデオモニターとプロジェクターが MultiPoint Services のステーションを操作する方法について説明します。
ms.topic: article
ms.assetid: 2f7f5a97-efd2-4184-8ad3-cf029d615eab
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: d580185a2fc6adfb3bdf7acc160610aaf4d2b5b9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946835"
---
# <a name="work-with-video-devices"></a>ビデオ デバイスの使用
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

-   "Y" スプリッターケーブルを使用すると、両方のビデオデバイスでビデオの品質が低下する可能性があります。

-   "Y" スプリッターケーブルを介してプロジェクターとモニターの両方を使用する場合、MultiPoint Services では、両方のデバイスの画面の解像度を、いずれかのデバイス (通常はプロジェクター) の最も低い最大解像度に調整します。

-   MultiPoint Services では、複数のモニター間での1つのステーションの表示の拡張はサポートされていません。

## <a name="see-also"></a>参照
[ステーションハードウェア](Manage-Station-Hardware.md) 
 の管理[ステーションを設定する](Set-Up-a-Station.md)