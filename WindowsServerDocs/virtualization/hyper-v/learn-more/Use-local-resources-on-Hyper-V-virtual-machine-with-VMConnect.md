---
title: Use local resources on Hyper-V virtual machine with VMConnect
description: VMConnect でローカル リソースを使用するための要件について説明します
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 18eface5-7518-4c6b-9282-93e2e3e87492
author: kbdazure
ms.author: kathydav
ms.date: 12/06/2016
ms.openlocfilehash: dccc4ccf66d457da9dcc2a71ff8d259565fe2714
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860475"
---
# <a name="use-local-resources-on-hyper-v-virtual-machine-with-vmconnect"></a>Use local resources on Hyper-V virtual machine with VMConnect

>適用先:Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2

仮想マシン接続 (VMConnect) を使用すると、コンピューターのローカル リソース (リムーバブル USB フラッシュ ドライブやプリンターなど) を仮想マシンで使用できます。 拡張セッション モードでは、VMConnect ウィンドウのサイズを変更することもできます。 この記事では、ホストを構成し、仮想マシンにローカル リソースへのアクセス権を付与する方法について説明します。

拡張セッション モードと [クリップボードからテキストを入力] は、最新の Windows オペレーティング システムを実行している仮想マシンでのみ使用できます。 \(以下の「[ローカル リソースを使用するための要件](#requirements-for-using-local-resources)」を参照してください。\) 

Ubuntu を実行する仮想マシンでは、次を参照してください。 [Hyper-v VM の Ubuntu 画面の解像度を変更する](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)です。 
  
## <a name="turn-on-enhanced-session-mode-on-a-hyper-v-host"></a>Hyper-V ホストで拡張セッション モードを有効にする  
Hyper-V ホストで Windows 10 または Windows 8.1 が実行されている場合、拡張セッション モードは既定で有効になっているため、これをスキップして次のセクションに進むことができます。 ただし、ホストで Windows Server 2016 または Windows Server 2012 R2 が実行されている場合は、最初にこれを行ってください。 
  
拡張セッション モードを有効にする:

1.  仮想マシンをホストするコンピューターに接続します。  
  
2.  HYPER-V マネージャーでは、ホストのコンピューター名を選択します。  
  
    ![ホスト コンピューター名のスクリーン ショットは、左側のウィンドウでは、HYPER-V マネージャーで下に表示します。](media/Hyper-V-HyperVManager-HostNameSelected.png)  
  
3.  **[Hyper-V の設定]** を選択します。  
  
    ![右側のウィンドウで 操作の HYPER-V 設定 オプションを示すスクリーン ショット。](media/HyperV-ActionsHyperVSettings.png)  
  
4.  **[サーバー]** で、 **[拡張セッション モード ポリシー]** を選択します。  
  
    ![[セキュリティ] セクションの拡張セッション モード ポリシー オプションを示すスクリーン ショット。](media/Hyper-V-Settings-ServerEnhancedSessionModePolicy.png)  
  
5.  **[拡張セッション モードを許可する]** チェック ボックスをオンにします。  
  
    ![許可する のスクリーン ショットには、拡張セッション モード ポリシーのセッション モードのチェック ボックスが強化されています。](media/Hyper-V-Settings-EnhancedSessionModePolicyCheckBox.png)  
  
6.  **[ユーザー]** で、 **[拡張セッション モード]** を選択します。  
  
    ![[ユーザー] セクションの拡張セッション モードのオプションを示すスクリーン ショット。 ](media/Hyper-V-Settings-UserEnhancedSessionMode.png)  
  
7.  **[拡張セッション モードを許可する]** チェック ボックスをオンにします。  
  
8.  **[OK]** をクリックします。  
  
## <a name="choose-a-local-resource"></a>ローカル リソースを選択する

ローカル リソースには、VMConnect を実行しているコンピューター上のプリンター、クリップボード、およびローカル ドライブが含まれます。 詳細については、以下の「[ローカル リソースを使用するための要件](#requirements-for-using-local-resources)」を参照してください。  
  
ローカル リソースを選択するには:
  
1.  VMConnect を開きます。  
  
2.  接続先の仮想マシンを選択します。  
  
3.  **[オプションの表示]** をクリックします。  
  
    ![ダイアログ ボックスの左下にあるオプションを表示 を呼び出すスクリーン ショット。](media/HyperV-VMConnect-DisplayConfig.png)  
  
4.  **[ローカル リソース]** を選択します。  
  
    ![ローカル リソース タブを呼び出すスクリーン ショット。](media/HyperV-VMConnect-DisplayConfig-LocalResources.png)  
  
5.  **[その他]** をクリックします。  
  
    ![[詳細] ボタンを呼び出すスクリーン ショット。](media/HyperV-VMConnect-DisplayConfig-LocalResourcesMore.png)  
  
6.  仮想マシンで使用するドライブを選択し、 **[OK]** をクリックします。  
  
    ![ローカル リソースおよび選択したドライブを示すスクリーン ショット。](media/HyperV-VMConnect-Settings-LocalResourcesDrives.png)  
  
7.  **[今後この仮想マシンに接続するときのために設定を保存する]** チェック ボックスをオンにします。  
  
    ![このオプションを選択する チェック ボックスを呼び出すスクリーン ショット。](media/HyperV-VMConnect-SaveSettings.png)  
  
8.  **[接続]** をクリックします。  
  
## <a name="edit-vmconnect-settings"></a>VMConnect の設定を編集する

Windows PowerShell またはコマンド プロンプトで次のコマンドを実行することで、VMConnect の接続設定を簡単に編集できます。  
  
`VMConnect.exe <ServerName> <VMName> /edit`  
  
## <a name="requirements-for-using-local-resources"></a>ローカル リソースを使用するための要件

仮想マシン上のコンピューターのローカル リソースを使用できるようにするには。  
  
-   Hyper-V ホストで **[拡張セッション モード ポリシー]** および **[拡張セッション モード]** 設定が有効になっている必要があります。  
  
-   VMConnect を使用するコンピューターでは、Windows 10、Windows 8.1、Windows Server 2016、または Windows Server 2012 R2 が実行されている必要があります。  
  
-   仮想マシンでは、リモート デスクトップ サービスが有効になっていて、Windows 10、Windows 8.1、Windows Server 2016、または Windows Server 2012 R2 がゲスト オペレーティング システムとして実行されている必要があります。  
  
VMConnect を実行しているコンピューターと仮想マシンの両方が要件を満たしている場合は、次のすべてのローカル リソースを使用できます (使用可能な場合)。  
  
-   ディスプレイの構成  
  
-   オーディオ
  
-   プリンター  
  
-   クリップボード (コピーと貼り付け用)  
  
-   スマート カード  
  
-   USB デバイス  
  
-   ドライブ  
  
-   サポートされているプラグ アンド プレイ デバイス  
  
## <a name="why-use-a-computers-local-resources"></a>コンピューターのローカル リソースを使用する理由
コンピューターのローカル リソースを使用して行います。  
  
-   仮想マシンへのネットワーク接続がない状態で仮想マシンをトラブルシューティングする。  
  
-   リモート デスクトップ接続 (RDP) を使ってコピーと貼り付けを行う場合と同じ方法で、仮想マシンとの間でファイルをコピーして貼り付ける。  
  
-   スマート カードを使って仮想マシンにサインインする。  
  
-   仮想マシンからローカル プリンターで印刷する。  
  
-   USB やサウンド リダイレクトを必要とする開発者向けアプリケーションを RDP を使わずにテストおよびトラブルシューティングする。  
  
## <a name="see-also"></a>参照  
[仮想マシンに接続する](https://technet.microsoft.com/library/cc742407.aspx)  
[Hyper-V で第 1 世代または第 2 世代の仮想マシンを作成する必要がありますか](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)



