---
title: システム要件
description: 各インストール オプションのクリーン インストールでの記憶域、CPU、ネットワーク、メモリ、RAM の最小要件について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 10/17/2017
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a8b42d7-9fe5-4efe-9ea1-ace2131fe068
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 29183c62830cbe9e26cce4e0ce4543b554f0ed65
ms.sourcegitcommit: 3883eebbba70bfea0221e510863ee1a724a5f926
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2018
ms.locfileid: "5783744"
---
# システム要件

>適用対象: Windows Server (半期チャネル)、Windows Server 2016 

このトピックでは、Windows Server&reg; 2016 または Windows Server バージョン 1709 を実行するための最小システム要件について説明します。


> [!Note]  
> このリリースでは、クリーン インストールをお勧めします。  
>   

> [!NOTE]  
> インストール時に、Server Core オプションを指定してインストールを行った場合、GUI コンポーネントがインストールされないこと、およびこれらのコンポーネントをサーバー マネージャーを使用してインストールまたはアンインストールできないことに注意してください。 GUI 機能が必要な場合は、Windows Server 2016 をインストールするときに、"デスクトップ エクスペリエンス搭載サーバー" オプションを選択してください。 詳細については、「[Install Nano Server](Getting-Started-with-Nano-Server.md)」 (Nano Server のインストール) を参照してください。  


## システム要件を確認する。  
Windows Server 2016 のシステム要件の概要は次のとおりです。 使用しているコンピューターが "最小" 要件を満たしていない場合は、この製品を正しくインストールすることはできません。 実際の要件は、システム構成やインストールするアプリケーションおよび機能によって異なります。

特に指定がない限り、これらの最小システム要件はすべてのインストール オプション (Server Core、デスクトップ エクスペリエンス搭載サーバー、および Nano Server) および Standard Edition と Datacenter Edition の両方に適用されます。  

> [!IMPORTANT]  
> 予定している展開の範囲が多岐にわたる場合、通常適用可能な "推奨" システム要件が現実的ではなくなります。 特定のサーバーの役割に必要なリソースの詳細については、展開する予定の各サーバーの役割のドキュメントで確認してください。 良い結果を得るために、展開のテストを実施して特定の展開シナリオに合ったシステム要件を決定してください。  


## プロセッサ  
プロセッサのパフォーマンスは、プロセッサのクロック周波数だけでなく、プロセッサ コアの数やプロセッサ キャッシュのサイズの影響も受けます。 この製品のプロセッサの要件を次に示します。  

**最小**:   
- 1.4 GHz 64 ビット プロセッサ  
- x64 命令セット対応  
- NX と DEP のサポート  
- CMPXCHG16b、LAHF/SAHF、および PrefetchW のサポート  
- 第 2 レベルのアドレス変換 (EPT または NPT) のサポート  

