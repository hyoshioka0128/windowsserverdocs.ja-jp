---
title: Web サーバーのパフォーマンス チューニング
description: Windows Server 16 上の Web サーバーに対するパフォーマンス チューニングの推奨事項
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: davso; ericam; yashi
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: ec36d87957e5bbe897597e330e766c3193cd30d0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851695"
---
# <a name="performance-tuning-web-servers"></a>Web サーバーのパフォーマンス チューニング


このトピックでは、Windows Server 2016 Web サーバーに対するパフォーマンス チューニングの方法と推奨事項について説明します。


## <a name="selecting-the-proper-hardware-for-performance"></a>パフォーマンスのための適切なハードウェアの選択


平均負荷、ピーク時の負荷、容量、拡張の計画、応答時間を考慮して、予想される Web 負荷に対応できる適切なハードウェアを選択することが重要です。 ハードウェアにボトルネックがあると、ソフトウェア チューニングの効果が限定されます。

[サーバー ハードウェアのパフォーマンス チューニング](../../hardware/index.md)に関する記事に、以下のパフォーマンス制約を回避するためのハードウェアに関する推奨事項が記載されています。

-   低速の CPU では、ASP、ASP.NET、TLS シナリオなど、CPU 負荷の高いワークロードの処理能力が制限されます。

-   小さな L2 または L3/LLC プロセッサ キャッシュは、パフォーマンスに悪影響を及ぼす可能性があります。

-   量が限られているメモリは、ホスティングできるサイトの数、格納できる動的コンテンツ スクリプト (ASP.NET など) の数、アプリケーション プールやワーカー プロセスの数に影響します。

-   非効率的なネットワーク アダプターが原因で、ネットワークがボトルネックになります。

-   非効率的なディスク サブシステムまたは記憶域アダプターが原因で、ファイル システムがボトルネックになります。

## <a name="operating-system-best-practices"></a>オペレーティング システムのベスト プラクティス


可能な場合は、オペレーティング システムのクリーン インストールから開始します。 ソフトウェアをアップグレードすると、古い、不要な、または最適ではないレジストリ設定と、自動的に起動される場合にリソースを消費する、以前にインストールしたサービスとアプリケーションが残る可能性があります。 別のオペレーティング システムがインストールされていて、それを保持しておく必要がある場合は、新しいオペレーティング システムを別のパーティションにインストールする必要があります。 そうしないと、%Program Files%\\Common Files にある設定が新しいインストールによって上書きされます。

ディスク アクセスの干渉を減らすために、可能であれば、システム ページ ファイル、オペレーティング システム、Web データ、ASP テンプレート キャッシュ、インターネット インフォメーション サービス (IIS) ログを個別の物理ディスクに置きます。

システム リソースの競合を軽減するために、可能であれば Microsoft SQL Server と IIS を異なるサーバーにインストールします。

重要ではないサービスとアプリケーションのインストールは避けます。 場合によっては、システム上の不要なサービスを無効にする価値があります。

## <a name="ntfs-file-system-settings"></a>NTFS ファイル システムの設定

システム グローバル スイッチ **NtfsDisableLastAccessUpdate** (REG\_DWORD) 1 は **HKLM\\System\\CurrentControlSet\\Control\\FileSystem** の下にあり、既定では 1 に設定されます。 このスイッチでは、最後のファイルまたはディレクトリ アクセスに関する日付と時刻のスタンプの更新を無効にすることで、ディスク I/O の負荷と待ち時間を低減します。 Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008 のクリーン インストールでは、この設定が既定で有効になるので、調整する必要はありません。 以前のバージョンの Windows では、このキーは設定されませんでした。 サーバーで以前のバージョンの Windows が実行されているか、サーバーが Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 または Windows Server 2008 にアップグレードされた場合は、この設定を有効にする必要があります。

更新の無効化は、何千もディレクトリを含む大規模なデータ セット (または多くのホスト) を使用している場合に効果的です。 Web 管理の目的でのみこの情報を保持している場合は、IIS ログを代わりに使用することをお勧めします。

>[!Warning]
> 増分バックアップ ユーティリティなどの一部のアプリケーションは、この更新情報に依存しており、この情報がないと正しく機能しません。

## <a name="see-also"></a>関連項目
- [IIS 10.0 のパフォーマンス チューニング](tuning-iis-10.md)
- [HTTP 1.1/2 のチューニング](http-performance.md)


