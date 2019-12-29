---
title: Hyper-v 仮想マシン接続
description: 仮想マシンへのリモートアクセスを提供する仮想マシン接続について説明します。 仮想マシンへの Ctrl + Alt-Delete の送信など、一般的なタスクの実行方法の詳細について説明します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fba83d22d9e5d9f31a5809781aa04943cc4cd3af
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364153"
---
# <a name="hyper-v-virtual-machine-connection"></a>Hyper-v 仮想マシン接続

>適用先:Windows Server 2016、Windows 10、Windows 8.1、Windows Server 2012 R2、Windows Server 2012、Windows 8

仮想マシン接続\(vmconnect\)は、仮想マシンに接続するために使用するツールで、仮想マシンにゲストオペレーティングシステムをインストールしたり、ゲストオペレーティングシステムと対話したりすることができます。 VMConnect を使用して実行できるタスクには、次のようなものがあります。  
  
-   仮想マシンの起動とシャットダウン  
  
-   DVD イメージ\(.iso ファイル\)または USB フラッシュドライブに接続する  
  
-   チェックポイントの作成  
  
-   仮想マシンの設定を変更する  
    
## <a name="tips-for-using-vmconnect"></a>VMConnect の使用に関するヒント  
VMConnect の使用に関しては、次の情報が役に立つ場合があります。  
  
|操作方法|操作の実行...|  
|---------------|------------|  
|マウスのクリックや仮想マシンにキーボード入力を送信します。|仮想マシンのウィンドウで、任意の場所をクリックします。 実行中の仮想マシンに接続するときが小さな点として、マウス ポインターがあります。|  
|戻り値のマウスのクリックや物理コンピューターのキーボード入力|CTRL\+ALT\+←キーを押して、仮想マシンウィンドウの外にマウスポインターを移動します。 このマウスリリースキーの組み合わせは、hyper-v\-\-マネージャーの hyper-v 設定で変更できます。|  
|CTRL\+ALT\+キーの組み合わせを仮想マシンに送信する|[**アクション** > ]\+**ctrl\+alt\+Delete**を選択するか、キー\+の組み合わせ ctrl alt END を使用します。|  
|ウィンドウモードから全\-画面表示モードに切り替える|**全画面** **表示** > モードを選択します。 ウィンドウモードに切り替えるには、ctrl\+ALT\+BREAK キーを押します。|  
|トラブルシューティングのためにコンピューターの現在の状態をキャプチャするチェックポイントを作成します|[**アクション** > **チェックポイント**] を選択するか\+、CTRL N キーの組み合わせを使用します。|  
|仮想マシンの設定を変更します。|[**ファイル** > の**設定**] を選択します。|  
|DVD イメージ\(.iso ファイル\)またはバーチャルフロッピーディスク\(.vfd ファイルに接続します。\)|**[メディア]** を選択します。<br /><br />第 2 世代仮想マシンでは、バーチャル フロッピー ディスクはサポートされていません。 詳細については、「 [hyper-v で第1世代または第2世代の仮想マシンを作成する必要がありますか?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)」を参照してください。|  
|USB フラッシュドライブのように、hyper-v\-仮想マシン上のホストのローカルリソースを使用する|Hyper-v ホストで拡張セッションモードを有効にし、VMConnect を使用して仮想マシンに接続します。接続する前に、使用するローカルリソースを選択します。 具体的な手順については、「 [vmconnect\-を使用した hyper-v 仮想マシンでのローカルリソースの使用](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)」を参照してください。|  
|仮想マシンの保存された VMConnect 設定を変更する|Windows PowerShell またはコマンドプロンプトで、次のコマンドを実行します。<br /><br />`VMConnect.exe <ServerName> <VMName> \/edit`|  
|VMConnect ユーザーによる別のユーザーの VMConnect セッションの引き継ぎを禁止する|[Hyper-v ホストで拡張セッションモードを有効に](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host)します。<br /><br />拡張セッションモードが有効になっていないと、セキュリティとプライバシーのリスクが生じる可能性があります。 ユーザーが VMConnect を使用して仮想マシンに接続し、別の承認されたユーザーが同じ仮想マシンに接続している場合は、2番目のユーザーがセッションを引き継ぎ、最初のユーザーがセッションを切断します。 2番目のユーザーは、最初のユーザーのデスクトップ、ドキュメント、およびアプリケーションを表示できます。|
|VM が Hyper-v ホストと通信できるようにする統合サービスまたはコンポーネントを管理する| Windows 10 または Windows Server 2016 を実行している Hyper-v ホストでは、VMConnect を使用して統合サービスを管理することはできません。 次のトピックを参照してください。 <br />- [Hyper-v ホストの統合サービスを有効または無効にする](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics) <br />- [Windows 仮想マシンから統合サービスを有効または無効にする](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-windows)<br />- [Linux 仮想マシンから統合サービスを有効または無効にする](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-linux) <br />- [仮想マシンの統合サービスが更新された状態を維持する](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#integration-service-maintenance)  <br />Windows Server 2012 または Windows Server 2012 R2 を実行しているホストの場合は、「 [Integration Services](https://technet.microsoft.com/library/dn798297(v=ws.11).aspx)」を参照してください。|
|VMConnect ウィンドウのサイズを変更する|Windows オペレーティングシステムを実行している第2世代仮想マシンでは、VMConnect ウィンドウのサイズを変更できます。 これを行うには、Hyper-v ホストで拡張セッションモードを有効にする必要がある場合があります。 詳細については、「 [hyper-v ホストで拡張セッションモードを有効にする](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host)」を参照してください。 Ubuntu を実行する仮想マシンでは、次を参照してください。 [Hyper-v VM の Ubuntu 画面の解像度を変更する](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)です。|


## <a name="keyboard-shortcuts"></a>キーボード ショートカット  
既定では、キーボード入力とマウスクリックが仮想マシンに送信されます。 そのため、次のショートカットキーを使用する前に、CTRL + ALT + ←キーを押す必要がある場合があります。 

|キーの組み合わせ|説明|  
|-------------------|---------------|  
|CTRL\+ALT\+←|マウスのリリース|  
|CTRL\+ALT\+END|仮想マシンで\+の\+CTRL ALT DELETE に相当します。|  
|CTRL\+ALT\+BREAK|全\-画面表示モードからウィンドウモードに切り替える|  
|CTRL\+O|仮想マシンの設定を開きます。|  
|CTRL\+S|仮想マシンを起動します。|  
|CTRL\+N|チェックポイントの作成|  
|CTRL\+E|チェックポイントを元に戻す|  
|CTRL\+C|画面のキャプチャを行う|  

## <a name="see-also"></a>関連項目  
-   [VMConnect を使用して Hyper-v 仮想マシン上のローカルリソースを使用する](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)  
-   [Windows Server 2016 の hyper-v](../Hyper-V-on-Windows-Server.md)  
-   [Windows 10 の hyper-v](https://msdn.microsoft.com/virtualization/hyperv_on_windows/windows_welcome)  
  
  
