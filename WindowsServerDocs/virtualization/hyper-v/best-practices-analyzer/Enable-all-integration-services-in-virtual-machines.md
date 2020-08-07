---
title: 仮想マシンですべての統合サービスを有効にする
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 16e202ad-3795-40c9-8176-7ca319e56d26
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: d1a3fd16be0d85f185efb9ceb9d7b2f690eaae47
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969979"
---
# <a name="enable-all-integration-services-in-virtual-machines"></a>仮想マシンですべての統合サービスを有効にする

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題

*1つ以上の統合サービスが無効になっているか、仮想マシンで動作していません。*

## <a name="impact"></a>影響

*次の仮想マシンでは、サービスまたは統合機能が正しく動作しない可能性があります。*

\<list of virtual machine names>

## <a name="resolution"></a>解決方法

*サービススナップインまたは sc config コマンドラインツールを使用して、サービスが自動的に開始するように構成されていて、停止していないことを確認します。*

#### <a name="to-configure-how-a-service-is-started-using-the-services-snap-in"></a>サービススナップインを使用してサービスを開始する方法を構成するには

1.  リモートデスクトップサービスまたは仮想マシン接続を使用して仮想マシンに接続し、ゲストオペレーティングシステムにログオンします。

2.  [サービス] を開きます。 (をクリックして **開始**, 、内をクリックして、 **検索の開始** ボックスに、入力 **services.msc**, 、ENTER キーを押します)。

3.  詳細ウィンドウで、構成するサービスを右クリックし、[**プロパティ**] をクリックします。

4.  **全般** ] タブの [ **スタートアップ** をクリックして、入力 **自動**です。

#### <a name="to-configure-how-a-service-is-started-using-sc-config"></a>SC Config を使用してサービスを開始する方法を構成するには

1.  Windows PowerShell を開きます。 (デスクトップから [**スタート**] をクリックし、「 **Windows PowerShell**」と入力を開始します)。

2.  右クリック **Windows PowerShell** ] をクリック **管理者として実行**します。

3.  <サービス名> をサービスの名前に置き換え、次のように入力します。

    ```
    sc config <service-name> start=auto
    ```



