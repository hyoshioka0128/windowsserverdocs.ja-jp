---
title: 生成とゲストでの HYPER-V 機能の互換性
description: キーの Hyper-v 機能と互換性のある生成とオペレーティングシステムの一覧を示します。
manager: dongill
ms.topic: article
ms.assetid: 81c1f32d-7814-4992-8a66-dd4b77c939b4
author: kbdazure
ms.author: kathydav
ms.date: 12/05/2016
ms.openlocfilehash: 1ea9e0d86e61f574af45b85701bae941bb9f6ad5
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960755"
---
# <a name="hyper-v-feature-compatibility-by-generation-and-guest"></a>生成とゲストでの HYPER-V 機能の互換性

>適用先:Windows Server 2016

この記事の表では、ジェネレーションといくつかのカテゴリごとにグループ化、HYPER-V の機能と互換性があるオペレーティング システムを説明します。 一般に、最も新しいオペレーティング システムを実行している第 2 世代仮想マシンの機能の最高レベルの可用性が得られます。

一部の機能は、ハードウェアやその他のインフラストラクチャに依存することに留意してください。 ハードウェアの詳細については、「 [Windows Server 2016 の hyper-v のシステム要件](System-requirements-for-Hyper-V-on-Windows.md)」を参照してください。 場合によっては、そのサポート対象のゲスト オペレーティング システム搭載の機能を使用できます。 詳細についてはオペレーティング システムがサポートされているを参照してください。

* [サポートされている Linux および FreeBSD の仮想マシン](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)
* [サポートされている Windows ゲスト オペレーティング システム](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)

## <a name="availability-and-backup"></a>可用性とバックアップ

機能  | Generation | ゲスト オペレーティング システム
------------- | ------------- | -----------
チェックポイント | 1 と 2 | 任意のサポートされているゲスト
ゲスト クラスタ リング | 1 と 2 | クラスター対応アプリケーションを実行し、iSCSI ターゲット ソフトウェアがインストールされているゲスト
レプリケーション | 1 と 2 | 任意のサポートされているゲスト
ドメイン コントローラー | 1 と 2 | 運用チェックポイントのみを使用する、サポートされているすべての Windows Server ゲスト。 「[サポートされている Windows Server ゲストオペレーティングシステム](https://docs.microsoft.com/windows-server/virtualization/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows#supported-windows-server-guest-operating-systems)」を参照してください。

## <a name="compute"></a>Compute

機能  | Generation | ゲスト オペレーティング システム
------------- | ------------- | -----------
動的メモリ | 1 と 2 | サポートされているゲストの特定のバージョン。 参照してください [HYPER-V 動的メモリの概要](https://technet.microsoft.com/library/hh831766.aspx) の Windows Server 2016 および Windows 10 より前のバージョン。
ホット追加/削除のメモリ | 1 と 2 | Windows Server 2016 の場合は Windows 10
仮想 NUMA | 1 と 2 | 任意のサポートされているゲスト

## <a name="development-and-test"></a>開発およびテスト
機能  | Generation | ゲスト オペレーティング システム
------------- | ------------- | -----------
COM/シリアル ポート | 1 と 2 <br>**注:** ジェネレーション 2 の場合は、Windows PowerShell を使用して構成します。 詳細については、「[カーネルデバッグ用の COM ポートの追加](./plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md#add-a-com-port-for-kernel-debugging)」を参照してください。 | 任意のサポートされているゲスト

## <a name="mobility"></a>可動性

機能  | Generation | ゲスト オペレーティング システム
------------- | ------------- | -----------
ライブ マイグレーション  | 1 と 2 |  任意のサポートされているゲスト
インポート/エクスポート | 1 と 2 |  任意のサポートされているゲスト

## <a name="networking"></a>ネットワーク

機能  | Generation | ゲスト オペレーティング システム
------------- | ------------- | -----------
ホット追加/削除の仮想ネットワーク アダプター | 2 | 任意のサポートされているゲスト
従来の仮想ネットワーク アダプター | 1 | 任意のサポートされているゲスト
単一ルート入出力仮想化 (SR-IOV) | 1 と 2 | 64 ビット Windows ゲストを Windows Server 2012 および Windows 8 で開始します。
バーチャル マシンの複数のキュー (VMMQ) | 1 と 2  | 任意のサポートされているゲスト

## <a name="remote-connection-experience"></a>リモート接続エクスペリエンス

機能  | Generation | ゲスト オペレーティング システム
------------- | ------------- | -----------
個別のデバイスの割り当て (DDA) | 1 と 2 | Windows Server 2016 では、Windows Server 2012 R2 Update 3133690 でのみのインストール、Windows 10 <br> **注:** 3133690 の更新プログラムの詳細については、「 [この](https://support.microsoft.com/kb/3133690) サポートの記事です。
拡張セッション モード | 1 と 2 | Windows Server 2016、Windows Server 2012 R2、Windows 10、Windows 8.1、リモートデスクトップサービス有効 <br>**注**: も、ホストを構成する必要があります。 詳細については、「 [VMConnect を使って HYPER-V 仮想マシンに使用するローカル リソース](./learn-more/Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)します。
RemoteFx | 1 と 2 | 32 ビットおよび 64 ビット バージョンの Windows で Windows 8 以降では 1 を生成します。 <br> 64 ビットの Windows 10 バージョンに第 2 世代

## <a name="security"></a>セキュリティ

機能  | Generation | ゲスト オペレーティング システム
------------- | ------------- | -----------
セキュア ブート | 2 | **Linux**: Ubuntu 14.04 およびそれ以降、SUSE Linux Enterprise Server 12 と以降では、Red Hat Enterprise Linux 7.0 およびその後、および CentOS 7.0 以降<br>**Windows**: サポートされているすべての第 2 世代仮想マシンで実行できるバージョン
シールドされた仮想マシン | 2 | **Windows**: サポートされているすべての第 2 世代仮想マシンで実行できるバージョン

## <a name="storage"></a>記憶域

機能  | Generation | ゲスト オペレーティング システム
------------- | ------------- | -----------
共有仮想ハード_ディスク (VHDX のみ) | 1 と 2  | Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
SMB3 | 1 と 2 | SMB3 をサポートするものすべて
記憶域スペース ダイレクト | 2 | Windows Server 2016
仮想ファイバー チャネル | 1 と 2 | Windows Server 2016、Windows Server 2012 R2、Windows Server 2012
VHDX 形式 | 1 と 2 | 任意のサポートされているゲスト







