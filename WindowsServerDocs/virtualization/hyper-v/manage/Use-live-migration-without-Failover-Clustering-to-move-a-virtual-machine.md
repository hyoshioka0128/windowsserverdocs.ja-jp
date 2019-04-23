---
title: フェールオーバー クラスタ リングのないライブ マイグレーションを使用して仮想マシンを移動するには
description: 前提条件と、スタンドアロン環境でのライブ マイグレーションを行うための手順を示します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75c32e42-97f7-48df-aac9-1d82d34825e1
author: KBDAzure
ms.author: kathydav
ms.date: 01/17/2017
ms.openlocfilehash: a33912e09d664296f6eda964c40177353718d49c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851543"
---
# <a name="use-live-migration-without-failover-clustering-to-move-a-virtual-machine"></a>フェールオーバー クラスタ リングのないライブ マイグレーションを使用して仮想マシンを移動するには

>適用先:Windows Server 2016

この記事では、フェールオーバー クラスタ リングを使用せず、ライブ移行の手順を実行して仮想マシンを移動する方法を説明します。 ライブ マイグレーションは、著しいダウンタイムなしの HYPER-V ホスト間で実行中の仮想マシンを移動します。   
  
これを行うには、必要があります。   

- ローカル HYPER-V Administrators グループまたはソースと宛先の両方のコンピューターの Administrators グループのメンバーであるユーザー アカウント。 
  
- Windows Server 2016 または Windows Server 2012 R2 で HYPER-V ロールでは、元と移行先サーバーにインストールされているし、ライブ マイグレーション用に設定します。 仮想マシンは、少なくとも場合は、Windows Server 2016 および Windows Server 2012 R2 を実行しているホスト間のライブ マイグレーションを行うことができますバージョン 5。 <br>バージョンのアップグレード手順については、次を参照してください。 [Windows 10 または Windows Server 2016 での Hyper-v で仮想マシンのアップグレード バージョン](..\deploy\Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)します。 インストール手順については、次を参照してください。[ライブ マイグレーションのホスト設定](../deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md)します。 
  
- 送信元または送信先のサーバーで、ツールがインストールされていない場合は、Windows Server 2016 または Windows 10 を実行しているコンピューターにインストールされている HYPER-V 管理ツールは、そこからそれらを実行します。  
   
## <a name="BKMK_Step3"></a>HYPER-V マネージャーを使用して、実行中の仮想マシンを移動するには  
  
1.  Hyper-V マネージャーを開きます。 (サーバー マネージャーで、クリックして **ツールの** >>**Hyper V マネージャー**.)  
  
2.  ナビゲーション ウィンドウで、サーバーのいずれかを選択します。 (表示されていない場合は右クリック **HYPER-V マネージャーで**, 、 をクリックして **サーバーへの接続**, サーバー名を入力し、クリックして、 **OK**します。 繰り返してサーバーを追加します。)  
  
3.  **仮想マシン**  ウィンドウで、仮想マシンを右クリックし、順にクリックして **移動**します。 移動ウィザードが開きます。 
  
4.  ウィザードのページを使用すると、移動、移行先サーバー、およびオプションの種類を選択できます。
  
5.  **[要約]** ページで、選択を確認し、**[完了]** をクリックします。  

## <a name="use-windows-powershell-to-move-a-running-virtual-machine"></a>Windows PowerShell を使用して、実行中の仮想マシンを移動するには
  
次の例は、という名前のバーチャル マシンを移動する MOVE-VM コマンドレットを使用して *LMTest* という名前の移行先サーバーに *TestServer02* 仮想ハード ディスクとその他のファイル、そのようなチェックポイント、およびスマート ページング ファイルを移動して、 *D:\LMTest* ディレクトリ、移行先サーバーにします。  
  
```  
PS C:\> Move-VM LMTest TestServer02 -IncludeStorage -DestinationStoragePath D:\LMTest  
```  
  
## <a name="troubleshooting"></a>トラブルシューティング

### <a name="failed-to-establish-a-connection"></a>接続を確立できませんでした。 

制約付き委任をセットアップしていない場合、仮想マシンを移動するには移行元サーバーにサインインする必要があります。 これを行わない場合は、エラーが発生する認証の試行は失敗し、このメッセージが表示されます。  
  
"バーチャル マシンの移行操作は、移行元で失敗しました。  
ホストとの接続を確立できませんでした*コンピューター名*:資格情報がない 0x8009030E セキュリティ パッケージで使用できます。"
  
 この問題を解決する、移行元サーバーにサインインし、移動を実行してください再します。 ライブ マイグレーションを実行する前に、移行元サーバーにサインインすることを回避するのには、制約付き委任を設定します。 ドメイン管理者の資格情報を制約付き委任を設定する必要があります。 手順については、次を参照してください。 [ライブ マイグレーションのためのホスト設定](../deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md)します。 
 
 ### <a name="failed-because-the-host-hardware-isnt-compatible"></a>ホストのハードウェア互換性がないために失敗しました
 
 場合は、バーチャル マシンは、プロセッサの互換性をオンになっていないし、1 つ以上のスナップショットを持つ、ホストが異なるバージョンのプロセッサがある場合、移行が失敗します。 エラーが発生し、このメッセージが表示されます。
 
**仮想マシンは、対象のコンピューターに移動できません。移行先コンピューターのハードウェアは、この仮想マシンのハードウェア要件と互換性がありません。**
 
 この問題を解決するには、仮想マシンをシャット ダウンし、プロセッサの互換性設定を有効にします。
 
1. HYPER-V マネージャーからの **仮想マシン**  ウィンドウが仮想マシンを右クリックし、設定 をクリックします。
2. ナビゲーション ウィンドウで **[プロセッサ]** をクリック **互換性**します。
3. 確認 **異なるプロセッサ バージョンがコンピューターへ移行する**です。
4. **[OK]** をクリックします。
 
 Windows PowerShell を使用する、 [Set-vmprocessor](https://technet.microsoft.com/library/hh848533.aspx) コマンドレット。
 
  ```
  PS C:\> Set-VMProcessor TestVM -CompatibilityForMigrationEnabled $true
  ```