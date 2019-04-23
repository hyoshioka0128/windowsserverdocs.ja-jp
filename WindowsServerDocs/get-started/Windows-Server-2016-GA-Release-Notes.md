---
title: リリース ノート - Windows Server 2016 に関する重要な問題
description: クラッシュ、ハング、インストールの失敗、データの損失を回避するための回避策を必要とする重大な問題についてまとめます。クラッシュ、ハング、インストールの失敗、データの損失を回避するための回避策を必要とする重大な問題についてまとめます。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 11/13/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 5a25a9152298a38ad77a377a87b71917ee586947
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878653"
---
# <a name="release-notes-important-issues-in-windows-server-2016"></a>リリース ノート:Windows Server 2016 に関する重要な問題

>適用先:Windows Server 2016

これらのリリース ノートは、Windows Server&reg; 2016 オペレーティング システムの最も重大な問題とその回避策 (存在する場合) についてまとめます。 このリリースにおける計画的な変更点、新機能、および修正プログラムについては、「[Windows Server 2016 の新機能](what-s-new-in-windows-server-2016.md)」と特定の機能チームからのお知らせを参照してください。 特に指定がない限り、レポートされる問題はそれぞれ、Windows Server 2016 のすべてのエディションおよびインストール オプションに適用されます。  

このドキュメントは継続的に更新されています。 解決策が必要な重大な問題が発見された場合、および新しい解決策および修正が使用可能になった場合は、ここに追加されます。  

## <a name="express-updates-available-starting-in-november-2018-new"></a>Express 2018 の年 11 月 (新規) で利用できる更新プログラム

