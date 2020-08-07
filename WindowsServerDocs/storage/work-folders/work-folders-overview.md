---
ms.assetid: c91c7196-ee0d-4856-8cfb-4c38494ccf1f
title: ワーク フォルダーの概要
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 06/15/2020
description: ワーク フォルダーの概要 - PC やデバイスから作業ファイルにアクセスするための一貫した方法をユーザーに提供する、Windows Server のサーバーの役割です。
ms.openlocfilehash: 5641ea38a75e79420a5e697c14c0e4e3422aa913
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970069"
---
# <a name="work-folders-overview"></a>ワーク フォルダーの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows 10、Windows 8.1、Windows 7

このトピックでは、Windows Server を実行しているファイル サーバーの役割サービスであるワーク フォルダーについて説明します。ワーク フォルダーは、ユーザーが PC やデバイスから作業ファイルにアクセスするための一貫した方法を提供します。

Windows 10、Windows 7、または Android または iOS デバイスでワークフォルダーをダウンロードまたは使用する場合は、次を参照してください。

- [Windows 10 のワーク フォルダー](https://support.microsoft.com/help/12370/windows-10-work-folders)
- [Windows 7 のワーク フォルダー (64 ビット ダウンロード)](https://www.microsoft.com/download/details.aspx?id=42558)
- [Windows 7 のワーク フォルダー (32 ビット ダウンロード)](https://www.microsoft.com/download/details.aspx?id=42559)
- [IOS 用のワークフォルダー](https://itunes.apple.com/app/work-folders/id950878067)
- [Android 用ワークフォルダー](https://play.google.com/store/apps/details?id=com.microsoft.workfolders)

## <a name="role-description"></a>役割の説明

 ワークロード フォルダーを使用すると、ユーザーは会社用の PC に加えて、個人用のコンピューターやデバイスにも作業ファイルを保存してアクセスできるようになります。これは、BYOD (bring-your-own device) とも呼ばれます。 ユーザーは、アクセスしやすい場所に作業ファイルを保存し、そのファイルにはどこからでもアクセスできます。 組織は、一元管理されたファイル サーバーにファイルを格納し、必要に応じてユーザーのデバイス ポリシー (暗号化とロック画面のパスワードなど) を指定することで、企業のデータを管理します。

 ワーク フォルダーは、フォルダー リダイレクト、オフライン ファイル、およびホーム フォルダーの既存の展開を使って、展開できます。 ワーク フォルダーでは、サーバー上の*同期共有*と呼ばれるフォルダーに、ユーザー ファイルを保存します。 既にユーザー データを含むフォルダーを指定することができるため、サーバーやデータを移行することなく、ワーク フォルダーを採用できます。また既存のソリューションを速やかに停止することもできます。

## <a name="practical-applications"></a>実際の適用例

 管理者は、ワーク フォルダーを使用して、一元的なストレージと組織のデータの制御を維持しながら、作業ファイルへのアクセスをユーザーに提供することができます。 具体的には、ワーク フォルダーを次のように使うことができます。

-   ユーザーの会社用と個人用の PC やデバイスから、作業ファイルにアクセスする、単一ポイントを提供します

-   オフラインのときでも作業ファイルにアクセスでき、PC やデバイスが次にインターネットまたはイントラネットに接続されたときに、集中ファイル サーバーと同期できます。

-   既存のフォルダー リダイレクト、オフライン ファイル、およびホーム フォルダーの展開と共存して展開できます。

-   ファイルの分類やフォルダーのクォータなど、既存のファイル サーバーの管理テクノロジを使用して、ユーザー データを管理できます。

-   セキュリティ ポリシーを指定して、ユーザーの PC やデバイスにワーク フォルダーの暗号化を指示したり、ロック画面のパスワードの使用を指示することができます。

-   ワーク フォルダーでフェールオーバー クラスタ リングを使用して、高可用性ソリューションを提供できます。

## <a name="important-functionality"></a>重要な機能

 ワーク フォルダーには、次の機能が含まれています。

| 機能 | 可用性 | 説明 |
| ------------------- | ------------------ | ----------------- |
| サーバー マネージャーでワーク フォルダーの役割サービスを使用 | Windows Server 2019、Windows Server 2016、または Windows Server 2012 R2 | ファイル サービスと記憶域サービスは、同期共有 (ユーザーの作業ファイルを格納するフォルダー) の設定、ワーク フォルダーの監視、同期共有とユーザー アクセスの管理などを行う方法を提供 |
| ワーク フォルダーのコマンドレット | Windows Server 2019、Windows Server 2016、または Windows Server 2012 R2 | ワーク フォルダー サーバーを管理するための包括的なコマンドレットを含む、Windows PowerShell モジュール |
| ワーク フォルダーと Windows の統合 | Windows 10<p> Windows 8.1<p> Windows RT 8.1<p> Windows 7 (ダウンロードが必要) | ワーク フォルダーは Windowsコンピューターで次の機能を提供します:<p> -   ワーク フォルダーの設定と監視を行うコントロール パネルの項目<br />-   エクスプローラーとの統合による、ワーク フォルダーのファイルへの容易なアクセス<br />-   バッテリー残量とシステム パフォーマンスを最大化しながら、集中ファイル サーバーとの間でファイルを転送する同期エンジン |
| デバイス用のワーク フォルダー アプリ | Android<p> Apple iPhone および iPad® | よく使われるデバイスからワーク フォルダー内のファイルにアクセスできるアプリ |

## <a name="new-and-changed-functionality"></a>新機能と変更された機能

ワーク フォルダーの主な変更点を次の表に示します。

| 機能 | 新規/更新 | 説明 |
| ---------------------------- | --------------------- | ----------------- |
| ログ記録の強化 | Windows Server 2019 の新サービス | ワークフォルダーサーバーのイベントログを使用して、同期アクティビティを監視し、同期セッションに失敗しているユーザーを特定できます。 Microsoft-Windows SyncShare/Operational イベントログでイベント ID 4020 を使用して、同期セッションに失敗しているユーザーを特定します。 Microsoft-Windows-SyncShare/Reporting イベントログでイベント ID 7000 とイベント ID 7001 を使用して、アップロードとダウンロードの同期セッションを正常に完了したユーザーを監視します。 |
| パフォーマンス カウンター | Windows Server 2019 の新サービス | 次のパフォーマンスカウンターが追加されました: 1 秒あたりのダウンロードバイト数、アップロードしたバイト数/秒、接続されたユーザー、1秒あたりのファイルダウンロード数、アップロードしたファイル数/秒、変更の検出、受信要求/秒、および未処理の要求。 |
| サーバーパフォーマンスの向上 | Windows Server 2019 で更新されました | サーバーごとにより多くのユーザーを処理するために、パフォーマンスが向上しました。 サーバーごとの制限はさまざまで、ファイルの数とファイルチャーンに基づいています。 サーバーごとの制限を決定するには、ユーザーを段階的にサーバーに追加する必要があります。 |
| オンデマンドのファイルアクセス | Windows 10 バージョン1803に追加されました | すべてのファイルを表示してアクセスできます。 PC に格納され、オフラインで使用できるファイルを制御します。 ファイルの残りの部分は常に表示され、PC 上の領域を占有しませんが、ワークフォルダーにアクセスするには、ワークフォルダーのファイルサーバーに接続する必要があります。 |
| Azure AD アプリケーション プロキシのサポート | Windows 10 バージョン 1703、Android、iOS に追加 | リモート ユーザーは、Azure AD アプリケーション プロキシを使用して、ワーク フォルダー サーバー上のファイルに安全にアクセスできます。 |
| 変更の高速なレプリケーション | Windows 10 および Windows Server 2016 で更新 | Windows Server 2012 R2 では、ワーク フォルダー サーバーにファイルの変更が同期されるときに、クライアントには変更についての通知が送られず、変更内容が反映されるまでに最大で 10 分かかっていました。 Windows Server 2016 を使用している場合、ワークフォルダーサーバーは直ちに Windows 10 クライアントに通知し、ファイルの変更は直ちに同期されます。 この機能は Windows Server 2016 の新機能であり、Windows 10 クライアントが必要です。 古いクライアントを使用しているか、ワーク フォルダー サーバーが Windows Server 2012 R2 である場合、クライアントでは引き続き 10 分ごとに変更を取得します。 |
| Windows 情報保護 (WIP) との統合 | Windows 10 バージョン 1607 に追加 | 管理者が WIP を展開すると、ワーク フォルダーは PC 上のデータを暗号化してデータ保護を適用できます。 暗号化には、エンタープライズ ID に関連付けられているキーが使用されます。これは Microsoft Intuneなど、サポート対象のモバイル デバイス管理パッケージを使用して、リモート消去することができます。 |

## <a name="software-requirements"></a>ソフトウェア要件

ワーク フォルダーには、ファイル サーバーとネットワーク インフラストラクチャについて、次のソフトウェア要件があります。

-   ユーザーファイルとの同期共有をホストするために Windows Server 2019、Windows Server 2016、または Windows Server 2012 R2 を実行しているサーバー

-   ユーザー ファイルを格納するための NTFS ファイル システムでフォーマットされたボリューム

-   Windows 7 PC でパスワード ポリシーを適用するには、グループ ポリシー パスワード ポリシーを使用する必要があります。 また、ワーク フォルダー パスワード ポリシーから Windows 7 PC を除外する必要もあります (使用している場合)。

-   ワーク フォルダーをホストする各ファイル サーバーのサーバー証明書。 これらの証明書には、ユーザーによって信頼されている証明機関 (CA)、できればパブリック CA から発行された証明書を使用してください。

-   Optional複数のファイルサーバーを使用する場合に、Pc とデバイスを適切なファイルサーバーに自動的に参照できるようにする、Windows Server 2012 R2 のスキーマ拡張を使用した Active Directory Domain Services フォレスト。

ユーザーがインターネット経由で同期できるようにするには、追加の要件があります。

-   組織のリバース プロキシまたはネットワーク ゲートウェイで公開規則を作成することによって、インターネットからサーバーへのアクセスを可能にする機能。

-   (省略可能) パブリックに登録されたドメイン名と、ドメインの追加のパブリック DNS レコードを作成する機能。

-   (省略可能) AD FS の認証を使用する場合、Active Directory フェデレーション サービス (AD FS) インフラストラクチャ。

ワーク フォルダーでは、クライアント コンピューターに次のソフトウェア要件があります。

-   PC およびサーバーは、次のいずれかのオペレーティング システムで動作します。

    -   Windows 10

    -   Windows 8.1

    -   Windows RT 8.1

    -   Windows 7

    -   Android 4.4 KitKat 以降

    -   iOS 10.2 以降

-   Windows 7 PC では、Windows の次のいずれかのエディションを実行している必要があります。

    -   Windows 7 Professional

    -   Windows 7 Ultimate

    -   Windows 7 Enterprise

-   Windows 7 PC は、組織のドメインに参加する必要があります (ワークグループには参加できません)。

-   NTFS フォーマットされたローカル ドライブ上で、ワーク フォルダー内のすべてのユーザー ファイルを格納するのに十分な空き領域。既定の設定のように、ワーク フォルダーがシステム ドライブ上にある場合は、追加で 6 GB の空き領域。 ワーク フォルダーは既定で次の場所を使用します。 **%USERPROFILE%\Work Folders**

     ただし、ユーザーはセットアップ時にこの場所を変更できます (NTFS ファイル システムでフォーマットされた microSD カードや USB ドライブはサポートされている場所ですが、ドライブを取り外すと同期は停止されます)。

     既定では、個々のファイルの最大サイズは 10 GB です。 管理者はファイル サーバー リソース マネージャーのクォータ機能を使用してクォータを実装できますが、ユーザーごとの記憶域の制限はありません。

-   ワーク フォルダーでは、クライアントの仮想マシンについて、仮想マシンの状態のロールバックはサポートされていません。 代わりにシステム イメージ バックアップまたはその他のバックアップ アプリを使って、クライアント仮想マシン内からバックアップと復元処理を実行します。

## <a name="work-folders-compared-to-other-sync-technologies"></a>ワーク フォルダーと他の同期テクノロジの比較

次の表は、Microsoft のさまざまな同期テクノロジの特徴と、それぞれを使用する場合について説明しています。

| | 作業フォルダー | オフライン ファイル | OneDrive for Business | OneDrive |
| - | ------------------ | ------------------- | -------------------------- | -------------- |
| **テクノロジの概要** | ファイル サーバーに保存されているファイルを PC やデバイスと同期する | ファイル サーバーに保存されているファイルを、企業ネットワークにアクセスできる PC と同期する (ワーク フォルダーで置き換え可能) | Office 365 または SharePoint に保存されているファイルを、企業ネットワークの内部または外部にある PC およびデバイスと同期したり、またドキュメント コラボレーション機能を提供する | OneDrive に保存されている個人用ファイルを PC、Mac コンピューター、デバイスと同期する |
| **ユーザーに業務用ファイルへのアクセスを提供** | はい | はい | はい | いいえ |
| **クラウド サービス** | None | None | Office 365 | Microsoft OneDrive |
| **社内ネットワーク サーバー** | Windows Server 2012 R2、Windows Server 2016、および Windows Server 2019 を実行するファイルサーバー | ファイル サーバー | SharePoint サーバー (オプション) | None |
| **サポートされているクライアント** | PC、iOS、Android | 企業ネットワーク内の PC、または DirectAccess、VPN、またはその他のリモート アクセス テクノロジを介して接続されている PC | Pc、iOS、Android、Windows Phone | Pc、Mac コンピューター、Windows Phone、iOS、Android |

> [!NOTE]
>  前の表に記載された同期テクノロジ以外にも、Microsoft は他のレプリケーション テクノロジを提供しています。たとえば、サーバー間のレプリケーション向けに設計された DFSレプリケーション、支社 WAN アクセラレーション テクノロジとして設計されている BranchCacheなどがあります。 詳しくは、「[DFS 名前空間と DFS レプリケーション](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v=ws.11))」および「[BranchCache の概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831696(v=ws.11))」をご覧ください。

## <a name="server-manager-information"></a>サーバー マネージャー情報

ワーク フォルダーは、ファイル サービスと記憶域サービスの役割の一部です。 [役割と機能の追加] ウィザードまたは `Install-WindowsFeature` コマンドレットを使用して、ワーク フォルダーをインストールできます。 いずれの方法でも、下記を行うことができます。

-   [サーバー マネージャー] の **[ファイル サービスと記憶域サービス]** に **[ワーク フォルダー]** ページを追加する

-   同期共有をホストする Windows Server が使用する、Windows 同期共有サービスをインストールする

-   サーバー上のワーク フォルダーを管理する、Windows PowerShell モジュール SyncShare をインストールする

## <a name="interoperability-with-windows-azure-virtual-machines"></a>Windows Azure Virtual Machines との相互運用性

 この Windows Server ロール サービスは、Windows Azure の仮想マシンで実行できます。 このシナリオは、Windows Server 2012 R2、Windows Server 2016、および Windows Server 2019 でテストされています。

Windows Azure 仮想マシンを使い始める方法については、[Windows Azure の Web サイト](https://www.windowsazure.com/documentation/services/virtual-machines)を参照してください。

## <a name="see-also"></a>関連項目

| コンテンツ タイプ | 参考資料 |
| ------------------ | ---------------- |
| **製品評価** | -   [Android のワークフォルダー – リリース済み](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) (ブログ記事)<br />-   [IOS 用ワークフォルダー– IPad アプリリリース](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)(ブログの投稿)<br />-   [Windows Server 2012 R2 のワーク フォルダーの導入](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) (ブログ記事)<br />-   [ワーク フォルダーの概要](https://channel9.msdn.com/posts/Introduction-to-Work-Folders) (Channel 9 ビデオ)<br />-   [ワークフォルダーのテストラボの展開](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)(ブログの投稿)<br />-   [Windows 7 のワークフォルダー](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) (ブログの投稿) |
| **デプロイ** | -   [ワークフォルダーの実装の設計](plan-work-folders.md)<br />-   [ワークフォルダーの展開](deploy-work-folders.md)<br />-   [AD FS と Web アプリケーションプロキシ (WAP) を使用したワークフォルダーの展開](deploy-work-folders-adfs-overview.md)<br />-   [Azure AD アプリケーション プロキシを使ったワーク フォルダーの展開](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)<br />- [オフラインファイル (CSC) からワークフォルダーへの移行ガイド](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)<br />-   [ワークフォルダーの展開のパフォーマンスに関する考慮事項](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)<br />-   [Windows 7 のワークフォルダー (64 ビットダウンロード)](https://www.microsoft.com/download/details.aspx?id=42558)<br />-   [Windows 7 のワークフォルダー (32 ビットダウンロード)](https://www.microsoft.com/download/details.aspx?id=42559) |
| **操作** | -   [ワークフォルダー iPad アプリ: FAQ](https://windows.microsoft.com/windows/work-folders-ipad-faq) (ユーザー向け)<br />-   [ワークフォルダーの証明書の管理](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)(ブログの投稿)<br />-   [Windows Server 2012 R2 ワークフォルダーの展開の監視](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)(ブログの投稿)<br />-   [Windows PowerShell の SyncShare コマンドレット (ワーク フォルダー)](/powershell/module/syncshare/?view=win10-ps)<br />-   [Windows Server 2012 R2 Preview Edition のストレージとファイルサービスの PowerShell コマンドレットのクイックリファレンスカード](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) |
| **トラブルシューティング** | -   [Windows Server 2012 R2 – IIS Web サイトとワーク フォルダーのポート競合の解決](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB) (ブログ記事)<br />-   [ワークフォルダー内の一般的なエラー](https://techcommunity.microsoft.com/t5/storage-at-microsoft/troubleshooting-work-folders-on-windows-client/ba-p/425627) |
| **コミュニティ リソース** | -   [ファイルサービスとストレージフォーラム](https://docs.microsoft.com/answers/topics/windows-server-storage.html)<br />-   [マイクロソフトのストレージ チーム - ファイル キャビネット ブログ](https://techcommunity.microsoft.com/t5/storage-at-microsoft/bg-p/FileCAB)<br />-   [ディレクトリサービスチームのブログを確認する](/archive/blogs/askds/) |
| **関連テクノロジ** | -   [Windows Server 2016 の記憶域](../storage.yml)<br>-   [ファイルサービスおよび記憶域サービス](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831487(v=ws.11))<br />-   [ファイルサーバーリソースマネージャー](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831701(v=ws.11))<br />-   [フォルダーリダイレクト、オフラインファイル、移動ユーザープロファイル](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh848267(v=ws.11))<br />-   [BranchCache](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831696(v=ws.11))<br />-   [DFS 名前空間と DFS レプリケーション](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v=ws.11)) |
