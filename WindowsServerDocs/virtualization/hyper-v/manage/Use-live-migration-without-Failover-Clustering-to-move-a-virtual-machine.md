---
title: フェールオーバー クラスタ リングのないライブ マイグレーションを使用して仮想マシンを移動するには
description: スタンドアロン環境でライブマイグレーションを実行するための前提条件と手順について説明します。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75c32e42-97f7-48df-aac9-1d82d34825e1
author: KBDAzure
ms.author: kathydav
ms.date: 01/17/2017
ms.openlocfilehash: 55c96ff4696871e4013c3abd6247209d0d4517c0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392557"
---
# <a name="use-live-migration-without-failover-clustering-to-move-a-virtual-machine"></a>フェールオーバー クラスタ リングのないライブ マイグレーションを使用して仮想マシンを移動するには

>適用先:Windows Server 2016

この記事では、フェールオーバー クラスタ リングを使用せず、ライブ移行の手順を実行して仮想マシンを移動する方法を説明します。 ライブ マイグレーションは、著しいダウンタイムなしの HYPER-V ホスト間で実行中の仮想マシンを移動します。   
  
これを行うには、必要があります。   

- ローカル HYPER-V Administrators グループまたはソースと宛先の両方のコンピューターの Administrators グループのメンバーであるユーザー アカウント。 
  
- 移行元サーバーと移行先サーバーにインストールされ、ライブマイグレーション用に設定されている Windows Server 2016 または Windows Server 2012 R2 の Hyper-v の役割。 Windows Server 2016 と Windows Server 2012 R2 を実行しているホスト間でライブマイグレーションを実行するには、仮想マシンのバージョンが少なくとも5である必要があります。

    バージョンのアップグレード手順については、「 [windows 10 または Windows Server 2016 で hyper-v の仮想マシンのバージョンをアップグレード](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)する」を参照してください。 インストール手順については、「[ライブマイグレーション用にホストを設定](../deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md)する」を参照してください。

- 送信元または送信先のサーバーで、ツールがインストールされていない場合は、Windows Server 2016 または Windows 10 を実行しているコンピューターにインストールされている HYPER-V 管理ツールは、そこからそれらを実行します。  
   
## <a name="use-hyper-v-manager-to-move-a-running-virtual-machine"></a>HYPER-V マネージャーを使用して、実行中の仮想マシンを移動  
  
1.  Hyper-V マネージャーを開きます。 (サーバー マネージャーで、クリックして **ツールの** >>**Hyper V マネージャー**.)  
  
2.  ナビゲーション ウィンドウで、サーバーのいずれかを選択します。 (表示されていない場合は右クリック **HYPER-V マネージャーで**, 、 をクリックして **サーバーへの接続**, サーバー名を入力し、クリックして、 **OK**します。 繰り返してサーバーを追加します。)  
  
3.  **仮想マシン**  ウィンドウで、仮想マシンを右クリックし、順にクリックして **移動**します。 移動ウィザードが開きます。 
  
4.  ウィザードのページを使用すると、移動、移行先サーバー、およびオプションの種類を選択できます。
  
5.  **[要約]** ページで、選択を確認し、 **[完了]** をクリックします。  

## <a name="use-windows-powershell-to-move-a-running-virtual-machine"></a>Windows PowerShell を使用して、実行中の仮想マシンを移動するには
  
次の例は、Move-VM コマンドレットを使用して *LMTest* という名前の仮想マシンを *TestServer02* という名前の移行先サーバーに移動し、仮想ハード ディスクとその他のファイル (チェックポイントやスマート ページング ファイルなど) を移行先サーバーの *D:\LMTest* ディレクトリに移動します。  
  
```  
PS C:\> Move-VM LMTest TestServer02 -IncludeStorage -DestinationStoragePath D:\LMTest  
```  
  
## <a name="troubleshooting"></a>トラブルシューティング

### <a name="failed-to-establish-a-connection"></a>接続を確立できませんでした。 

制約付き委任をセットアップしていない場合、仮想マシンを移動するには移行元サーバーにサインインする必要があります。 これを行わない場合は、エラーが発生する認証の試行は失敗し、このメッセージが表示されます。  
  
"仮想マシンの移行操作は、移行元で失敗しました。  
ホスト*コンピューター名*との接続を確立できませんでした:セキュリティパッケージ0x8009030E で利用できる資格情報がありません。 "
  
 この問題を解決する、移行元サーバーにサインインし、移動を実行してください再します。 ライブ マイグレーションを実行する前に、移行元サーバーにサインインすることを回避するのには、制約付き委任を設定します。 ドメイン管理者の資格情報を制約付き委任を設定する必要があります。 手順については、次を参照してください。 [ライブ マイグレーションのためのホスト設定](../deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md)します。 
 
 ### <a name="failed-because-the-host-hardware-isnt-compatible"></a>ホストのハードウェア互換性がないために失敗しました
 
 プロセッサの互換性がオンになっていない仮想マシンに 1 つ以上のスナップショットがある場合、ホストに異なるバージョンのプロセッサがあると、移行が失敗します。 エラーが発生し、このメッセージが表示されます。
 
**The machine は対象のコンピューターに移動できません。対象のコンピューターのハードウェアが、この仮想マシンのハードウェア要件と互換性がありません。**
 
 この問題を解決するには、仮想マシンをシャット ダウンし、プロセッサの互換性設定を有効にします。
 
1. HYPER-V マネージャーからの **仮想マシン**  ウィンドウが仮想マシンを右クリックし、設定 をクリックします。
2. ナビゲーション ウィンドウで **[プロセッサ]** をクリック **互換性**します。
3. 確認 **異なるプロセッサ バージョンがコンピューターへ移行する**です。
4. **[OK]** をクリックします。
 
   Windows PowerShell を使用する、 [Set-vmprocessor](https://technet.microsoft.com/library/hh848533.aspx) コマンドレット。
 
   ```
   PS C:\> Set-VMProcessor TestVM -CompatibilityForMigrationEnabled $true
   ```