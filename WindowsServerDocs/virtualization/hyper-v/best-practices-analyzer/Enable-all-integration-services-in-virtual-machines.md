---
title: 仮想マシンのすべての integration services を有効にします。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 16e202ad-3795-40c9-8176-7ca319e56d26
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 307e2d407a0defa14a6b57bda95a2f3ab018406d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829433"
---
# <a name="enable-all-integration-services-in-virtual-machines"></a>仮想マシンのすべての integration services を有効にします。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*1 つまたは複数の統合サービスは、無効になっているか、仮想マシンで動作していません。*  
  
## <a name="impact"></a>影響  
  
*次の仮想マシンのサービスまたは統合機能が正常に動作しません。*  
  
\<仮想マシン名の一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*サービス スナップインまたは sc config コマンド ライン ツールを使用して、サービスが自動的に開始するように構成され、停止していないことを確認します。*  
  
#### <a name="to-configure-how-a-service-is-started-using-the-services-snap-in"></a>書き込み方法、サービスを構成するには、は、開始、サービス スナップインを使用して  
  
1.  リモート デスクトップ サービスまたは仮想マシン接続を使用して、ゲスト オペレーティング システム上の仮想マシンとログに接続します。  
  
2.  [サービス] を開きます。 (をクリックして **開始**, 、内をクリックして、 **検索の開始** ボックスに、入力 **services.msc**, 、ENTER キーを押します)。  
  
3.  詳細ペインで、構成、およびクリックするとなるサービスを右クリックして**プロパティ**します。  
  
4.  **全般** ] タブの [ **スタートアップ** をクリックして、入力 **自動**です。  
  
#### <a name="to-configure-how-a-service-is-started-using-sc-config"></a>方法、サービスを構成するには、を使用して開始 SC Config  
  
1.  Windows PowerShell を開きます。 (デスクトップで、次のようにクリックします**開始**の入力を開始および**Windows PowerShell**。)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  < サービス名 > を交換して、サービスの名前を入力し。  
  
    ```  
    sc config <service-name> start=auto  
    ```  
  