2018 年 11 月以降"更新 Tuesday"更新プログラム、Windows は発行がもう一度[更新プログラムを Express](express-updates.md) for Windows Server 2016。 WSUS や System Center Configuration Manager (SCCM) を使用している場合は、Windows Server 2016 更新プログラムの 2 つのパッケージをもう一度表示されます。 完全な更新と Express の更新プログラム。 Express サーバー環境で使用する場合は、サーバーが 2017 年 11 月 (KB # 4048953) Express の更新プログラムが正しくインストールすることを確認するための完全な更新をなったことを確認する必要があります。 2017 11 b の更新 (4048953 KB #) 以降に更新されていないサーバーで高速更新プログラムを試行する場合は、帯域幅と無限ループに CPU リソースを消費する連続のエラーを確認します。 このシナリオが発生した場合は、Express の更新のプッシュを停止し、代わりにエラー ループを停止する場合は、最近使用した完全な更新をプッシュします。  

## <a name="server-core-installation-option"></a>Server Core インストール オプション
[comment]: # (ID:370;送信者: amason;状態: サインオフ)  
Server Core インストール オプションを使用して Windows Server 2016 をインストールすると、プリント サーバーの役割がインストールされていなくても、印刷スプーラーがインストールされ、既定で開始されます。

これを回避するには、初回起動後に、印刷スプーラーを無効に設定します。


## <a name="containers"></a>コンテナー  

[comment]: # (ID:371;送信者: taylorb;状態: サインオフ)  
- コンテナーを使用する前にインストールする[Windows 10 バージョン 1607 のサービス スタック更新プログラム。2016 年 8 月 23 日、](https://support.microsoft.com/en-us/kb/3176936)または利用可能な後で更新します。 それ以外の場合、エラーを構築など、さまざまな問題が発生できます以降、またはコンテナー、およびのようなエラーを実行している"Win32 で CreateProcess が失敗しました。RPC サーバーは使用できません。"

[comment]: # (ID:373;送信者: plang;状態: サインオフ)  
- NanoServerPackage OneGet プロバイダーは、Windows コンテナーでは動作しません。 これを回避するには、(コンテナー以外の) 別のコンピューターで Find-NanoServerPackage および Save-NanoServerPackage を使用して、必要なパッケージをダウンロードします。 その後、ダウンロードしたパッケージをコンテナーにコピーしてインストールします。

## <a name="device-guard"></a>Device Guard
[comment]: # (ID:369;送信者: nirb;状態: サインオフ)
コードの整合性に対する仮想化ベースの保護、またはシールドされた仮想マシン (コードの整合性に対する仮想化ベースの保護を使用します) を利用する場合、これらのテクノロジは一部のデバイスやアプリケーションとの互換性がない可能性があることに注意してください。 運用システムで機能を有効にする前に、ラボでこのような構成をテストする必要があります。 このテストを行わない場合は、予期しないデータの損失や Stop エラーが発生する可能性があります。

## <a name="microsoft-exchange"></a>Microsoft Exchange
[comment]: # (ID:375;送信者: wgries;状態: サインオフ)
Windows Server 2016 で Microsoft Exchange 2016 CU3 を実行しようとすると、IIS ホスト プロセス W3WP.exe でエラーが発生します。 現時点では、回避策はありません。 サポートされる修正プログラムが利用可能になるまでは、Windows Server 2016 での Exchange 2016 CU3 の展開を延期する必要があります。

## <a name="remote-server-administration-tools-rsat"></a>リモート サーバー管理ツール (RSAT)
[comment]: # (ID:374;送信者: ryanpu;状態: サインオフ)
Anniversary Update より前のバージョンの Windows 10 を実行していて、Hyper-V と、仮想トラステッド プラットフォーム モジュールが有効になった仮想マシン (シールドされた仮想マシンを含む) を使用している場合は、Windows Server 2016 用の RSAT バージョンをインストールすると、このような仮想マシンの起動に失敗します。

これを回避するには、RSAT をインストールする前に、クライアント コンピューターを Windows 10 Anniversary Update (以降) にアップグレードします。 この問題が既に発生している場合は、RSAT をアンインストールし、クライアントを Windows 10 Anniversary Update にアップグレードした後、RSAT を再インストールします。


## <a name="shielded-virtual-machines"></a>シールドされた仮想マシン
[comment]: # (ID:369;送信者: nirb;状態: サインオフ)  
- シールドされた仮想マシンを運用環境で展開する前に、利用可能なすべての更新プログラムがインストールされていることを確認します。

- コードの整合性に対する仮想化ベースの保護、またはシールドされた仮想マシン (コードの整合性に対する仮想化ベースの保護を使用します) を利用する場合、これらのテクノロジは一部のデバイスやアプリケーションとの互換性がない可能性があることに注意してください。 運用システムで機能を有効にする前に、ラボでこのような構成をテストする必要があります。 このテストを行わない場合は、予期しないデータの損失や Stop エラーが発生する可能性があります。


## <a name="start-menu"></a>スタート メニュー
[comment]: # (ID:372;送信者: samli;状態: サインオフ)
この問題は、デスクトップ エクスペリエンス搭載サーバー オプションを使用してインストールされた Windows Server 2016 に影響します。

スタート メニューのフォルダー内にショートカット項目を追加するアプリケーションをインストールした場合、そのショートカットを動作させるには、一度ログアウトしてから、もう一度ログインする必要があります。



メインの [Windows Server 2016](Windows-Server-2016.md) ハブに戻ります。

## <a name="storport-performance"></a>Storport のパフォーマンス
Windows Server 2016 を新たにインストールして実行した場合、Windows Server 2012 R2 と比較して、一部のシステムでストレージのパフォーマンスが低下することがあります。  Windows Server 2016 の開発では、プラットフォームのセキュリティと信頼性を強化するため、複数の変更が行われました。 これらの中には、Windows Defender を既定で有効にするなど、I/O パスの延伸につながる変更が含まれているため、特定のワークロードとパターンで I/O パフォーマンスが低下する可能性があります。 Windows Defender は、システム保護のための重要な層であるため、無効にすることはお勧めできません。  

## <a name="copyright"></a>著作権  
このドキュメントは「現状有姿のまま」提供されます。 このドキュメントに記載されている情報および見解 (URL 等のインターネット Web サイトに関する情報を含む) は、将来予告なしに変更されることがあります。  

このドキュメントは、マイクロソフト製品に含まれる知的財産に対していかなる法的権利も付与しません。 お客様は、内部的な参照目的に限り、ドキュメントを複製して使用することができます。  

&copy;2016 Microsoft Corporation. All rights reserved.  

Microsoft、Active Directory、Hyper-V、Windows、および Windows Server は、米国 Microsoft Corporation の米国およびその他の国における登録商標または商標です。  

この製品には、グラフィックス フィルター ソフトウェアが含まれています。本ソフトウェアの一部は Independent JPEG Group で作成されたコードの一部を利用しています。  


1.0  
