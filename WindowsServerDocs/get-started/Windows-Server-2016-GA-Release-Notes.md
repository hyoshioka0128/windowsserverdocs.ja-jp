---
title: リリース ノート - Windows Server 2016 に関する重要な問題
description: クラッシュ、ハング、インストールの失敗、データの損失を回避するための回避策を必要とする重大な問題についてまとめます。クラッシュ、ハング、インストールの失敗、データの損失を回避するための回避策を必要とする重大な問題についてまとめます。
ms.prod: windows-server
ms.date: 11/13/2018
ms.technology: server-general
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
ms.openlocfilehash: 8ceff837c2b85466f5583eed03f39e73f32fd4a4
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826385"
---
# <a name="release-notes-important-issues-in-windows-server-2016"></a>リリース ノート:Windows Server 2016 に関する重要な問題

>適用先:Windows Server 2016

これらのリリース ノートでは、Windows Server 2016 オペレーティング システムの最も重大な問題とその回避策 (存在する場合) についてまとめています。 このリリースにおける計画的な変更点、新機能、および修正プログラムについては、「[Windows Server 2016 の新機能](whats-new-in-windows-server-2016.md)」と特定の機能チームからのお知らせを参照してください。 特に指定がない限り、レポートされる問題はそれぞれ、Windows Server 2016 のすべてのエディションおよびインストール オプションに適用されます。

このドキュメントは継続的に更新されています。 解決策が必要な重大な問題が発見された場合、および新しい解決策および修正が使用可能になった場合は、ここに追加されます。

## <a name="express-updates-available-starting-in-november-2018-new"></a>2018 年 11 月 から利用できる高速更新プログラム (新規)

