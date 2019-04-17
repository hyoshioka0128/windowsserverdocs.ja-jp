---
title: "AD フォレストの回復 - サーバーの完全回復の実行"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 1a1182a6-4462-4a13-806e-0e642a0d5db2
ms.technology: identity-adfs
ms.openlocfilehash: 5de71cc005e9ec4c1425f9fa805b3c043ab4ea36
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---performing-a-full-server-recovery"></a>AD フォレストの回復 - サーバーの完全回復の実行 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:
 
Windows Server 2016、2012 R2、または 2012 のサーバーの完全回復を実行するのにには、次の手順を使用します。 

## <a name="active-directory-full-server-recovery"></a>Active Directory サーバー全体の回復
サーバーの完全回復は、さまざまなハードウェアまたは別のオペレーティング システムのインスタンスに復元する場合は、必要です。 次に従ってしてください。

- バックアップの数と一致するターゲット サーバーのニーズにドライブの数とサイズ以上に同じにする必要があります。
- ターゲット サーバーがアクセスするために、オペレーティング システム DVD から起動する必要があります、**コンピューターを修復**オプションです。 
- DC が Hyper-v ホストとバックアップで VM で実行されているターゲットは、ネットワークの場所に保存されている場合は、レガシ ネットワーク アダプターをインストールする必要があります。  
- サーバーの完全回復を実行した後する必要があるとは別に、SYSVOL の authoritative restore を実行する」の説明に従って[AD フォレストの回復 - DFSR でレプリケートされた SYSVOL の権限のある同期の実行](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)します。


シナリオに応じて、次の手順のいずれかを使用して完全復元を実行します。  
  
### <a name="perform-a-full-server-restore-with-a-local-backup-with-the-latest-image"></a>最新のイメージをローカル バックアップによるサーバーの完全復元を実行します。
  
1.  Windows セットアップを開始、言語、時刻と通貨の形式、およびキーボードのオプションを指定し、クリックして**次**します。  
2.  をクリックして**コンピューターを修復**します。</br>
![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore1.png)
3.  をクリックして**トラブルシューティング**します。</br>
![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore2.png)
4.  をクリックして**システム イメージの回復**します。</br>
![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore3.png)
5.  をクリックして**Windows Server 2016**します。  
![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore4.png)
6.  ローカル直近のバックアップを復元する場合はクリックして**(推奨)、最新の利用可能なシステム イメージを使用して**] をクリック**[次へ]**します。
![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore5.png)
7.  オプションを指定するようになりましたされます。
    -  ディスクのフォーマットとパーティションに再分割
    -  ドライバーをインストールします。
    -  解除を選択すると、**詳細**ディスクのエラーを自動的に再起動して確認の機能です。  既定では、これらが有効にします。
![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore6.png)
8. をクリックして**次**します。
9. をクリックして**完了**します。  続行することを確認して確認を求められます。  をクリックして**はい**します。  
![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore11.png) 
10. これが完了すると」の説明に従って、SYSVOL の authoritative restore を実行[AD フォレストの回復 - DFSR でレプリケートされた SYSVOL の権限のある同期の実行](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)します。
 

### <a name="perform-a-full-server-restore-with-any-image-local-or-remote"></a>任意のイメージは、ローカルまたはリモートでのサーバーの完全復元を実行します。
1.  Windows セットアップを開始、言語、時刻と通貨の形式、およびキーボードのオプションを指定し、クリックして**次**します。  
2.  をクリックして**コンピューターを修復**します。</br>
3.  をクリックして**トラブルシューティング**、] をクリックして**システム イメージの回復**、] をクリック**Windows Server 2016**します。  
4.  ローカル直近のバックアップを復元する場合はクリックして**システム イメージを選択**] をクリック**次**します。

5.  復元するバックアップの場所を選択します。  イメージがローカルの場合は、一覧から選択できます。  
6.  ネットワーク共有に、イメージがある場合は、選択**詳細**します。  選択することも**詳細**ドライバーをインストールする必要がある場合。
![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore7.png)
7.  クリックすると、ネットワークから復元する場合**詳細**選択**ネットワーク上のシステム イメージの検索**します。  ネットワーク接続を復元するように求め可能性があります。  [OK] を選択します。 </br>
![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore8.png)
8. バックアップの共有の場所 (たとえば、\\\server1\backups) への UNC パスを入力し、をクリックして**OK**します。  \\\192.168.1.3\backups など、ターゲット サーバーの IP アドレスを入力することもできます。  
![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore9.png)
10. 共有にアクセスし、[OK] をクリックする必要な資格情報を入力します。  
11. 今すぐ**を復元するには、日付と時刻システム イメージの選択**] をクリック**[次へ]**します。
12. オプションを指定するようになりましたされます。
    1.   ディスクのフォーマットとパーティションに再分割
    2.   ドライバーをインストールします。
    3.   解除を選択すると、**詳細**ディスクのエラーを自動的に再起動して確認の機能です。  既定では、これらが有効にします。
13. をクリックして**次**します。
14. をクリックして**完了**します。  続行することを確認して確認を求められます。  をクリックして**はい**します。   
15. これが完了すると」の説明に従って、SYSVOL の authoritative restore を実行[AD フォレストの回復 - DFSR でレプリケートされた SYSVOL の権限のある同期の実行](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)します。


### <a name="enabling-the-network-adapter-for-a-network-backup"></a>ネットワーク バックアップ用のネットワーク アダプターを有効にします。
をネットワーク共有から復元する、コマンド プロンプトから、ネットワーク アダプターを有効にする必要がある場合は、次の手順を使用します。

1.  Windows セットアップを開始、言語、時刻と通貨の形式、およびキーボードのオプションを指定し、クリックして**次**します。  
2.  をクリックして**コンピューターを修復**します。 私
3.  をクリックして**トラブルシューティング**、] をクリックして**コマンド プロンプト**します。  
4.  次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    wpeinit  
    ```   
5.  ネットワーク アダプターの名前を確認するには、次のように入力します。  
  
    ```  
    show interfaces  
    ```  
  
     次のコマンドを入力し、各コマンドの後 Enter キーを押します。  
  
    ```  
    netsh  
    ```  
  
    ```  
    interface  
    ```  
  
    ```  
    tcp  
    ```  
  
    ```  
    ipv4  
    ```  
  
    ```  
    set address "Name of Network Adapter" static IPv4 Address SubnetMask IPv4 Gateway Address 1  
    ```  
  
     例えば：  
  
    ```  
    set address "Local Area Connection" static 192.168.1.2 255.0.0.0 192.168.1.1 1  
    ```  
  
     種類`quit`コマンド プロンプトに戻ります。 種類`ipconfig /all`を確認、ネットワーク アダプターには IP アドレスおよび接続を確認するをバックアップ、共有をホストするサーバーの IP アドレスに対して ping を実行してみてください。 完了したら、コマンド プロンプトを閉じます。  
  
6.  これで、ネットワーク アダプターが動作して、復元を完了するのには、上記の手順を選択します。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
