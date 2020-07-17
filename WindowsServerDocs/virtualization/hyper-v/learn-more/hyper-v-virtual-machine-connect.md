---
title: Hyper-V 仮想マシン接続
description: 仮想マシンへのリモート アクセスを提供する仮想マシン接続について説明します。 仮想マシンへの Ctrl-Alt-Delete の送信など、一般的なタスクの実行方法に関する詳細が含まれます。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: deae35b9-7647-42b8-b6bf-45645a44c9c4
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 8de3fe607eb9dc0d140fe9f494991cb917b8994f
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80854015"
---
# <a name="hyper-v-virtual-machine-connection"></a>Hyper-V 仮想マシン接続

>適用先:Windows Server 2016、Windows 10、Windows 8.1、Windows Server 2012 R2、Windows Server 2012、Windows 8

仮想マシン接続 \(VMConnect\) は、仮想マシンへの接続に使用するツールです。これにより、仮想マシンでのゲスト オペレーティング システムのインストールや操作が可能になります。 VMConnect を使用して実行できるタスクの一部を次に示します。  
  
-   仮想マシンの起動とシャットダウン  
  
-   DVD イメージ \(.iso ファイル\) または USB フラッシュ ドライブへの接続  
  
-   チェックポイントの作成  
  
-   仮想マシンの設定を変更する  
    
## <a name="tips-for-using-vmconnect"></a>VMConnect の使用に関するヒント  
VMConnect を使用する場合は、次の情報が役立つことがあります。  
  
|目的|操作内容|  
|---------------|------------|  
|マウスのクリックや仮想マシンにキーボード入力を送信します。|仮想マシンのウィンドウで、任意の場所をクリックします。 実行中の仮想マシンに接続するときが小さな点として、マウス ポインターがあります。|  
|戻り値のマウスのクリックや物理コンピューターのキーボード入力|Ctrl \+ Alt \+ 左方向キーを押してから、仮想マシン ウィンドウの外にマウス ポインターを移動します。 このマウス リリースのキーの組み合わせは、Hyper\-V マネージャーの [Hyper\-V の設定] で変更できます。|  
|Ctrl \+ Alt \+ Delete キーの組み合わせを仮想マシンに送信する|**[アクション]**  >  **[Ctrl\+Alt\+Delele]** を選択するか、Ctrl \+ Alt \+ End キーの組み合わせを使用します。|  
|ウィンドウ モードから全画面表示モードに切り替える|**[表示]**  >  **[全画面表示モード]** を選択します。 ウィンドウ モードに戻すには、Ctrl \+ Alt \+Break キーを押します。|  
|トラブルシューティングの目的でマシンの現在の状態をキャプチャするためのチェックポイントを作成する|**[アクション]**  >  **[チェックポイント]** を選択するか、Ctrl \+ N キーの組み合わせを使用します。|  
|仮想マシンの設定を変更します。|**[ファイル]**  >  **[設定]** を選択します。|  
|DVD イメージ \(.iso ファイル\) または仮想フロッピー ディスク \(.vfd ファイル\) に接続する|**[メディア]** を選択します。<p>第 2 世代仮想マシンでは、バーチャル フロッピー ディスクはサポートされていません。 詳細については、「[Hyper-V で第 1 世代または第 2 世代の仮想マシンを作成する必要がありますか](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)」を参照してください。|  
|Hyper\-V 仮想マシンで ホストのローカル リソース (USB フラッシュ ドライブなど) を使用する|Hyper-V ホストで拡張セッション モードを有効にし、VMConnect を使用して仮想マシンに接続します。なお、接続する前に、使用するローカル リソースを選択します。 具体的な手順については、「[MConnect を使って Hyper\-V 仮想マシン上でローカル リソースを使用する](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)」を参照してください。|  
|仮想マシンの保存した VMConnect 設定を変更する|Windows PowerShell またはコマンド プロンプトで、次のコマンドを実行します。<p>`VMConnect.exe <ServerName> <VMName> /edit`|  
|VMConnect ユーザーが別のユーザーの VMConnect セッションを乗っ取らないようにする|[Hyper-V ホストで拡張セッション モードを有効にします](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host)。<p>拡張セッション モードが有効になっていないと、セキュリティおよびプライバシーのリスクが生じる可能性があります。 ユーザーが VMConnect を使用して仮想マシンに接続およびログオンしていて、別の承認されたユーザーが同じ仮想マシンに接続すると、2 番目のユーザーがそのセッションを引き継ぎ、最初のユーザーはセッションから切断されます。 2 番目のユーザーは、最初のユーザーのデスクトップ、ドキュメント、およびアプリケーションを表示できます。|
|VM が Hyper-V ホストと通信できるようにする統合サービスまたはコンポーネントを管理する| Windows 10 または Windows Server 2016 を実行している Hyper-V ホストでは、VMConnect を使用して統合サービスを管理することはできません。 次のトピックを参照してください。 <br />- [Hyper-V ホストから統合サービスを有効または無効にする](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics) <br />- [Windows 仮想マシンから統合サービスを有効または無効にする](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-windows)<br />- [Linux 仮想マシンから統合サービスを有効または無効にする](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-linux) <br />- [仮想マシンの統合サービスが更新された状態を維持する](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#integration-service-maintenance)  <br />Windows Server 2012 または Windows Server 2012 R2 を実行しているホストについては、「[統合サービス](https://technet.microsoft.com/library/dn798297(v=ws.11).aspx)」を参照してください。|
|VMConnect ウィンドウのサイズを変更する|Windows オペレーティング システムを実行している第 2 世代仮想マシンでは、VMConnect ウィンドウのサイズを変更できます。 これを行うには、Hyper-V ホストで拡張セッション モードを有効にしなければならない場合があります。 詳細については、「[Hyper-V ホストで拡張セッション モードを有効にする](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host)」を参照してください。 Ubuntu を実行する仮想マシンでは、次を参照してください。 [Hyper-v VM の Ubuntu 画面の解像度を変更する](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)です。|


## <a name="keyboard-shortcuts"></a>キーボード ショートカット  
既定では、キーボード入力とマウス クリックは、仮想マシンに送信されます。 そのため、次のショートカット キーを使用する前に、Ctrl + Alt + 左方向キーを押すことが必要な場合があります。 

|キーの組み合わせ|説明|  
|-------------------|---------------|  
|Ctrl \+ Alt \+ 左方向キー|マウスのリリース|  
|Ctrl \+ Alt \+ End|仮想マシンでの Ctrl \+ Alt \+ Delete と同等|  
|Ctrl \+ Alt \+ Break|全画面表示モードを ウィンドウ モードに切り替える|  
|Ctrl \+ O|仮想マシンの設定を開く|  
|Ctrl \+ S|仮想マシンを起動する|  
|Ctrl \+ N|チェックポイントの作成|  
|Ctrl \+ E|チェックポイントを元に戻す|  
|Ctrl \+ C|画面のキャプチャを行う|  

## <a name="see-also"></a>参照  
-   [VMConnect を使って Hyper-V 仮想マシン上でローカル リソースを使用する](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)  
-   [Windows Server 2016 の Hyper-V](../Hyper-V-on-Windows-Server.md)  
-   [Windows 10 の Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/windows_welcome)  
  
  
