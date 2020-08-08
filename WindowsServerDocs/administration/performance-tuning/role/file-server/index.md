---
title: ファイル サーバーのパフォーマンス チューニング
description: Windows Server を実行しているファイル サーバーのパフォーマンス チューニング
ms.topic: article
author: phstee
ms.author: nedpyle; danlo; dkruse; v-tea
ms.date: 12/12/2019
manager: dcscontentpm
audience: Admin
ms.openlocfilehash: ecbd1bc751f133b80cf1d9cb264cf70a4ac4f47c
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992194"
---
# <a name="performance-tuning-for-file-servers"></a>ファイル サーバーのパフォーマンス チューニング

平均負荷、ピーク時の負荷、容量、拡張の計画、応答時間を考慮して、予想されるファイル サーバー負荷に対応できる適切なハードウェアを選択する必要があります。 ハードウェアにボトルネックがあると、ソフトウェア チューニングの効果が限定されます。

## <a name="general-tuning-parameters-for-clients"></a>クライアントの一般的なチューニング パラメーター

次の REG\_DWORD のレジストリ設定は、SMB ファイル サーバーとやり取りするクライアント コンピューターのパフォーマンスに影響を与える可能性があります。

-   **ConnectionCountPerNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerNetworkInterface
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

    既定値は 1 であり、既定値を使用することを強くお勧めします。 有効範囲は、1 から 16 です。 非 RSS インターフェイスのサーバーで確立される、インターフェイスごとの最大接続数です。


-   **ConnectionCountPerRssNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerRssNetworkInterface
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

    既定値は 4 であり、既定値を使用することを強くお勧めします。 有効範囲は、1 から 16 です。 RSS インターフェイスのサーバーで確立される、インターフェイスごとの最大接続数です。

-   **ConnectionCountPerRdmaNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerRdmaNetworkInterface
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

    既定値は 2 であり、既定値を使用することを強くお勧めします。 有効範囲は、1 から 16 です。 RDMA インターフェイスのサーバーで確立される、インターフェイスごとの最大接続数です。

-   **MaximumConnectionCountPerServer**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\MaximumConnectionCountPerServer
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

    既定値は 32 であり、有効範囲は 1 から 64 です。 Windows Server 2012 を実行している単一サーバーで確立される、インターフェイス全体の最大接続数です。

-   **DormantDirectoryTimeout**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantDirectoryTimeout
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

    既定値は 600 秒です。 サーバー ディレクトリのハンドルがディレクトリのリースで開いた状態を維持する最大時間です。

-   **FileInfoCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheLifetime
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定は 10 秒です。 ファイル情報キャッシュのタイムアウト期間です。

-   **DirectoryCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheLifetime
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定は 10 秒です。 これは、ディレクトリ キャッシュのタイムアウトです。

    > [!NOTE]
    > このパラメーターは、ディレクトリのリースがない場合のディレクトリ メタデータのキャッシュを制御します。

     > [!NOTE]
     > Windows 10 バージョン 1803 の既知の問題は、Windows 10 が大規模なディレクトリをキャッシュする機能に影響します。 コンピューターを Windows 10 バージョン 1803 にアップグレードした後、ユーザーは何千ものファイルとフォルダーが含まれているネットワーク共有にアクセスし、その共有にあるドキュメントを開きます。 どちらの操作でも大幅な遅延が発生します。
     >
     > この問題を解決するには、Windows 10 バージョン 1809 以降のバージョンをインストールします。
     >
     > この問題を回避するには、**DirectoryCacheLifetime** を **0** に設定します。
     >
     > この問題は、Windows 10 の次のエディションに影響します。
     > - Windows 10 Enterprise バージョン 1803
     > - Windows 10 Pro for Workstations バージョン 1803
     > - Windows 10 Pro Education バージョン 1803
     > - Windows 10 Professional バージョン 1803
     > - Windows 10 Education バージョン 1803
     > - Windows 10 Home バージョン 1803

-   **DirectoryCacheEntrySizeMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntrySizeMax
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定値は 64 KB です。 これは、ディレクトリ キャッシュ エントリの最大サイズです。

-   **FileNotFoundCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheLifetime
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定値は 5 秒です。 見つからなかったファイルのキャッシュのタイムアウト期間です。

