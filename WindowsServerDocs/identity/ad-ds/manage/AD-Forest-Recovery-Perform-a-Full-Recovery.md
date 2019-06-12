---
title: AD フォレストの回復 - サーバーの完全回復を実行します。
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 1a1182a6-4462-4a13-806e-0e642a0d5db2
ms.technology: identity-adds
ms.openlocfilehash: 9cf89c9f4875f602abea89e366cadfba8d0599c3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443011"
---
# <a name="ad-forest-recovery---performing-a-full-server-recovery"></a>AD フォレストの回復 - サーバーの完全回復を実行します。 

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

Windows Server 2016、2012 R2、または 2012 用のサーバーの完全回復を実行するのにには、次の手順を使用します。 

## <a name="active-directory-full-server-recovery"></a>Active Directory サーバー全体の回復

サーバー全体の回復は、別のハードウェアまたはオペレーティング システムの異なるインスタンスに復元する場合は、必要があります。 次の点に留意してください。

- ターゲット サーバーがバックアップ内の数と同じでする必要がドライブの数とサイズ以上に同じである必要があります。
- ターゲット サーバーがアクセスするには、オペレーティング システム DVD から起動する必要があります、**コンピューターの修復**オプション。 
- Hyper-v ホストと、バックアップで DC が VM で実行されているターゲットがネットワークの場所に格納されている場合は、レガシ ネットワーク アダプターをインストールする必要があります。 
- サーバーの完全回復を実行した後必要があります、SYSVOL の authoritative restore を個別に実行する」の説明に従って[DFSR でレプリケートされた SYSVOL の権限のある同期の実行 - AD フォレストの回復](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)します。

シナリオによっては、完全な復元を実行するのに手順は次のいずれかを使用します。 
  
## <a name="perform-a-full-server-restore-with-a-local-backup-with-the-latest-image"></a>最新のイメージをローカルのバックアップによるサーバーの完全復元を実行します。
  
1. Windows セットアップを開始し、言語、時間と通貨の形式とキーボード オプションを指定しをクリックして**次**します。 
2. **[コンピューターの修復]** をクリックします。
   ![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore1.png)
3. **[トラブルシューティング]** をクリックします。</br>
   ![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore2.png)
4. クリックして**システム イメージの回復**します。</br>
   ![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore3.png)
5. クリックして**Windows Server 2016**します。 
   ![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore4.png)
6. 最新のローカル バックアップを復元する場合にクリックします **(推奨)、最新の利用可能なシステム イメージを使用して、**  をクリック**次**。
   ![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore5.png)
7. ためのオプションを提供するようになりましたされます。
   -  ディスクをフォーマットしてパーティションを再作成
   -  ドライバーをインストールします。
   -  選択解除、**詳細**ディスク エラーを自動的に再起動して確認の機能です。 既定ではこれらを有効にします。
   ![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore6.png)
8. **[次へ]** をクリックします。
9. **[Finish]** (完了) をクリックします。 続行することを確認して確認を求められます。 **[はい]** をクリックします。 
   ![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore11.png) 
10. これが完了」の説明に従って、SYSVOL の authoritative restore を実行[DFSR でレプリケートされた SYSVOL の権限のある同期の実行 - AD フォレストの回復](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)します。

## <a name="perform-a-full-server-restore-with-any-image-local-or-remote"></a>任意のイメージは、ローカルまたはリモートでのサーバーの完全復元を実行します。

1. Windows セットアップを開始し、言語、時間と通貨の形式とキーボード オプションを指定しをクリックして**次**します。 
2. **[コンピューターの修復]** をクリックします。</br>
3. クリックして**トラブルシューティング**、 をクリックして**システム イメージの回復**、 をクリック**Windows Server 2016**します。 
4. 最新のローカル バックアップを復元する場合にクリックします**システム イメージを選択** をクリック**次**します。
5. 復元するバックアップの場所を選択します。 イメージがローカルの場合は、一覧から選択できます。 
6. イメージがネットワーク共有上にある場合は、選択**詳細**します。 選択することも**詳細**ドライバーをインストールする必要がある場合。
   ![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore7.png)
7. クリックした後、ネットワークから復元する場合**詳細**選択 **、ネットワーク上のシステム イメージの検索**。 ネットワーク接続を復元するように求める可能性があります。 [Ok] を選択します。 </br>
   ![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore8.png)
8. バックアップ共有の場所への UNC パスを入力 (たとえば、 \\\server1\backups) をクリック**OK**します。 など、ターゲット サーバーの IP アドレスを入力することもできます。 \\\192.168.1.3\backups します。 
   ![サーバーの復元](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore9.png)
9. 共有へのアクセスし、[ok] をクリックします。 必要な資格情報を入力します。 
10. 今すぐ**を復元するには、日付と時刻システム イメージの選択** をクリック**次**します。
11. ためのオプションを提供するようになりましたされます。
    - ディスクをフォーマットしてパーティションを再作成
    - ドライバーをインストールします。
    - 選択解除、**詳細**ディスク エラーを自動的に再起動して確認の機能です。 既定ではこれらを有効にします。
12. **[次へ]** をクリックします。
13. **[Finish]** (完了) をクリックします。 続行することを確認して確認を求められます。 **[はい]** をクリックします。  
14. これが完了」の説明に従って、SYSVOL の authoritative restore を実行[DFSR でレプリケートされた SYSVOL の権限のある同期の実行 - AD フォレストの回復](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)します。

## <a name="enabling-the-network-adapter-for-a-network-backup"></a>ネットワークのバックアップ用のネットワーク アダプターを有効にします。

ネットワーク共有から復元するコマンド プロンプトからのネットワーク アダプターを有効にする必要がある場合は、次の手順を使用します。

1. Windows セットアップを開始し、言語、時間と通貨の形式とキーボード オプションを指定しをクリックして**次**します。 
2. **[コンピューターの修復]** をクリックします。 I
3. クリックして**トラブルシューティング**、 をクリックして**コマンド プロンプト**します。 
4. 次のコマンドを入力し、Enter キーを押します。  

   ```  
   wpeinit  
   ```

5. ネットワーク アダプターの名前を確認するには、次のように入力します。  

   ```  
   show interfaces  
   ```  

   次のコマンドを入力し、各コマンドの後 ENTER キーを押します。  

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

   次に、例を示します。  
  
   ```  
   set address "Local Area Connection" static 192.168.1.2 255.0.0.0 192.168.1.1 1  
   ```  

   型`quit`コマンド プロンプトに戻ります。 型`ipconfig /all`ネットワークを確認するアダプターには、IP アドレスと接続の確認、バックアップ共有をホストするサーバーの IP アドレスに ping を実行してください。 完了したら、コマンド プロンプトを閉じます。 

6. これで、ネットワーク アダプターを使用すると、復元を完了する前の手順を選択します。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
