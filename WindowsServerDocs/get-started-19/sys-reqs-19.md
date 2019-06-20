---
title: Windows Server 2019 システム要件
description: Windows Server 2019 のクリーン インストールでの記憶域、CPU、ネットワーク、メモリ、RAM の最小要件です。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a8b42d7-9fe5-4efe-9ea1-ace2131f860e
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: d97ec0efee86165f82bdf99a316d24d9c39ec958
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810718"
---
# <a name="system-requirements"></a>システム要件

>適用先:Windows Server 2019 

このトピックの「Windows Server を実行する最小システム要件の概要&reg;2019 します。

## <a name="review-system-requirements"></a>システム要件を確認する。  

Windows Server 2019 のシステム要件を次に示します。 使用しているコンピューターが "最小" 要件を満たしていない場合は、この製品を正しくインストールすることはできません。 実際の要件は、システム構成やインストールするアプリケーションおよび機能によって異なります。

特に指定がない限り、これらの最小システム要件はすべてのインストール オプション (Server Core、デスクトップ エクスペリエンス搭載サーバー、および Nano Server) および Standard Edition と Datacenter Edition の両方に適用されます。  

> [!IMPORTANT]  
> 予定している展開の範囲が多岐にわたる場合、通常適用可能な "推奨" システム要件が現実的ではなくなります。 特定のサーバーの役割に必要なリソースの詳細については、展開する予定の各サーバーの役割のドキュメントで確認してください。 良い結果を得るために、展開のテストを実施して特定の展開シナリオに合ったシステム要件を決定してください。  

## <a name="processor"></a>処理者  

プロセッサのパフォーマンスは、プロセッサのクロック周波数だけでなく、プロセッサ コアの数やプロセッサ キャッシュのサイズの影響も受けます。 この製品のプロセッサの要件を次に示します。  

**最小**:  
- 1.4 GHz 64 ビット プロセッサ  
- x64 命令セット対応  
- NX と DEP のサポート  
- CMPXCHG16b、LAHF/SAHF、および PrefetchW のサポート  
- 第 2 レベルのアドレス変換 (EPT または NPT) のサポート  

[Coreinfo](https://technet.microsoft.com/sysinternals/cc835722.aspx)は、CPU がこれらの機能の確認に使用できるツールです。

## <a name="ram"></a>RAM  
この製品で推定される RAM の要件を次に示します。  

**最小**:  
- 512 MB (デスクトップ エクスペリエンス搭載サーバー インストール オプションを使用したサーバーの場合、2 GB)
- ECC (エラーを修正するコード) 型または物理ホストの展開用の同様のテクノロジ

> [!IMPORTANT]  
> サポートされる最小のハードウェア パラメーター (1 プロセッサ コアと 512 MB RAM) で仮想マシンを作成し、このリリースを仮想マシンにインストールしようとすると、セットアップが失敗します。  
>   
> この問題を回避するには、次のいずれかの操作を行います。  
>   
> -   このリリースをインストールする仮想マシンに 800 MB を超える RAM を割り当てます。 セットアップが完了したら、実際のサーバーの構成に応じて、割り当てを最小の 512 MB RAM に変更できます。  
> -   Shift + F10 キーを押して仮想マシン上のこのリリースのブート プロセスを中断します。 開いたコマンド プロンプトで、Diskpart.exe を使用してインストール パーティションを作成してフォーマットします。 **Wpeutil createpagefile /path=C:\pf.sys** を実行します (作成したインストール パーティションを C: とする)。 コマンド プロンプトを閉じ、セットアップを続行します。  

## <a name="storage-controller-and-disk-space-requirements"></a>記憶域コントローラーとディスク領域の要件  
Windows Server 2019 を実行しているコンピューターでは、PCI Express アーキテクチャの仕様に準拠している記憶域アダプターを含める必要があります。 ハード ディスク ドライブとして分類されるサーバー上の永続的な記憶装置は、PATA であってはなりません。 Windows Server 2019 ブート、ページ、またはデータ ドライブに ATA、PATA、IDE/EIDE ができませんでした。  

システム **パ** ーティションで必要と予想される、最小のディスク領域の要件は次のとおりです  。  

**最小**:32 GB  

> [!NOTE]
> 32 GB は、正常にインストールするための*最小*値であることに注意してください。 この最小値を使用して、Web サービス (IIS) サーバーの役割の Server Core モードで Windows Server 2019 をインストールする必要がありますできます。 Server Core モードのサーバーは、フル インストール モードの同じサーバーより約 4 GB 小さくなります。 
> 
> 次のいずれかの状況に対して、追加のディスク領域がシステム パーティションに必要になります。  
> 
> -   ネットワークを介してシステムをインストールする場合。  
> -   16 GB を超える RAM を搭載したコンピューターでは、ページング ファイル、休止状態ファイル、およびダンプ ファイル用にさらにディスク領域が必要になります。  

## <a name="network-adapter-requirements"></a>ネットワーク アダプターの要件  

このリリースで使用するネットワーク アダプターは、次の機能を搭載している必要があります。  

**最小**:  
- ギガビット以上の処理能力があるイーサネット アダプター  
- PCI Express アーキテクチャの仕様への準拠  

ネットワーク デバッグ (KDNet) をサポートするネットワーク アダプターは有用ですが、最小要件ではありません。   

サポートするブート前実行環境 (PXE) が便利な場合は、ネットワーク アダプターが最小要件ではありません。

## <a name="other-requirements"></a>その他の要件  
このリリースを実行するコンピューターには、次のものも必要です。  

-   DVD ドライブ (DVD メディアからオペレーティング システムをインストールする場合)  

次のアイテムは厳密には必須ではありませんが、特定の機能では必要です。  

- セキュア ブートをサポートしている UEFI 2.3.1c ベースのシステムとファームウェア  
- トラステッド プラットフォーム モジュール  

-   Super VGA (1024 x 768) またはそれ以上の解像度に対応しているグラフィックス デバイスおよびモニター  

-   キーボードおよび Microsoft&reg; マウス (または互換性のある他のポインティング デバイス)  

-   インターネット アクセス (費用が発生することもあります)  

> [!NOTE]  
> トラステッド プラットフォーム モジュール (TPM) チップは、このリリースをインストールには厳密に必要というわけではありませんが、BitLocker ドライブ暗号化などの特定の機能を使用するためには必要です。 お使いのコンピューターが TPM を使用している場合は、次の要件を満たす必要があります。  
>  
> - ハードウェアベースの TPM では、TPM 仕様のバージョン 2.0 を実装する必要があります。  
> - バージョン 2.0 を実装する TPM では、EK 証明書がハードウェア ベンダーによって事前に TPM にプロビジョニングされているか、最初の起動時にデバイスでこの証明書を取得可能である必要があります。  
> - バージョン 2.0 を実装する TPM は、SHA-256 PCR バンクを搭載し、SHA-256 の PCR 0 - 23 を実装している必要があります。 TPM に、SHA-1 と SHA-256 の両方に使用できる切り替え可能な単一の PCR バンクを搭載することもできます。  
> - TPM をオフにする UEFI オプションは必須ではありません。  