-   **CacheFileTimeout**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\CacheFileTimeout
    ```

    適用対象: Windows 8.1、Windows 8、Windows Server 2012、Windows Server 2012 R2、Windows 7

    既定は 10 秒です。 この設定は、ファイルへの最後のハンドルがアプリケーションによって閉じられた後、そのファイルのキャッシュされたデータがリダイレクターで保持される時間 (秒単位) を制御します。

-   **DisableBandwidthThrottling**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableBandwidthThrottling
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定値は 0 です。 既定では、SMB リダイレクターは、ネットワーク関連のタイムアウトを回避するために、待機時間の長いネットワーク接続全体のスループットを調整します。 このレジストリ値を 1 に設定すると、この調整が無効になり、待機時間の長いネットワーク接続でのファイル転送のスループットがより高くなります。

-   **DisableLargeMtu**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableLargeMtu
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定値は、Windows 8 の場合のみ 0 です。 Windows 8 では、SMB リダイレクターは、要求ごとに最大 1 MB のペイロードを転送するため、ファイル転送速度が向上します。 このレジストリ値を 1 に設定すると、要求のサイズは 64 KB に制限されます。 この設定を適用する前に、この設定の影響を評価する必要があります。

-   **RequireSecuritySignature**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\RequireSecuritySignature
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定値は 0 であり、SMB 署名を無効にします。 この値を 1 に変更すると、すべての SMB 通信に対して SMB 署名が有効になり、SMB 署名が無効になっているコンピューターとの SMB 通信が防止されます。 SMB 署名は、CPU コストとネットワークのラウンド トリップを増やす可能性がありますが、man-in-the-middle 攻撃の阻止に役立ちます。 SMB 署名が不要な場合は、すべてのクライアントとサーバーでこのレジストリ値が 0 であることを確認してください。

    詳細については、「[The Basics of SMB Signing](/archive/blogs/josebda/the-basics-of-smb-signing-covering-both-smb1-and-smb2)」(SMB 署名の基本) をご覧ください。

-   **FileInfoCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheEntriesMax
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定値は 64 であり、有効範囲は 1 から 65536 です。 この値は、クライアントがキャッシュできるファイル メタデータの量を決定するために使用されます。 この値を増やすと、大量のファイルへのアクセス時にネットワーク トラフィックを削減してパフォーマンスを向上させることができます。

-   **DirectoryCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntriesMax
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定値は 16 であり、有効範囲は 1 から 4096 です。 この値は、クライアントがキャッシュできるディレクトリ情報の量を決定するために使用されます。 この値を増やすと、大規模なディレクトリへのアクセス時にネットワーク トラフィックを削減してパフォーマンスを向上させることができます。

-   **FileNotFoundCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheEntriesMax
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定値は 128 であり、有効範囲は 1 から 65536 です。 この値は、クライアントがキャッシュできるファイル名情報の量を決定するために使用されます。 この値を増やすと、大量のファイル名へのアクセス時にネットワーク トラフィックを削減してパフォーマンスを向上させることができます。

-   **MaxCmds**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\MaxCmds
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定値は 15 です。 このパラメーターは、1 つのセッションに対する未処理の要求の数を制限します。 この値を増やすとメモリをより多く使用できますが、より深い要求パイプラインを有効にすることでパフォーマンスを向上させることができます。 また、MaxMpxCt とともにこの値を増やすと、FindFirstChangeNotification 呼び出しなどの、多数のファイル要求が長期間未処理であることが原因で発生するエラーを除去することもできます。 このパラメーターは、SMB 2.0 サーバーとの接続には影響しません。

-   **DormantFileLimit**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantFileLimit
    ```

    適用対象: Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Vista、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

    既定値は 1023 です。 このパラメーターでは、アプリケーションがファイルを閉じた後に共有リソース上で開いたままにする必要があるファイルの最大数を指定します。

### <a name="client-tuning-example"></a>クライアントのチューニングの例

クライアント コンピューターの一般的なチューニング パラメーターを使用すると、特に一部の待機時間の長いネットワーク (ブランチ オフィス、データ センター間の通信、ホーム オフィス、モバイル ブロード バンドなど) 上でリモート ファイル共有にアクセスするコンピューターを最適化できます。 この設定は、すべてのコンピューターに最適で妥当というわけでありません。 個々の設定を適用する前に、その影響を評価する必要があります。

| パラメーター                   | 値 | 既定 |
|-----------------------------|-------|---------|
| DisableBandwidthThrottling  | 1     | 0       |
| FileInfoCacheEntriesMax     | 32768 | 64      |
| DirectoryCacheEntriesMax    | 4096  | 16      |
| FileNotFoundCacheEntriesMax | 32768 | 128     |
| MaxCmds                     | 32768 | 15      |



Windows 8 以降では、Windows PowerShell コマンドレットの **Set-SmbClientConfiguration** および **Set-SmbServerConfiguration** を使用して、これらの SMB 設定の多くを構成できます。 レジストリのみの設定は、Windows PowerShell を使用しても構成できます。

```
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecuritySignature -Value 0 -Force
```