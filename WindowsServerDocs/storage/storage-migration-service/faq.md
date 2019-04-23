---
title: よく寄せられる質問 (FAQ) の記憶域の移行サービス
description: 別の 1 つのサーバーから移行する場合、どのようなファイルが転送から除外するなどの記憶域の移行サービスについてよく寄せられる質問。
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 11/06/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: df03f722b7b36a163693f675a2eaade2fabeb82f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860913"
---
# <a name="storage-migration-service-frequently-asked-questions-faq"></a>よく寄せられる質問 (FAQ) の記憶域の移行サービス

このトピックを使用してに関するよく寄せられる質問 (Faq) への回答を含む[記憶域の移行サービス](overview.md)サーバーを移行します。

## <a name="excluded-files"></a> どのようなファイルとフォルダーは、転送から除外されますか。

記憶域の移行サービスには、Windows オペレーションに干渉する可能性がわかっているファイルやフォルダーを転送しません。 具体的には、ここでは、どのようなしません転送 PreExistingData フォルダーに、先に移動します。

- Windows では、プログラム ファイル、Program Files (x86)、Program Data, ユーザー
- $Recycle.bin、recycler、Recycled、システム ボリューム情報、$UpgDrv$、$SysReset、$Windows ~ $Windows。 bt によって ~ %.*ls、Windows.old、ブート、回復、Documents and Settings。
- pagefile.sys, hiberfil.sys, swapfile.sys, winpepge.sys, config.sys, bootsect.bak, bootmgr, bootnxt
- ファイルやフォルダーと競合する移行元サーバーで、変換先のフォルダーを除外します。 <br>たとえば、N:\Windows フォルダーがソースであるし、C:\ にマップされます。ボリューム、先に転送されませんの取得-含まれるものに関係なく — ため先に C:\Windows システム フォルダーに影響すること。

## <a name="domain-migration"></a> ドメインの移行がサポートされますか。

記憶域の移行サービスは、Active Directory ドメイン間の移行を許可されません。 常にサーバー間の移行は、移行先サーバーに同じドメインに参加します。 Active Directory フォレスト内の別のドメインからの移行の資格情報を使用できます。 記憶域の移行サービスは、ワークグループ間の移行はサポートします。  

## <a name="cluster-support"></a> クラスターは、ソースまたは変換先としてサポートされますか。

現時点で記憶域の移行サービスは Windows Server 2019 のクラスター間で移行します。 記憶域の移行サービスの今後のリリースのクラスター サポートを追加する予定です。

## <a name="local-principals"></a> ローカル グループとローカル ユーザーを移行しますか。

現在は記憶域の移行サービスを移行するは、ローカルのユーザーまたは Windows Server 2019 内のローカル グループ。 ローカル ユーザーとローカル グループの移行は、記憶域の移行サービスの今後のリリースでサポートを追加する予定です。

## <a name="domain-controller"></a> ドメイン コント ローラーへの移行がサポートされますか。

記憶域の移行サービスでは、Windows Server 2019 のドメイン コント ローラーが移行現在しません。 この問題を回避するを Active Directory ドメインでは、複数のドメイン コント ローラーがある限り、降格する前に、ドメイン コント ローラー カット オーバーの完了後、変換先を昇格し、移行します。 記憶域の移行サービスの今後のリリースでドメイン コント ローラーの移行のサポートを追加する予定です。

## <a name="share-attributes"></a> 記憶域の移行サービスでは、どのような属性を移行しますか。

記憶域の移行サービスは、すべてのフラグ、設定、およびセキュリティの SMB 共有を移行します。 記憶域の移行サービスに移行するフラグの一覧は次のとおりです。

    - 共有状態
    - 可用性の種類
    - 共有の種類
    - フォルダーの列挙モード*とも呼ばれるアクセス ベースの列挙 (ABE)*
    - キャッシュ モード
    - リースのモード
    - Smb インスタンス
    - CA のタイムアウト
    - 同時ユーザー数の制限
    - 継続的に使用できます。
    - 説明           
    - データを暗号化します。
    - Identity のリモート処理
    - インフラストラクチャ
    - 名前
    - パス
    - スコープ
    - スコープ名
    - セキュリティ記述子
    - シャドウ コピー
    - 特別です
    - 一時

## <a name="move-db"></a> 記憶域の移行サービス データベースを移動することができますか。

記憶域の移行サービスでは、既定で非表示の c:\programdata\microsoft\storagemigrationservice フォルダーにインストールされている拡張可能なストレージ エンジン (ESE) データベースを使用します。 ジョブが追加され、転送が完了し、移行後に大幅なドライブの領域を消費する、このデータベースは拡張が数百万のファイルの場合、ジョブを削除しないでください。 データベースを移動する場合は、次の手順に従います。

