---
title: HYPER-V 仮想マシン接続
description: 仮想マシンへのリモート アクセスを提供する仮想マシン接続について説明します。 仮想マシンに送信 Ctrl、alt キーを押し、削除などの一般的なタスクを実行する方法の詳細が含まれています。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: deae35b9-7647-42b8-b6bf-45645a44c9c4
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: e1f3260fdbbd82a97c3b0949936afc6a04ec5e5a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887843"
---
# <a name="hyper-v-virtual-machine-connection"></a>HYPER-V 仮想マシン接続

>適用先:Windows Server 2016、Windows 10、Windows 8.1、Windows Server 2012 R2、Windows Server 2012、Windows 8

仮想マシン接続\(VMConnect\)をインストールするか、仮想マシンでゲスト オペレーティング システムと対話するために、仮想マシンに接続するために使用するツールです。 VMConnect を使用して実行できるタスクの一部を以下に示します。  
  
-   起動し、仮想マシンをシャット ダウン  
  
-   DVD イメージへの接続\(.iso ファイル\)または USB フラッシュ ドライブ  
  
-   チェックポイントの作成  
  
-   仮想マシンの設定を変更する  
    
## <a name="tips-for-using-vmconnect"></a>VMConnect を使用するためのヒント  
次の情報役に立つの VMConnect を使用します。  
  
|これを行う.|これを行う.|  
|---------------|------------|  
|マウスのクリックや仮想マシンにキーボード入力を送信します。|仮想マシンのウィンドウで、任意の場所をクリックします。 実行中の仮想マシンに接続するときが小さな点として、マウス ポインターがあります。|  
|戻り値のマウスのクリックや物理コンピューターのキーボード入力|Ctrl キーを押して\+ALT\+ままに仮想マシンのウィンドウの外部の矢印ボタンをマウス ポインターを移動します。 このマウス リリース キーの組み合わせは、ハイパースレッディングで変更できます\-ハイパー V 設定\-V マネージャー。|  
|Ctrl キーを送信\+ALT\+仮想マシンにキーの組み合わせを削除|選択**アクション** > **ctrl キーを押し\+Alt\+削除**CTRL キーの組み合わせを使用して、または\+alt キーを押し\+終了。|  
|ウィンドウ モードから完全に切り替える\-画面表示モード|選択**ビュー** > **全画面表示モード**します。 ウィンドウ モードに戻るには、ctrl キーを押して\+ALT\+中断します。|  
|トラブルシューティングのマシンの現在の状態をキャプチャするチェックポイントを作成します。|選択**アクション** > **チェックポイント**CTRL キーの組み合わせを使用して、または\+n ください。|  
|仮想マシンの設定を変更します。|選択**ファイル** > **設定**します。|  
|DVD イメージへの接続\(.iso ファイル\)またはバーチャル フロッピー ディスク\(.vfd ファイル\)|選択**メディア**します。<br /><br />第 2 世代仮想マシンでは、バーチャル フロッピー ディスクはサポートされていません。 詳細については、次を参照してください。 [、Hyper-v でジェネレーション 1 または 2 仮想マシンを作成する必要がありますか?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)します。|  
|ハイパースレッディングでホストのローカル リソースを使用して\-USB フラッシュ ドライブと同様に、V 仮想マシン|HYPER-V ホスト上の拡張セッション モードを有効に、仮想マシンに接続する VMConnect を使用して、接続する前に使用するローカル リソースを選択します。 特定の手順では、次を参照してください。[ハイパースレッディングを使用するローカル リソース\-VMConnect を使って仮想マシン](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)します。|  
|変更は、仮想マシンの VMConnect の設定を保存|Windows PowerShell またはコマンド プロンプトで次のコマンドを実行します。<br /><br />`VMConnect.exe <ServerName> <VMName> \/edit`|  
|VMConnect のユーザーが別のユーザーの VMConnect セッション経由で取得するを防ぐ|[HYPER-V ホスト上の拡張セッション モードを有効に](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#BKMK_OVER)します。<br /><br />拡張セッション モードをオンになってもいませんと、セキュリティとプライバシーのリスクが生じる場合があります。 ユーザーが接続されており、ログオンしている場合は、VMConnect と別の権限を持つユーザーを使用して仮想マシンが同じ仮想マシンに接続して 2 番目のユーザー引き継いだセッションは最初のユーザーは、セッションが失われます。 2 番目のユーザーは最初のユーザーのデスクトップ、ドキュメント、およびアプリケーションを表示することになります。|
|Integration services またはコンポーネントが HYPER-V ホストと通信する VM を管理します。| Windows 10 または Windows Server 2016 を実行する HYPER-V ホストでは、VMConnect を使って統合サービスを管理できません。 これらのトピックを参照してください。 <br />- [オンにする]、[HYPER-V ホストから統合サービスをオフにします。](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics) <br />- [オンにする]、[Windows 仮想マシンから統合サービスをオフにします。](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-windows)<br />- [オン/Linux 仮想マシンから統合サービスをオフにします。](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-linux) <br />- [仮想マシンの更新の統合サービスを維持します。](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#integration-service-maintenance)  <br />Windows Server 2012 または Windows Server 2012 R2 を実行するホストの場合は、次を参照してください。 [Integration Services](https://technet.microsoft.com/library/dn798297(v=ws.11).aspx)します。|
|VMConnect ウィンドウのサイズ変更します。|第 2 世代仮想マシン、Windows オペレーティング システムを実行するの VMConnect ウィンドウのサイズを変更することができます。 これを行うには、HYPER-V ホストで拡張セッション モードを有効にする必要があります。 詳細については、次を参照してください。 [、Hyper-v ホスト上の拡張セッション モードを有効に](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#BKMK_OVER)します。 Ubuntu を実行する仮想マシンでは、次を参照してください。 [Hyper-v VM の Ubuntu 画面の解像度を変更する](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)です。|


## <a name="keyboard-shortcuts"></a>キーボード ショートカット  
既定では、キーボードの入力とマウスのクリックは、仮想マシンに送信されます。 CTRL + ALT + 左を押す必要がありますように次のショートカット キーを使用する前に矢印。 

|キーの組み合わせ|説明|  
|-------------------|---------------|  
|Ctrl キーを押し\+ALT\+左矢印|マウスのリリース|  
|CTRL キーを押し\+ALT\+終了|等価の CTRL\+ALT\+仮想マシンの削除|  
|CTRL キーを押し\+ALT\+中断|完全なから切り替える\-画面表示モード ウィンドウ表示モードに戻る|  
|CTRL キーを押し\+O|仮想マシンの設定を開きます|  
|CTRL\+S|仮想マシンを開始します。|  
|CTRL\+N|チェックポイントの作成|  
|CTRL キーを押し\+E|チェックポイントを元に戻す|  
|CTRL\+C|画面のキャプチャを行う|  

## <a name="see-also"></a>関連項目  
-   [VMConnect を使って、HYPER-V 仮想マシン上のローカル リソースの使用](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)  
-   [Windows Server 2016 で Hyper-v](../Hyper-V-on-Windows-Server.md)  
-   [Windows 10 の hyper V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/windows_welcome)  
  
  