[Coreinfo](https://technet.microsoft.com/sysinternals/cc835722.aspx)は、ツールを使いの CPU がこれらの機能の確認を使用することができます。

## RAM  
この製品で推定される RAM の要件を次に示します。  

**最小**:   
- 512 MB (デスクトップ エクスペリエンス搭載サーバー インストール オプションを使用したサーバーの場合、2 GB)
- ECC (誤り訂正符号) 型または同様のテクノロジ  

> [!IMPORTANT]  
> サポートされる最小のハードウェア パラメーター (1 プロセッサ コアと 512 MB RAM) で仮想マシンを作成し、このリリースを仮想マシンにインストールしようとすると、セットアップが失敗します。  
>   
> この問題を回避するには、次のいずれかの操作を行います。  
>   
> -   このリリースをインストールする仮想マシンに 800 MB を超える RAM を割り当てます。 セットアップが完了したら、実際のサーバーの構成に応じて、割り当てを最小の 512 MB RAM に変更できます。  
> -   Shift + F10 キーを押して仮想マシン上のこのリリースのブート プロセスを中断します。 開いたコマンド プロンプトで、Diskpart.exe を使用してインストール パーティションを作成してフォーマットします。 **Wpeutil createpagefile /path=C:\pf.sys** を実行します (作成したインストール パーティションを C: とする)。 コマンド プロンプトを閉じ、セットアップを続行します。  

## 記憶域コントローラーとディスク領域の要件  
Windows Server 2016 を実行するコンピューターでは、PCI Express アーキテクチャの仕様に準拠している記憶域アダプターを搭載する必要があります。 ハード ディスク ドライブとして分類されるサーバー上の永続的な記憶装置は、PATA であってはなりません。 Windows Server 2016 では、ブート ドライブ、ページ ドライブ、またはデータ ドライブに ATA、PATA、IDE、EIDE は使用できません。  

システム パーティションで必要と予想される、**最小**のディスク領域の要件は次のとおりです。  

**最小**:32 GB  

   > [!NOTE]  
    > 32 GB は、正常にインストールするための*最小*値であることに注意してください。 この最小値では、Server Core モードで Windows Server 2016 をインストールして Web サービス (IIS) のサーバーの役割を構成できます。 Server Core モードのサーバーは、フル インストール モードの同じサーバーより約 4 GB 小さくなります。 
    >   
    > 次のいずれかの状況に対して、追加のディスク領域がシステム パーティションに必要になります。  
    >   
    > -   ネットワークを介してシステムをインストールする場合。  
    > -   16 GB を超える RAM を搭載したコンピューターでは、ページング ファイル、休止状態ファイル、およびダンプ ファイル用にさらにディスク領域が必要になります。  

## ネットワーク アダプターの要件  

このリリースで使用するネットワーク アダプターは、次の機能を搭載している必要があります。  

**最小**:   
- ギガビット以上の処理能力があるイーサネット アダプター  
- PCI Express アーキテクチャの仕様への準拠  
- Preboot Execution Environment (PXE) のサポート  

ネットワーク デバッグ (KDNet) をサポートするネットワーク アダプターは有用ですが、最小要件ではありません。   



## その他の要件  
このリリースを実行するコンピューターには、次のものも必要です。  


-   DVD ドライブ (DVD メディアからオペレーティング システムをインストールする場合)  

次のアイテムは厳密には必須ではありませんが、特定の機能では必要です。  

- セキュア ブートをサポートしている UEFI 2.3.1c ベースのシステムとファームウェア  
- トラステッド プラットフォーム モジュール  

-   Super VGA (1024 x 768) またはそれ以上の解像度に対応しているグラフィックス デバイスおよびモニター  

-   キーボードおよび Microsoft&reg; マウス (または互換性のある他のポインティング デバイス)  

-   インターネット アクセス (費用が発生することもあります)  

>[!NOTE]  
> トラステッド プラットフォーム モジュール (TPM) チップは、このリリースをインストールには厳密に必要というわけではありませんが、BitLocker ドライブ暗号化などの特定の機能を使用するためには必要です。 お使いのコンピューターが TPM を使用している場合は、次の要件を満たす必要があります。  
>  
>- ハードウェアベースの TPM では、TPM 仕様のバージョン 2.0 を実装する必要があります。  
>- バージョン 2.0 を実装する TPM では、EK 証明書がハードウェア ベンダーによって事前に TPM にプロビジョニングされているか、最初の起動時にデバイスでこの証明書を取得可能である必要があります。  
>- バージョン 2.0 を実装する TPM は、SHA-256 PCR バンクを搭載し、SHA-256 の PCR 0 - 23 を実装している必要があります。 TPM に、SHA-1 と SHA-256 の両方に使用できる切り替え可能な単一の PCR バンクを搭載することもできます。  
>- TPM をオフにする UEFI オプションは必須ではありません。  

## Nano Server のインストール  
Windows Server 2016 を Nano Server としてインストールする詳細な手順については、「[Nano Server のインストール](Getting-Started-with-Nano-Server.md)」を参照してください。

## その他のリソース
- [Windows のプロセッサの要件](https://docs.microsoft.com/windows-hardware/design/minimum/windows-processor-requirements)
- [Windows Server 2016 の Standard エディションと Datacenter エディションの比較](https://docs.microsoft.com/windows-server/get-started/2016-edition-comparison)
- [Windows 10 のシステム要件 ](https://www.microsoft.com/windows/windows-10-specifications#system-specifications)
- [Windows Server 2016 ライセンス データシートのダウンロード](http://download.microsoft.com/download/7/2/9/7290EA05-DC56-4BED-9400-138C5701F174/WS2016LicensingDatasheet.pdf)