1. Orchestrator コンピューターの「記憶域の移行サービス」サービスを停止します。
2. 所有権を取得、`%programdata%/Microsoft/StorageMigrationService`フォルダー
3. 完全に制御を共有するユーザー アカウントとすべてのファイルとサブフォルダーを追加します。
4. Orchestrator コンピューターのフォルダーを別のドライブに移動します。
5. 次のレジストリの REG_SZ 値を設定します。

    HKEY_Local_Machine\Software\Microsoft\SMS DatabasePath =*別のボリュームに新しいデータベース フォルダーのパスを*します。 
6. システムがすべてのファイルとフォルダーのサブフォルダーへのフル コントロールを持っていることを確認します。
7. 自分のアカウントのアクセス許可を削除します。
8. 「記憶域の移行サービス」サービスを開始します。

## <a name="transfer-threads"></a> 同時にコピーされるファイルの数を増やすことができますか。

記憶域の移行サービスのプロキシ サービスは、特定のジョブで同時に 8 つのファイルをコピーします。 このサービスは、セットアップ先のコンピューターが Windows Server 2012 R2 または Windows Server 2016 の場合は、転送中に、orchestrator で実行しますが、すべての Windows Server 2019 移行先ノード上でも実行されます。 SMS のプロキシを実行しているすべてのノードでは、10 進数で次のレジストリ REG_DWORD 値の名前を調整することによって、同時コピーのスレッドの数を増やすことができます。

    HKEY_Local_Machine\Software\Microsoft\SMSProxy
    FileTransferThreadCount

 有効範囲は、Windows Server 2019 では、1 ~ 128 です。 

 変更した後に、移行ではすべてのコンピューター partipating 上の記憶域の移行サービスのプロキシ サービスを再起動する必要があります。 記憶域の移行サービスの今後のバージョンでは、この値を大きく予定です。

## <a name="non-windows"></a> Windows Server 以外のソースから移行できますか。

Windows Server 2019 に付属して記憶域の移行サービスのバージョンでは、Windows Server 2003 以降のオペレーティング システムからの移行をサポートします。 現在、Linux、Samba、NetApp、EMC、またはその他の SAN および NAS ストレージ デバイスから移行できません。 記憶域の移行サービス, Linux Samba サポート開始の将来のバージョンでこれを可能にする予定です。

## <a name="previous-versions"></a> 以前のバージョンのファイルを移行できますか。

Windows Server 2019 の付属ストレージ移行サービスのバージョンでは、移行する以前のバージョンで作成されたボリュームのシャドウ コピー サービス) のファイルをサポートしていません。 現在のバージョンのみが移行されます。 

## <a name="ntfs-refs"></a> REFS を NTFS から移行できますか。

Windows Server 2019 の付属ストレージ移行サービスのバージョンでは、NTFS から REFS ファイル システムへの移行をサポートしていません。 NTFS から NTFS および ReFS を REFS に移行することができます。 これは、機能、メタデータ、および NTFS から ReFS が重複していない他の側面では、多くの違いのための仕様です。 ReFS では、アプリケーションのワークロード ファイル システム、一般的なファイル システムではありません。 詳細については、次を参照してください[Resilient File System (ReFS) の概要。](../refs/refs-overview.md)

## <a name="consolidate-servers"></a> 1 つのサーバーに複数のサーバーを統合できますか。

Windows Server 2019 の付属ストレージ移行サービスのバージョンでは、1 つのサーバーに複数のサーバーの統合をサポートしていません。 -同じ共有名があります。 次の 3 つの別のソース サーバーの統合の例を移行すると、ローカル ファイル パス - これらのパスと、重複または競合の発生を防ぐための共有を仮想化を 1 つの新しいサーバーに 3 つすべてに回答しました前のサーバー名と IP アドレス。 記憶域の移行サービスの今後のバージョンでこの機能を追加する可能性があります。  


## <a name="give-feedback"></a> バグの報告、フィードバックを提供またはサポートを受けるには、オプションとは

記憶域の移行サービスのフィードバック。

- クリックする「の機能」をお勧めします「と"Windows Server"のカテゴリとサブカテゴリの「記憶域の移行」を指定する Windows 10 でフィードバック ハブ ツールを使用して
- 使用して、 [Windows Server UserVoice](https://windowsserver.uservoice.com)サイト
- 電子メール smsfeed@microsoft.com

バグ報告します。

- 「レポートの問題」をクリックし、"Windows Server"のカテゴリとサブカテゴリの「記憶域の移行」を指定する、Windows 10 でフィードバック ハブ ツールを使用してください。
- 使用してサポート ケースを開く[マイクロソフトのサポート](https://support.microsoft.com)

サポートを受けるには。

 - 質問を投稿、 [Windows Server Tech コミュニティ](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server)
 - 投稿、 [Windows Server 2019 Technet フォーラム](https://social.technet.microsoft.com/Forums/en-US/home?forum=ws2019&filter=alltypes&sort=lastpostdesc) 
 - 使用してサポート ケースを開く[マイクロソフトのサポート](https://support.microsoft.com)


## <a name="see-also"></a>関連項目

- [記憶域の移行サービスの概要](overview.md)