2018 年 11 月の Update Tuesday 更新プログラムから、Windows では Windows Server 2016 用の[高速更新プログラム](express-updates.md)が再発行されます。 WSUS と Configuration Manager を使用している場合、Windows Server 2016 更新用の 2 つのパッケージ (完全更新プログラムと高速更新プログラム) が再表示されます。 お使いのサーバー環境で高速更新プログラムを使用する場合、高速更新プログラムを正しくインストールするには、2017 年 11 月以降の完全更新プログラム (KB# 4048953) を使用してサーバーが更新されていることを確認する必要があります。 2017 11B 更新プログラム (KB 4048953) 以降更新されていないサーバーで高速更新プログラムを試行した場合、無限ループに入って帯域幅や CPU リソースを消費する繰り返しエラーが発生します。 このシナリオが発生した場合は、高速更新プログラムのプッシュを停止し、最新の完全更新プログラムをプッシュして、エラー ループを停止します。

## <a name="server-core-installation-option"></a>Server Core インストール オプション

[comment]: # (ID:370; 提出者: Amason; 状態: サインオフ)

Server Core インストール オプションを使用して Windows Server 2016 をインストールすると、プリント サーバーの役割がインストールされていなくても、印刷スプーラーがインストールされ、既定で開始されます。

これを回避するには、初回起動後に、印刷スプーラーを無効に設定します。

## <a name="containers"></a>コンテナー

[comment]: # (ID:371; 提出者: taylorb; 状態:サインオフ)
- コンテナーを使用する前に、[Windows 10 Version 1607 用のサービス スタック更新プログラム: 2016 年 8 月 23 日](https://support.microsoft.com/kb/3176936) またはそれ以降に利用可能になった更新プログラムをインストールしてください。 インストールしないと、コンテナーの作成、開始、または実行に失敗するほか、"Win32 で CreateProcess が失敗しました: RPC サーバーが利用できません。

[comment]: # (ID:373; 提出者: plang; 状態: サインオフ)
- NanoServerPackage OneGet プロバイダーは、Windows コンテナーでは動作しません。 これを回避するには、(コンテナー以外の) 別のコンピューターで Find-NanoServerPackage および Save-NanoServerPackage を使用して、必要なパッケージをダウンロードします。 その後、ダウンロードしたパッケージをコンテナーにコピーしてインストールします。

## <a name="device-guard"></a>Device Guard

[comment]: # (ID:369; 提出者: nirb; 状態: サインオフ)
仮想化ベースでのコード整合性の保護や (仮想化ベースでのコード整合性の保護を使用する) シールドされた仮想マシンを利用する場合、これらのテクノロジは一部のデバイスやアプリケーションとの互換性がない可能性があることに注意してください。 運用システム上で機能を有効にする前に、ラボでこのような構成をテストする必要があります。 これを行わない場合は、予期しないデータの損失や Stop エラーが発生する可能性があります。

## <a name="microsoft-exchange"></a>Microsoft Exchange

[comment]: # (ID:375; 提出者: wgries; 状態: サインオフ)
Windows Server 2016 上で Microsoft Exchange 2016 CU3 を実行しようとすると、IIS ホスト プロセス W3WP.exe でエラーが発生します。 現時点では、回避策はありません。 サポートされる修正プログラムが利用可能になるまでは、Windows Server 2016 での Exchange 2016 CU3 の展開を延期する必要があります。

## <a name="remote-server-administration-tools-rsat"></a>リモート サーバー管理ツール (RSAT)

[comment]: # (ID:374; 提出者: ryanpu; 状態: サインオフ)
Anniversary Update より前のバージョンの Windows 10 を実行していて、Hyper-V と、仮想トラステッド プラットフォーム モジュールが有効になった仮想マシン (シールドされた仮想マシンを含む) を使用している場合、Windows Server 2016 用の RSAT バージョンをインストールすると、これらの仮想マシンの起動に失敗します。

これを回避するには、RSAT をインストールする前に、クライアント コンピューターを Windows 10 Anniversary Update (以降) にアップグレードします。 この問題既に発生している場合は、RSAT をアンインストールし、クライアントを Windows 10 Anniversary Update にアップグレードした後、RSAT を再インストールします。

## <a name="shielded-virtual-machines"></a>シールドされた仮想マシン

[comment]: # (ID:369; 提出者: nirb; 状態: サインオフ)  
- シールドされた仮想マシンを運用環境で展開する前に、利用可能なすべての更新プログラムがインストールされていることを確認します。

- 仮想化ベースでのコード整合性の保護や (仮想化ベースでのコード整合性の保護を使用する) シールドされた仮想マシンを利用する場合、これらのテクノロジは一部のデバイスやアプリケーションとの互換性がない可能性があることに注意してください。 運用システム上で機能を有効にする前に、ラボでこのような構成をテストする必要があります。 これを行わない場合は、予期しないデータの損失や Stop エラーが発生する可能性があります。

## <a name="start-menu"></a>スタート メニュー

[comment]: # (ID:372; 提出者: samli; 状態: サインオフ)
この問題は、デスクトップ エクスペリエンス搭載サーバー オプションを使用してインストールされた Windows Server 2016 に影響します。

**スタート** メニューのフォルダー内にショートカット項目を追加するアプリケーションをインストールした場合、そのショートカットを動作させるには、一度ログアウトしてから、もう一度ログインする必要があります。

メインの [Windows Server 2016](Windows-Server-2016.md) ハブに戻ります。

## <a name="storport-performance"></a>Storport のパフォーマンス

Windows Server 2016 を新たにインストールして実行した場合、Windows Server 2012 R2 と比較して、一部のシステムではストレージのパフォーマンスが低下することがあります。  Windows Server 2016 の開発では、プラットフォームのセキュリティと信頼性を強化するために、複数の変更が行われました。 それらの中には、Windows Defender を既定で有効にするなど、I/O パスの延伸につながる変更が含まれているため、特定のワークロードとパターンで I/O パフォーマンスが低下する可能性があります。 Windows Defender はシステム保護のための重要な層であるため、Microsoft では無効にすることをお勧めしていません。  

## <a name="copyright"></a>著作権

このドキュメントは、現状のままで提供されています。 このドキュメントに記載されている情報および見解 (URL 等のインターネット Web サイトに関する情報を含む) は、将来予告なしに変更されることがあります。  

このドキュメントは、マイクロソフト製品に含まれる知的財産に対していかなる法的権利も付与しません。 お客様は、内部的な参照目的に限り、このドキュメントを複製して使用することができます。  

&copy; 2016 Microsoft Corporation. All rights reserved.  

Microsoft、Active Directory、Hyper-V、Windows、および Windows Server は、米国 Microsoft Corporation の米国およびその他の国における登録商標または商標です。  

この製品には、グラフィックス フィルター ソフトウェアが含まれています。本ソフトウェアの一部は Independent JPEG Group で作成されたコードの一部を利用しています。  

1.0
