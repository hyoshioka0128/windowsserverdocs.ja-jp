---
title: Use local resources on Hyper-V virtual machine with VMConnect
description: VMConnect を使ってローカル リソースを使用するための要件について説明します
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18eface5-7518-4c6b-9282-93e2e3e87492
author: KBDAzure
ms.author: kathyDav
ms.date: 12/06/2016
ms.openlocfilehash: a7e465313c68ee793715aba045cc56a2ca5fd1de
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222841"
---
# <a name="use-local-resources-on-hyper-v-virtual-machine-with-vmconnect"></a>Use local resources on Hyper-V virtual machine with VMConnect

>適用先:Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2

仮想マシン接続 (VMConnect) を使用して、リムーバブル USB フラッシュ ドライブやプリンターなど、仮想マシンでは、コンピューターのローカル リソースを使用できます。 拡張セッション モードを使用して、VMConnect ウィンドウのサイズを変更することもできます。 この記事ではどのホストを構成し、ローカル リソースに仮想マシンのアクセスを提供します。

拡張セッション モードとクリップボードのテキストを入力は、最新の Windows オペレーティング システムを実行する仮想マシンでのみ使用できます。 \(参照してください[ローカル リソースを使用するための要件](#requirements-for-using-local-resources)、後述します。\) 

Ubuntu を実行する仮想マシンでは、次を参照してください。 [Hyper-v VM の Ubuntu 画面の解像度を変更する](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)です。 
  
## <a name="turn-on-enhanced-session-mode-on-a-hyper-v-host"></a>HYPER-V ホストで拡張セッション モードを有効にします。  
場合は、HYPER-V ホストには、Windows 10 または Windows 8.1 が実行される、拡張セッション モードは既定で、ため、これをスキップして次のセクションに移動することができます。 ホストは、Windows Server 2016 または Windows Server 2012 R2 を実行する場合が最初に実行します。 
  
拡張セッション モードを有効にします。

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
  
## <a name="choose-a-local-resource"></a>ローカル リソースを選択します。

ローカル リソースには、プリンターには、クリップボード、VMConnect を実行しているコンピューター上のローカル ドライブが含まれます。 詳細については、次を参照してください。[ローカル リソースを使用するための要件](#requirements-for-using-local-resources)、後述します。  
  
ローカル リソースを選択。
  
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
  
-   HYPER-V ホストが必要**拡張セッション モード ポリシー**と**拡張セッション モード**設定が有効にします。  
  
-   VMConnect を使用するコンピューターには、Windows 10、Windows 8.1、Windows Server 2016 または Windows Server 2012 R2 を実行する必要があります。  
  
-   仮想マシンは、リモート デスクトップ サービスを有効にし、ゲスト オペレーティング システムとして Windows 10、Windows 8.1、Windows Server 2016 または Windows Server 2012 R2 を実行に必要です。  
  
利用可能な場合、次のローカル リソースのいずれかの VMConnect と仮想マシンを実行しているコンピューターの要件を満たして両方とサーバー オブジェクトする使用できます。  
  
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
  
## <a name="see-also"></a>関連項目  
[仮想マシンに接続します。](https://technet.microsoft.com/library/cc742407.aspx)  
[HYPER-V にジェネレーション 1 または 2 仮想マシンを作成する必要があります。](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)



