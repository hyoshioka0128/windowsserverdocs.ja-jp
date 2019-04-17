---
title: Windows Server バージョン 1803 の概要
description: 入手、インストール、ライセンス認証の方法
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: jaimeo
ms.localizationpriority: high
ms.date: 05/02/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cf87597-b15d-4f43-8aa1-91e60367f011
ms.openlocfilehash: c5cd8fbcf8424fa158ad31ca64e3eabe426240a6
ms.sourcegitcommit: 8e2903c9b58646840eedd63b47a9bba6c6a06bf7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2018
ms.locfileid: "1859877"
---
# <a name="introducing-windows-server-version-1803"></a>Windows Server バージョン 1803 の概要

>適用対象: Windows Server (半期チャネル)

**Windows Server バージョン 1803 は新しい半期チャネルの現在のリリースです。**


## <a name="what-the-semi-annual-channel-is--and-isnt"></a>半期チャネルとは
Windows Server バージョン 1803 は Windows Server 2016 の "更新プログラム" または "サービス パック" *ではありません*。 これは、変化の激しい開発サイクルへの対応が必要なユーザーなど、"クラウドに適したペース" での進化を希望するユーザーに対応するリリース トラックで行われる、年 2 回のサーバー リリースの現在のリリースです。 このトラックは、最新のアプリケーション、およびコンテナーやマイクロ サービスなどの革新シナリオに最適です。 このトラックの各リリースは、最初のリリースから 18 か月サポートされます。 半期チャネルの詳細および**参加するチャネル (または現在のチャネルを維持すべきかどうか) を決定するためのヒント** については、「[半期チャネルの概要](semi-annual-channel-overview.md)」を参照してください。


**Windows Server 2016 は、現在の長期的なサービス チャネル (LTSC) 製品です**。 LTSC は、従来のワークロードやアプリケーションをサポートするために、サーバー オペレーティング システムの長期的な安定性と予測可能性を必要とする場合に最適です。 LTSC を維持する場合は、Windows Server 2016 をインストールする (または使用を継続する) 必要があります。この場合、Server Core モードまたはデスクトップ エクスペリエンス搭載サーバー モードでインストールすることができます。 詳細については、「[Windows Server 2016 の概要](https://docs.microsoft.com/windows-server/get-started/server-basics)」を参照してください。


## <a name="whats-different-about-windows-server-version-1803"></a>Windows Server のバージョン 1803 の相違点

Windows Server バージョン 1803 は、Server Core モードで実行されます。 Windows Server Core モードには、ハードウェア要件が低い、攻撃対象が非常に少ない、更新プログラムの必要性の削減など、大きな利点があります。 グラフィカル ユーザー インターフェイスがないため、Windows Server Core モードはリモートで最適に管理されます。 Server Core を初めて使用する場合、この環境に慣れるには、「[Server Core サーバーの管理](../administration/server-core/server-core-manage.md)」を参照してください。 「[Windows Server 2016 の管理](../administration/manage-windows-server.md)」では、サーバーをリモートで管理するためのさまざまなオプションを示しています。

「[Windows Server バージョン 1803 の新機能](whats-new-in-windows-server-1803.md)」では、Windows Server バージョン 1803 の新機能と追加された機能について説明します。

### <a name="why-does-windows-server-version-1803-offer-only-the-server-core-installation-option"></a>Windows Server バージョン 1803 で Server Core インストール オプションのみが提供される理由
Windows Server の各リリースの計画で最も重要な手順の 1 つは、お客様からのフィードバック、つまりお客様がどのように Windows Server を使用しているかについて情報を収集することです。 どのような新機能が、Windows Server の展開、言い換えれば、お客様の日常的なビジネスに大きな影響を与えるでしょうか。 お客様からのフィードバックは、新しい技術革新をできるだけ迅速かつ効率的に提供することが最優先であることを示しています。 同時に、最も迅速に技術革新を進めているお客様からは、主に PowerShell でコマンド ライン スクリプトを使用してデータ センターを管理しているため、デスクトップ エクスペリエンス モードでインストールされた Windows Server で利用可能なデスクトップ GUI の必要性は高くないというご意見をいただいています。 Server Core インストール オプションに重点を置くことによって、従来の Windows Server プラットフォームの機能やアプリケーションとの互換性を維持しながら、新しい技術革新により多くのリソースを割り当てることができます。 Windows Server と今後のリリースに関して、この問題を含むさまざまな問題に関するフィードバックがある場合は、[フィードバック Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) を通じてご意見やご提案をお寄せください。


### <a name="what-about-nano-server"></a>Nano Server について
Nano Server は、コンテナー オペレーティング システムとして使用できます。 詳細については、「[Windows Server 半期チャネルでの Nano Server の変更点](nano-in-semi-annual-channel.md)」をご覧ください。

## <a name="additional-information-about-this-release"></a>このリリースに関する追加情報
Windows Server バージョン 1803 に関する重要な情報を総合的に理解するには、インストールの前に以下のトピックを確認してください。

- 実行に必要なハードウェアについては、 この[システム要件](system-requirements.md)を参照してください。このリリースのシステム要件は、Windows Server 2016 と同じです。
- 新機能と追加された機能については、 「[Windows Server バージョン 1803 の新機能](whats-new-in-windows-server-1803.md)」をご覧ください。
- 削除された機能については、 「[Windows Server (バージョン 1803 以降) で削除された機能と置換が計画されている機能](windows-server-1803-removed-features.md)」を参照してください。
- このリリースに固有の回避する必要がある問題については、 「[リリース ノート: Windows Server バージョン 1803 に関する重要な問題](server-1803-release-notes.md)」を参照してください。


## <a name="where-to-obtain-windows-server-version-1803"></a>Windows Server バージョン 1803 を取得する場所

このリリースは、クリーン インストールでインストールする必要があります。

- ボリューム ライセンス サービス センター (VLSC): ボリューム ライセンスのお客様が[ソフトウェア アシュアランス](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx)をご利用の場合は、このリリースを入手できます、[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)に移動して、**[サインイン]** をクリックすることによって、このリリースを入手できます。 次に、**[Downloads and Keys]** (ダウンロードとキー) をクリックし、このリリースを検索します。 

- Windows Server バージョン 1803 もまた、[Microsoft Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.WindowsServer?tab=Overview) で使用可能です。

- Visual Studio サブスクリプション: Visual Studio サブスクライバーは、[Visual Studio サブスクライバー ダウンロード ページ](https://my.visualstudio.com/downloads?pid=2347)からダウンロードしてWindows Server バージョン 1803 を入手することができます。 まだサブスクライバーではない場合は、[Visual Studio サブスクリプション](https://www.visualstudio.com/subscriptions/)にサインアップしてから、上記のように [Visual Studio サブスクライバーのダウンロード ページ](https://my.visualstudio.com/downloads?pid=2347)にアクセスします。 Visual Studio サブスクリプション経由で入手したリリースは、開発とテストにのみ利用できます。




## <a name="activating-windows-server-version-1803"></a>Windows Server バージョン 1803 のライセンス認証

- ボリューム ライセンス サービス センターからこのリリースを入手した場合、キーの管理システム (KMS) 環境で Windows Server 2016 CSVLK を使用してライセンス認証することができます。
- Microsoft Azure を使用している場合、このリリースは自動的にライセンス認証されます。
- Visual Studio サブスクリプションからこのリリースを入手した場合、キー管理システム (KMS) 環境で Windows Server 2016 CSVLK を使用してライセンス認証することができます。 