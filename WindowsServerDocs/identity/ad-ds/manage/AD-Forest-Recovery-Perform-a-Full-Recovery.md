---
title: AD フォレストの回復-サーバーの完全回復の実行
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 1a1182a6-4462-4a13-806e-0e642a0d5db2
ms.technology: identity-adds
ms.openlocfilehash: 1ade1f2e316387fbe84209c1bc7a986fff6f2a71
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390543"
---
# <a name="ad-forest-recovery---performing-a-full-server-recovery"></a>AD フォレストの回復-サーバーの完全回復の実行 

>適用先:Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

Windows Server 2016、2012 R2、または2012のサーバーの完全復旧を実行するには、次の手順に従います。 

## <a name="active-directory-full-server-recovery"></a>サーバーの完全復旧の Active Directory

別のハードウェアまたは別のオペレーティングシステムのインスタンスに復元する場合は、完全なサーバー回復が必要です。 次の点に留意してください。

- 対象サーバー上のドライブの数は、バックアップ内の数値と同じである必要があり、同じサイズ以上である必要があります。
- 対象サーバーは、 **[コンピューターの修復]** オプションにアクセスするために、オペレーティングシステム DVD から起動する必要があります。 
- ターゲット DC が Hyper-v 上の VM で実行されていて、バックアップがネットワーク上の場所に格納されている場合は、レガシネットワークアダプターをインストールする必要があります。 
- サーバーの完全復旧を実行した後、「 [AD フォレストの回復-DFSR によってレプリケートされた sysvol の権限のある同期を実行](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)する」の説明に従って、SYSVOL の authoritative restore を個別に実行する必要があります。

シナリオによっては、次のいずれかの手順に従って完全な復元を実行します。 
  
## <a name="perform-a-full-server-restore-with-a-local-backup-with-the-latest-image"></a>最新のイメージでローカルバックアップを使用してサーバーの完全復元を実行する
  
1. Windows セットアップを開始するには、言語、時刻と通貨の形式、およびキーボードのオプションを指定し、 **[次へ]** をクリックします。 
2. **[コンピューターの修復]** をクリックします。
   ![Server Restore @ no__t-1
3. **[トラブルシューティング]** をクリックします。</br>
   ![Server Restore @ no__t-1
4. **[システムイメージの回復]** をクリックします。</br>
   ![Server Restore @ no__t-1
5. **[Windows Server 2016]** をクリックします。 
   ![Server Restore @ no__t-1
6. 最新のローカルバックアップを復元する場合は、使用 **[可能な最新のシステムイメージを使用する (推奨)]** をクリックし、 **[次へ]** をクリックします。
   ![Server Restore @ no__t-1
7. 次のオプションが表示されます。
   -  ディスクのフォーマットと再パーティション
   -  ドライバーのインストール
   -  自動的に再起動し、ディスクエラーをチェックする**高度な**機能の選択を解除します。 これらは既定で有効になっています。
   ![Server Restore @ no__t-1
8. **[次へ]** をクリックします。
9. **[完了]** をクリックします。 続行するかどうかを確認するメッセージが表示されます。 **[はい]** をクリックします。 
   ![Server Restore @ no__t-1 
10. これが完了したら、「 [AD フォレストの回復-DFSR によってレプリケートされた sysvol の権限のある同期を実行する](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)」の説明に従って、SYSVOL の authoritative restore を実行します。

## <a name="perform-a-full-server-restore-with-any-image-local-or-remote"></a>ローカルまたはリモートで任意のイメージを使用してサーバーの完全復元を実行する

1. Windows セットアップを開始するには、言語、時刻と通貨の形式、およびキーボードのオプションを指定し、 **[次へ]** をクリックします。 
2. **[コンピューターの修復]** をクリックします。</br>
3. **[トラブルシューティング]** をクリックし、 **[システムイメージの回復]** をクリックして、 **[Windows Server 2016]** をクリックします。 
4. 最新のローカルバックアップを復元する場合は、 **[システムイメージの選択]** をクリックし、 **[次へ]** をクリックします。
5. ここで、復元するバックアップの場所を選択できます。 画像がローカルの場合は、一覧から選択できます。 
6. イメージがネットワーク共有上にある場合は、 **[詳細設定]** を選択します。 ドライバーをインストールする必要がある場合は、 **[詳細設定]** を選択することもできます。
   ![Server Restore @ no__t-1
7. **[詳細設定]** をクリックした後にネットワークから復元する場合は **、[ネットワーク上のシステムイメージを検索**する] を選択します。 ネットワーク接続を復元するように求めるメッセージが表示される場合があります。 [Ok] を選択します。 </br>
   ![Server Restore @ no__t-1
8. バックアップ共有の場所への UNC パス (たとえば、\\ \ server1\backups) を入力し、[ **OK]** をクリックします。 また、ターゲットサーバーの IP アドレス (\\ \ 192.168.1.3 \ バックアップなど) を入力することもできます。 
   ![Server Restore @ no__t-1
9. 共有にアクセスするために必要な資格情報を入力し、[OK] をクリックします。 
10. **復元するシステムイメージの日付と時刻を選択**し、 **[次へ]** をクリックします。
11. 次のオプションが表示されます。
    - ディスクのフォーマットと再パーティション
    - ドライバーのインストール
    - 自動的に再起動し、ディスクエラーをチェックする**高度な**機能の選択を解除します。 これらは既定で有効になっています。
12. **[次へ]** をクリックします。
13. **[完了]** をクリックします。 続行するかどうかを確認するメッセージが表示されます。 **[はい]** をクリックします。  
14. これが完了したら、「 [AD フォレストの回復-DFSR によってレプリケートされた sysvol の権限のある同期を実行する](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)」の説明に従って、SYSVOL の authoritative restore を実行します。

## <a name="enabling-the-network-adapter-for-a-network-backup"></a>ネットワークバックアップ用にネットワークアダプターを有効にする

ネットワーク共有から復元するために、コマンドプロンプトからネットワークアダプターを有効にする必要がある場合は、次の手順を実行します。

1. Windows セットアップを開始するには、言語、時刻と通貨の形式、およびキーボードのオプションを指定し、 **[次へ]** をクリックします。 
2. **[コンピューターの修復]** をクリックします。 I
3. **[トラブルシューティング]** をクリックし、 **[コマンドプロンプト]** をクリックします。 
4. 次のコマンドを入力し、Enter キーを押します。  

   ```  
   wpeinit  
   ```

5. ネットワークアダプターの名前を確認するには、次のように入力します。  

   ```  
   show interfaces  
   ```  

   次のコマンドを入力し、各コマンドの後に enter キーを押します。  

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

   以下に例を示します。  
  
   ```  
   set address "Local Area Connection" static 192.168.1.2 255.0.0.0 192.168.1.1 1  
   ```  

   コマンドプロンプトに戻るには、「`quit`」と入力します。 「@No__t-0」と入力して、ネットワークアダプターに IP アドレスがあることを確認し、バックアップ共有をホストしているサーバーの IP アドレスに対して ping を実行し、接続を確認します。 完了したら、コマンドプロンプトを閉じます。 

6. ネットワークアダプターが動作しているので、上記の手順を選択して復元を完了します。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
