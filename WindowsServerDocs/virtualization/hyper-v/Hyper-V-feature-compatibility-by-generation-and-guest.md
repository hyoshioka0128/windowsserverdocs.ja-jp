---
title: 生成とゲストでの HYPER-V 機能の互換性
description: ジェネレーションと主な HYPER-V 機能と互換性のあるオペレーティング システムを一覧表示します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81c1f32d-7814-4992-8a66-dd4b77c939b4
author: KBDAzure
ms.author: kathydav
ms.date: 12/05/2016
ms.openlocfilehash: 5950a75da4569979794a5848bd41ab349dc34676
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812656"
---
# <a name="hyper-v-feature-compatibility-by-generation-and-guest"></a>生成とゲストでの HYPER-V 機能の互換性

>適用先:Windows Server 2016
  
この記事の表では、ジェネレーションといくつかのカテゴリごとにグループ化、HYPER-V の機能と互換性があるオペレーティング システムを説明します。 一般に、最も新しいオペレーティング システムを実行している第 2 世代バーチャル マシンの機能の最高レベルの可用性が得られます。  
  
一部の機能は、ハードウェアやその他のインフラストラクチャに依存することに留意してください。 ハードウェアの詳細については、次を参照してください。 [Windows Server 2016 で Hyper-v のシステム要件](System-requirements-for-Hyper-V-on-Windows.md)します。 場合によっては、そのサポート対象のゲスト オペレーティング システム搭載の機能を使用できます。 詳細についてはオペレーティング システムがサポートされているを参照してください。  
  
* [サポートされている Linux および FreeBSD の仮想マシン](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  
* [サポートされている Windows ゲスト オペレーティング システム](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)  
  
## <a name="availability-and-backup"></a>可用性とバックアップ  
  
機能  | 生成 | ゲスト オペレーティング システム  
------------- | ------------- | -----------  
チェックポイント | 1 と 2 | 任意のサポートされているゲスト  
ゲスト クラスタ リング | 1 と 2 | クラスター対応アプリケーションを実行し、iSCSI ターゲット ソフトウェアがインストールされているゲスト  
レプリケーション | 1 と 2 | 任意のサポートされているゲスト  
ドメイン コントローラー | 1 と 2 | いずれかには、実稼働のチェックポイントのみを使用して Windows Server のゲストがサポートされています。 参照してください[Windows Server のサポートされているゲスト オペレーティング システム](https://docs.microsoft.com/windows-server/virtualization/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows#supported-windows-server-guest-operating-systems)   
  
## <a name="compute"></a>計算  
  
機能  | 生成 | ゲスト オペレーティング システム  
------------- | ------------- | -----------  
動的メモリ | 1 と 2 | サポートされているゲストの特定のバージョン。 参照してください [HYPER-V 動的メモリの概要](https://technet.microsoft.com/library/hh831766.aspx) の Windows Server 2016 および Windows 10 より前のバージョン。  
ホット追加/削除のメモリ | 1 と 2 | Windows Server 2016 の場合は Windows 10  
仮想 NUMA | 1 と 2 | 任意のサポートされているゲスト  
  
## <a name="development-and-test"></a>開発およびテスト  
機能  | 生成 | ゲスト オペレーティング システム  
------------- | ------------- | -----------  
COM/シリアル ポート | 1 と 2 <br>**注:** ジェネレーション 2 の場合は、Windows PowerShell を使用して、構成します。 詳細については、次を参照してください。[カーネル デバッグ用に COM ポートを追加](./plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md#add-a-com-port-for-kernel-debugging)します。 | 任意のサポートされているゲスト  
  
## <a name="mobility"></a>モビリティ  
  
機能  | 生成 | ゲスト オペレーティング システム  
------------- | ------------- | -----------  
ライブ マイグレーション  | 1 と 2 |  任意のサポートされているゲスト  
インポート/エクスポート | 1 と 2 |  任意のサポートされているゲスト  
  
## <a name="networking"></a>ネットワーク  
  
機能  | 生成 | ゲスト オペレーティング システム  
------------- | ------------- | -----------  
ホット追加/削除の仮想ネットワーク アダプター | 2 | 任意のサポートされているゲスト  
従来の仮想ネットワーク アダプター | 1 | 任意のサポートされているゲスト  
単一ルート入出力仮想化 (SR-IOV) | 1 と 2 | 64 ビット Windows ゲストを Windows Server 2012 および Windows 8 で開始します。  
バーチャル マシンの複数のキュー (VMMQ) | 1 と 2  | 任意のサポートされているゲスト  
  
## <a name="remote-connection-experience"></a>リモート接続エクスペリエンス  
  
機能  | 生成 | ゲスト オペレーティング システム  
------------- | ------------- | -----------  
個別のデバイスの割り当て (DDA) | 1 と 2 | Windows Server 2016 では、Windows Server 2012 R2 Update 3133690 でのみのインストール、Windows 10 <br> **注:** Update 3133690 の詳細については、「[この](https://support.microsoft.com/kb/3133690)サポートの記事。  
拡張セッション モード | 1 と 2 | Windows Server 2016、Windows Server 2012 R2、Windows 10 および Windows 8.1、リモート デスクトップ サービスを有効になっています。 <br>**注意**:また、ホストを構成する必要があります。 詳細については、「 [VMConnect を使って HYPER-V バーチャル マシンに使用するローカル リソース](./learn-more/Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)します。  
RemoteFx | 1 と 2 | 32 ビットおよび 64 ビット バージョンの Windows で Windows 8 以降では 1 を生成します。 <br> 64 ビットの Windows 10 バージョンに第 2 世代  
  
## <a name="security"></a>セキュリティ  
  
機能  | 生成 | ゲスト オペレーティング システム  
------------- | ------------- | -----------  
セキュア ブート | 2 | **Linux**:Ubuntu 14.04 およびそれ以降、SUSE Linux Enterprise Server 12 と以降では、Red Hat Enterprise Linux 7.0 および以降、および CentOS 7.0 以降<br>**Windows**:第 2 世代仮想マシンで実行できるサポートされているすべてのバージョン  
シールドされた仮想マシン | 2 | **Windows**:第 2 世代仮想マシンで実行できるサポートされているすべてのバージョン  
  
## <a name="storage"></a>ストレージ  
  
機能  | 生成 | ゲスト オペレーティング システム  
------------- | ------------- | -----------  
共有仮想ハード_ディスク (VHDX のみ) | 1 と 2  | Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012  
SMB3 | 1 と 2 | SMB3 をサポートするものすべて  
記憶域スペース ダイレクト | 2 | Windows Server 2016  
仮想ファイバー チャネル | 1 と 2 | Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012  
VHDX 形式 | 1 と 2 | 任意のサポートされているゲスト   
  
  
  
  
    


