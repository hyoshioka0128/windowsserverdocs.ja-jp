---
ms.assetid: c91c7196-ee0d-4856-8cfb-4c38494ccf1f
title: ワーク フォルダーの概要
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 06/07/2019
description: ワーク フォルダーの概要 - PC やデバイスから作業ファイルにアクセスするための一貫した方法をユーザーに提供する、Windows Server のサーバーの役割です。
ms.openlocfilehash: ca76412a6e623b42718fc4f7589f7053073e0f64
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950193"
---
# <a name="work-folders-overview"></a>ワーク フォルダーの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows 10、Windows 8.1、Windows 7

このトピックでは、Windows Server を実行しているファイル サーバーの役割サービスであるワーク フォルダーについて説明します。ワーク フォルダーは、ユーザーが PC やデバイスから作業ファイルにアクセスするための一貫した方法を提供します。  
  
Windows 10、Windows 7、または Android または iOS デバイスでワークフォルダーをダウンロードまたは使用する場合は、次を参照してください。

- [Windows 10 用のワークフォルダー](https://support.microsoft.com/help/12370/windows-10-work-folders)
- [Windows 7 のワークフォルダー (64 ビットダウンロード)](https://www.microsoft.com/download/details.aspx?id=42558)
- [Windows 7 のワークフォルダー (32 ビットダウンロード)](https://www.microsoft.com/download/details.aspx?id=42559)
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
  
| 機能 | 対象 | 説明 |  
| ------------------- | ------------------ | ----------------- |  
| サーバー マネージャーでワーク フォルダーの役割サービスを使用 | Windows Server 2019、Windows Server 2016、または Windows Server 2012 R2 | ファイル サービスと記憶域サービスは、同期共有 (ユーザーの作業ファイルを格納するフォルダー) の設定、ワーク フォルダーの監視、同期共有とユーザー アクセスの管理などを行う方法を提供 |
| ワーク フォルダーのコマンドレット | Windows Server 2019、Windows Server 2016、または Windows Server 2012 R2 | ワーク フォルダー サーバーを管理するための包括的なコマンドレットを含む、Windows PowerShell モジュール |  
| ワーク フォルダーと Windows の統合 | Windows 10<br /><br /> Windows 8.1<br /><br /> Windows RT 8.1<br /><br /> Windows 7 (ダウンロードが必要) | ワーク フォルダーは Windowsコンピューターで次の機能を提供します:<br /><br /> -   ワーク フォルダーの設定と監視を行うコントロール パネルの項目<br />-   エクスプローラーとの統合による、ワーク フォルダーのファイルへの容易なアクセス<br />-   バッテリー残量とシステム パフォーマンスを最大化しながら、集中ファイル サーバーとの間でファイルを転送する同期エンジン |
| デバイス用のワーク フォルダー アプリ | Android<br /><br /> Apple iPhone および iPad® | よく使われるデバイスからワーク フォルダー内のファイルにアクセスできるアプリ |  
  
## <a name="new-and-changed-functionality"></a>新機能と変更された機能
  
ワーク フォルダーの主な変更点を次の表に示します。  
  
| 機能 | 新規/更新 | 説明 |
| ---------------------------- | --------------------- | ----------------- |
| Azure AD アプリケーション プロキシのサポート | Windows 10 バージョン 1703、Android、iOS に追加 | リモート ユーザーは、Azure AD アプリケーション プロキシを使用して、ワーク フォルダー サーバー上のファイルに安全にアクセスできます。 |
| 変更の高速なレプリケーション | Windows 10 および Windows Server 2016 で更新 | Windows Server 2012 R2 では、ワーク フォルダー サーバーにファイルの変更が同期されるときに、クライアントには変更についての通知が送られず、変更内容が反映されるまでに最大で 10 分かかっていました。 Windows Server 2016 を使用している場合、ワークフォルダーサーバーは直ちに Windows 10 クライアントに通知し、ファイルの変更は直ちに同期されます。 この機能は Windows Server 2016 の新機能であり、Windows 10 クライアントが必要です。 古いクライアントを使用しているか、ワーク フォルダー サーバーが Windows Server 2012 R2 である場合、クライアントでは引き続き 10 分ごとに変更を取得します。 |  
| Windows 情報保護 (WIP) との統合 | Windows 10 バージョン 1607 に追加 | 管理者が WIP を展開すると、ワーク フォルダーは PC 上のデータを暗号化してデータ保護を適用できます。 暗号化には、エンタープライズ ID に関連付けられているキーが使用されます。これは Microsoft Intuneなど、サポート対象のモバイル デバイス管理パッケージを使用して、リモート消去することができます。 |  
| Microsoft Office との統合 | Windows 10 バージョン 1511 に追加 | Windows 8.1 では、Office アプリ内から [PC] をクリックまたはタップして、PC 上のワーク フォルダーの場所に移動して、ワーク フォルダーを使用できます。 Windows 10 では、Office がファイルを保存したり開いたりする場所のリストにワークフォルダーを追加して、より容易にワーク フォルダーを使えるようにできます。 詳しくは、「[Windows 10 のワーク フォルダー](https://windows.microsoft.com/windows-10/work-folders-in-windows-10)」および「[Microsoft Office でワークフォルダーを場所として使用する場合のトラブルシューティング](https://social.technet.microsoft.com/wiki/contents/articles/32881.troubleshooting-using-work-folders-as-a-place-in-microsoft-office.aspx)」をご覧ください。 |  
  
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
  
| | ワーク フォルダー | オフライン ファイル | OneDrive for Business | [OneDrive] |
| - | ------------------ | ------------------- | -------------------------- | -------------- |
| **テクノロジの概要** | ファイル サーバーに保存されているファイルを PC やデバイスと同期する | ファイル サーバーに保存されているファイルを、企業ネットワークにアクセスできる PC と同期する (ワーク フォルダーで置き換え可能) | Office 365 または SharePoint に保存されているファイルを、企業ネットワークの内部または外部にある PC およびデバイスと同期したり、またドキュメント コラボレーション機能を提供する | OneDrive に保存されている個人用ファイルを PC、Mac コンピューター、デバイスと同期する |
| **作業ファイルへのユーザーアクセスを提供することを目的としています。** | [はい] | [はい] | [はい] | 必須ではない |
| **クラウド サービス** | None | None | Office 365 | Microsoft OneDrive |
| **内部ネットワークサーバー** | Windows Server 2012 R2 または Windows Server 2016 を実行しているファイル サーバー | ファイル サーバー | SharePoint サーバー (オプション) | None |
| **サポートされているクライアント** | PC、iOS、Android | 企業ネットワーク内の PC、または DirectAccess、VPN、またはその他のリモート アクセス テクノロジを介して接続されている PC | Pc、iOS、Android、Windows Phone | Pc、Mac コンピューター、Windows Phone、iOS、Android |
  
> [!NOTE]
>  前の表に記載された同期テクノロジ以外にも、Microsoft は他のレプリケーション テクノロジを提供しています。たとえば、サーバー間のレプリケーション向けに設計された DFSレプリケーション、支社 WAN アクセラレーション テクノロジとして設計されている BranchCacheなどがあります。 詳しくは、「[DFS 名前空間と DFS レプリケーション](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx)」および「[BranchCache の概要](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx)」をご覧ください。 
  
## <a name="server-manager-information"></a>サーバー マネージャー情報  

ワーク フォルダーは、ファイル サービスと記憶域サービスの役割の一部です。 [役割と機能の追加] ウィザードまたは `Install-WindowsFeature` コマンドレットを使用して、ワーク フォルダーをインストールできます。 いずれの方法でも、下記を行うことができます。  
  
-   [サーバー マネージャー] の **[ファイル サービスと記憶域サービス]** に **[ワーク フォルダー]** ページを追加する  
  
-   同期共有をホストする Windows Server が使用する、Windows 同期共有サービスをインストールする  
  
-   サーバー上のワーク フォルダーを管理する、Windows PowerShell モジュール SyncShare をインストールする  
  
## <a name="interoperability-with-windows-azure-virtual-machines"></a>Windows Azure Virtual Machines との相互運用性

 この Windows Server ロール サービスは、Windows Azure の仮想マシンで実行できます。 このシナリオは、Windows Server 2012 R2 および Windows Server 2016 でテストされました。  
  
Windows Azure 仮想マシンを使い始める方法については、[Windows Azure の Web サイト](http://www.windowsazure.com/documentation/services/virtual-machines)を参照してください。  
  
## <a name="see-also"></a>「

 その他の関連情報については、次の情報を参照してください。  
  
| コンテンツの種類 | 参照先 |
| ------------------ | ---------------- |
| **製品評価** | [Android 用のワークフォルダーの -   –リリース](https://blogs.technet.microsoft.com/filecab/2016/03/16/work-folders-for-android-released)(ブログの投稿)<br />[iOS 用ワークフォルダーの -   – IPad アプリのリリース](https://blogs.technet.com/b/filecab/archive/2015/01/16/work-folders-for-ios-ipad-app-release.aspx)(ブログの投稿)<br />[Windows Server 2012 R2 でのワークフォルダーの導入](https://blogs.technet.com/b/filecab/archive/2013/07/09/introducing-work-folders-on-windows-server-2012-r2.aspx)-   (ブログの投稿)<br />-   [ワークフォルダーの概要](https://channel9.msdn.com/posts/Introduction-to-Work-Folders)(Channel 9 ビデオ)<br />[ワークフォルダーのテストラボの展開](https://blogs.technet.com/b/filecab/archive/2013/07/10/work-folders-test-lab-deployment.aspx)の -   (ブログの投稿)<br />[Windows 7 のワークフォルダーの](https://blogs.technet.com/b/filecab/archive/2014/04/24/work-folders-for-windows-7.aspx)-   (ブログの投稿) |
| **展開** | [ワークフォルダーの実装の設計](plan-work-folders.md)-   <br />[ワークフォルダーの展開](deploy-work-folders.md)-   <br />[AD FS と Web アプリケーションプロキシ (WAP) を使用したワークフォルダーの展開](deploy-work-folders-adfs-overview.md)-   <br />[Azure AD アプリケーションプロキシを使用してワークフォルダーを展開](https://blogs.technet.microsoft.com/filecab/2017/05/31/enable-remote-access-to-work-folders-using-azure-active-directory-application-proxy/)する -   <br />- [オフラインファイル (CSC) からワークフォルダーへの移行ガイド](https://blogs.technet.microsoft.com/filecab/2016/08/12/offline-files-csc-to-work-folders-migration-guide/)<br />[ワークフォルダーの展開のパフォーマンスに関する考慮事項](https://blogs.technet.com/b/filecab/archive/2013/11/01/performance-considerations-for-large-scale-work-folders-deployments.aspx)-   <br />[Windows 7 のワークフォルダーの -   (64 ビットダウンロード)](https://www.microsoft.com/download/details.aspx?id=42558)<br />[Windows 7 のワークフォルダーの -   (32 ビットダウンロード)](https://www.microsoft.com/download/details.aspx?id=42559) |
| **運用** | [ワークフォルダー iPad アプリの -   : FAQ](https://windows.microsoft.com/windows/work-folders-ipad-faq) (ユーザー向け)<br />[ワークフォルダーの証明書管理](https://blogs.technet.com/b/filecab/archive/2013/08/09/work-folders-certificate-management.aspx)の -   (ブログの投稿)<br />-   [Windows Server 2012 R2 ワークフォルダーの展開の監視](https://blogs.technet.com/b/filecab/archive/2013/10/15/monitoring-windows-server-2012-r2-work-folders-deployments.aspx)(ブログの投稿)<br />[Windows PowerShell での Syncshare (ワークフォルダー) コマンドレットの](https://docs.microsoft.com/powershell/module/syncshare/?view=win10-ps)-   <br />-   [ストレージとファイルサービスの PowerShell コマンドレット Windows Server 2012 R2 Preview Edition のクイックリファレンスカード](https://blogs.technet.com/b/filecab/archive/2013/07/30/storage-and-file-services-powershell-cmdlets-quick-reference-card-for-windows-server-2012-r2-preview-edition.aspx) |
| **トラブルシューティング** | -   [Windows Server 2012 R2 – IIS Web サイトおよびワークフォルダーとのポートの競合の解決](https://blogs.technet.com/b/filecab/archive/2013/10/15/windows-server-2012-r2-resolving-port-conflict-with-iis-websites-and-work-folders.aspx)(ブログの投稿)<br />[ワークフォルダーでの一般的なエラーの](https://social.technet.microsoft.com/wiki/contents/articles/30578.common-errors-in-work-folders.aspx)-    |
| **コミュニティ リソース** | -   [ファイルサービスとストレージフォーラム](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverfiles)<br />[Microsoft-ファイルキャビネットブログのストレージチーム](https://blogs.technet.com/b/filecab/)-   <br />[ディレクトリサービスチームのブログに質問 -   には](https://blogs.technet.com/b/askds/) |  
| **関連テクノロジ** | [Windows Server 2016 の -   ストレージ](../storage.md)<br>[ファイルサービスおよび記憶域サービスの](https://technet.microsoft.com/library/hh831487(v=ws.11).aspx)-   <br />-   [ファイルサーバーリソースマネージャー](https://technet.microsoft.com/library/hh831701(v=ws.11).aspx)<br />-   [フォルダーリダイレクト、オフラインファイル、移動ユーザープロファイル](https://technet.microsoft.com/library/hh848267(v=ws.11).aspx)<br />[BranchCache](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx)の -   <br />[DFS 名前空間と DFS レプリケーションの](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx)-    |
