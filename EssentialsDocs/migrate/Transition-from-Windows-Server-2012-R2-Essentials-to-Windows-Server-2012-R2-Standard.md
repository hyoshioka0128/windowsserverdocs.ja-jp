---
title: Windows Server Essentials から Windows Server 2012 R2 Standard への移行
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: a14689e3-2310-4229-bd3e-dafc0e739e02
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 3902fa53f59b99475f0ae117fd5ac193afeff8a3
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470237"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-r2-standard"></a>Windows Server Essentials から Windows Server 2012 R2 Standard への移行

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server 2016 は、現在のワークロードをサポートするクラウド対応のオペレーティングシステムであり、クラウドコンピューティングへの移行を容易にする新しいテクノロジを導入しています。 Windows Server 2016 のコンテンツは、準備のために役立ちます。

 Windows Server Essentials は、最大25人のユーザーと50台のデバイスをサポートしています。 ビジネスニーズが制限を超える場合は、Windows Server Essentials から Windows Server 2012 R2 Standard へのインプレースライセンス移行を実行して、ライセンスに準拠した状態を維持することができます。

 Windows Server 2012 R2 Standard に移行すると、ユーザーアカウントとデバイスの制限がなくなりますが、Windows Server Essentials に固有の機能 (ダッシュボード、リモート Web アクセス、クライアントコンピューターのバックアップなど) は引き続き利用できます。 ただし、これらの機能の技術的な制限により、サポートされる最大ユーザー数は 100 人、デバイス数は 200 台になります。 クライアント コンピューター バックアップ機能は、最大で 75 台のデバイスのバックアップをサポートします。

> [!IMPORTANT]
>   Windows Server 2012 R2 Standard では、環境内のユーザーまたはデバイスごとにクライアントアクセスライセンス (CAL) が必要です。 これは、CAL モデルを使用せず、Cal が付属していない Windows Server Essentials とは異なります。 Windows Server Essentials から Windows Server 2012 R2 Standard に移行する場合は、環境に応じて適切な数と種類の Cal を購入する必要があります (ほとんどのお客様はユーザー Cal を購入します)。

## <a name="before-the-transition"></a>移行前に

-   Windows Server Essentials から Windows Server 2012 R2 Standard に移行する前に、サーバーデータを完全にバックアップする必要があります。

    > [!IMPORTANT]
    >  サーバーの完全バックアップがない場合、サーバーを移行前の状態に復元することはできません。

-   また、Windows Server 2012 R2 Standard の使用許諾契約書 (EULA) を読んで理解していることを確認してください。 EULA を表示するには:

    1.  管理者としてコマンド ウィンドウを開きます。

    2.  次のコマンドを実行します。

         **dism /online /set-edition:ServerStandard /geteula:** *eula path* ( *eula path* は、EULA ファイルの保存先の場所を表します。例: C:\ws8std_eula.rtf)。 ファイル名拡張子として .rtf を使用してください。

    3.  ファイルを保存した場所を開き、そのファイルをダブルクリックして開きます。

## <a name="transition-to--windows-server-2012-r2-standard"></a>Windows Server 2012 R2 Standard への移行
 Windows Server Essentials から Windows Server 2012 R2 Standard への移行を決定したら、次の2つの手順を実行します。

1. Windows Server 2012 R2 Standard のライセンスと、環境に合わせて適切な数のユーザーまたはデバイスクライアントアクセスライセンスを購入します。

    Windows Server 2012 R2 Standard のライセンスは、小売店、ディストリビューター、または[Microsoft パートナー](https://pinpoint.microsoft.com/SelectCulture.aspx)の支援を通じて購入できます。

   > [!NOTE]
   >  Windows Server 2012 R2 Standard を最初に購入し、2つの仮想インスタンスのいずれかを Windows Server Essentials としてインストールするためにダウングレード権を行使した場合は、何も追加購入する必要はありません。
   >
   >  ボリュームライセンスチャネルを使用して Windows Server 2012 R2 Standard を購入した場合は、ボリュームライセンスサービスセンター (VLSC) から Windows Server 2012 R2 Standard の ISO イメージとプロダクトキーをダウンロードできます。
   >
   >  Windows Server 2012 R2 Standard を他のチャネルから購入した場合は、 [TechNet 評価センター](https://technet.microsoft.com/evalcenter/jj659306.aspx)から Windows server ESSENTIALS の ISO イメージと評価版のプロダクトキーをダウンロードできます。 次の手順に記載されている移行操作を実行すると、評価版の製品がフル ライセンス版のサポート対象製品に変換されます。

2. 管理者として Windows PowerShell を開き、次のコマンドを実行します。

    **dism/online/set-edition: ServerStandard/accepteula/productkey:** *Product Key* ( *Product key*は、Windows Server 2012 R2 Standard のコピーのプロダクトキーです)。

    サーバーが再起動すると、移行プロセスが完了します。

   移行後、Windows Server Essentials の機能はサーバーに残り、最大100ユーザーおよび200デバイスでサポートされています。

## <a name="additional-references"></a>その他のリファレンス


-   [サーバー データの Windows Server Essentials への移行](Migrate-Server-Data-to-Windows-Server-Essentials.md)

