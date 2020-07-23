---
title: SMB ファイル転送速度の低下
description: SMB ファイル転送のパフォーマンスの問題をトラブルシューティングする方法について説明します。
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: cb575015ea8a8fc6cbc35358103774a931b0b749
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958864"
---
# <a name="slow-smb-files-transfer-speed"></a>SMB ファイル転送速度の低下

この記事では、SMB によるファイル転送速度の低下に関する推奨されるトラブルシューティング手順について説明します。

## <a name="large-file-transfer-is-slow"></a>大きなファイル転送速度が遅い

大きなファイルの転送速度が遅い場合は、次の手順を検討してください。

- バッファーされていない IO (**xcopy/j**または**robocopy/j**) に対して、ファイルコピーコマンドを実行してください。

- ストレージの速度をテストします。 これは、ファイルコピーの速度がストレージの速度によって制限されるためです。

- ファイルのコピーはすぐに開始され、その後速度が低下することがあります。 この状況を確認するには、次のガイドラインに従ってください。
    
  - これは通常、初期コピーがキャッシュまたはバッファー (メモリ内または RAID コントローラーのメモリキャッシュ内) にある場合に発生し、キャッシュは実行されます。これにより、データは強制的にディスクに直接書き込まれます (書き込み)。 これは、処理速度が遅いプロセスです。
    
  - ストレージパフォーマンスモニターカウンターを使用して、時間の経過と共にストレージのパフォーマンスが低下するかどうかを判断します。 詳細については、「 [SMB ファイルサーバーのパフォーマンスチューニング](../../../administration/performance-tuning/role/file-server/smb-file-server.md)」を参照してください。

- RAMMap (SysInternals) を使用して、メモリ内の "マップされたファイル" の使用状況が空きメモリ不足のために増加するのを停止するかどうかを判断します。

- トレースのパケット損失を検索します。 これにより、TCP 輻輳プロバイダーによって調整が発生する可能性があります。

- SMBv3 以降のバージョンでは、SMB マルチチャネルが有効で動作していることを確認してください。

- SMB クライアントで、SMB の大きな MTU を有効にし、帯域幅調整を無効にします。 そのためには、次のコマンドを実行します。  
  
  ```PowerShell
  Set-SmbClientConfiguration -EnableBandwidthThrottling 0 -EnableLargeMtu 1
  ```

## <a name="small-file-transfer-is-slow"></a>小さいファイル転送の速度が遅い

SMB による小さいファイルの転送速度の低下は、多くのファイルが存在する場合に最もよく発生します。 これは予想される現象です。

ファイルの転送中に、ファイルの作成により、高レベルのプロトコルオーバーヘッドと高いファイルシステムのオーバーヘッドが発生します。 大きなファイル転送の場合、これらのコストは1回だけ発生します。 多数の小さなファイルが転送されると、コストが繰り返し発生し、転送速度が低下します。

この問題に関する技術的な詳細は次のとおりです。

- SMB は、ファイルの作成を要求する create コマンドを呼び出します。 コードによっては、ファイルが存在するかどうかがチェックされ、ファイルが作成されます。 または、create コマンドの一部のバリエーションによって、実際のファイルが作成されます。

- 各 create コマンドは、ファイルシステムに対してアクティビティを生成します。

- データが書き込まれると、ファイルは閉じられます。

- しばらくの間、プロセスはネットワーク待ち時間や SMB サーバーの待機時間に影響します。 これは、SMB 要求が最初にファイルシステムコマンドに変換され、その後、実際のファイルシステムの待機時間がその操作を完了するためです。

- ウイルス対策プログラムが実行されている場合、転送速度が低下します。 これは、通常、データはパケットスニッファによって1回スキャンされ、ディスクに書き込まれるときに2回スキャンされるためです。 シナリオによっては、これらのアクションが何千も繰り返される場合があります。 1 MB/秒未満で速度が低下する可能性があります。

## <a name="opening-office-documents-is-slow"></a>Office ドキュメントを開くのに時間がかかる

この問題は、通常、WAN 接続で発生します。 これは一般的に、Office アプリ (特に Microsoft Excel) がデータにアクセスしてデータを読み取る方法に起因します。

Office と SMB のバイナリが最新であることを確認し、SMB サーバーでリースが無効になっていることを確認することをお勧めします。 その手順は次のとおりです。
   
1. Windows 8 と Windows Server 2012 以降のバージョンの Windows で、次の PowerShell コマンドを実行します。
      
   ```PowerShell
   Set-SmbServerConfiguration -EnableLeasing $false  
   ```
      
   または、管理者特権のコマンドプロンプトウィンドウで次のコマンドを実行します。  

   ```cmd
   REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\lanmanserver\parameters /v DisableLeasing /t REG\_DWORD /d 1 /f  
   ```
      
   > [!NOTE]
   > このレジストリキーを設定した後は、SMB2 リースは付与されませんが、oplock は引き続き利用できます。 この設定は、主にトラブルシューティングのために使用されます。
    
2. ファイルサーバーを再起動するか、**サーバー**サービスを再起動します。 サービスを再起動するには、次のコマンドを実行します。

   ```cmd  
   NET STOP SERVER 
   NET START SERVER
   ```

この問題を回避するには、ファイルをローカルファイルサーバーにレプリケートすることもできます。 詳細については、「 [Aving Office documents to a network server](/office/troubleshoot/office/saving-file-to-network-server-slow)」を参照してください。
