---
title: Windows Server Essentials から Windows Server 2012 R2 Standard への移行
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a14689e3-2310-4229-bd3e-dafc0e739e02
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ca36533af169c899865789f153960bf5f0dda684
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432553"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-r2-standard"></a>Windows Server Essentials から Windows Server 2012 R2 Standard への移行

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server 2016 とは、クラウド コンピューティングへの移行をしやすく新しいテクノロジを導入して、現在のワークロードをサポートするクラウド対応のオペレーティング システムです。 Windows Server 2016 のコンテンツは、準備に役立ちます。

 Windows Server Essentials では、25 ユーザーおよび 50 デバイスまでサポートしています。 ビジネスでは、制限を超える必要がある、ときに、Windows Server 2012 R2 Standard ライセンスに準拠したままにする Windows Server Essentials から、ライセンスのインプレース移行を実行できます。  
  
 Windows Server 2012 R2 Standard への移行後、ユーザーのアカウントとデバイスの制限が削除されますが、(ダッシュ ボード、リモート Web アクセス、クライアント コンピューターのバックアップなど) の Windows Server Essentials に固有の機能は、引き続き利用できます。 ただし、これらの機能の技術的な制限により、サポートされる最大ユーザー数は 100 人、デバイス数は 200 台になります。 クライアント コンピューター バックアップ機能は、最大で 75 台のデバイスのバックアップをサポートします。  
  
> [!IMPORTANT]
>   Windows Server 2012 R2 Standard ユーザーまたは環境内でデバイスごとのクライアント アクセス ライセンス (CAL) が必要です。 これは、CAL モデルを使用しないと、Cal が付属していませんが、Windows Server Essentials と異なります。 Windows Server Essentials から Windows Server 2012 R2 Standard への移行、ときに、適切な数と種類の Cal、環境 (ほとんどのお客様は user Cal を購入) を購入する必要があります。  
  
## <a name="before-the-transition"></a>移行前に  
  
-   Windows Server 2012 R2 Standard への Windows Server Essentials から移行する前に、サーバーのデータをバックアップする必要があります。  
  
    > [!IMPORTANT]
    >  サーバーの完全バックアップがない場合、サーバーを移行前の状態に復元することはできません。  
  
-   さらに、読み取り、Windows Server 2012 R2 Standard のエンド ユーザー ライセンス契約 (EULA) を理解することを確認します。 EULA を表示するには:  
  
    1.  管理者としてコマンド ウィンドウを開きます。  
  
    2.  次のコマンドを実行します。  
  
         **dism/online -エディション: ServerStandard/geteula:** *eula のパス*(場所*eula のパス*は、EULA ファイルを保存する場所を表す例。C:\ws8std_eula.rtf)。 ファイル名拡張子として .rtf を使用してください。  
  
    3.  ファイルを保存した場所を開き、そのファイルをダブルクリックして開きます。  
  
## <a name="transition-to--windows-server-2012-r2-standard"></a>Windows Server 2012 R2 Standard への移行  
 移行します。 Windows Server Essentials から Windows Server 2012 R2 Standard、完全な 2 つの手順を決定したら。  
  
1. Windows Server 2012 R2 Standard、およびユーザーやデバイスのクライアント アクセス ライセンスのお客様の環境の適切な数のライセンスを購入します。  
  
    小売店、ディストリビューター、または利用して、Windows Server 2012 R2 Standard のライセンスを購入することができます、 [Microsoft パートナー](https://pinpoint.microsoft.com/SelectCulture.aspx)します。  
  
   > [!NOTE]
   >  Windows Server 2012 R2 Standard を最初に購入し、2 つの仮想インスタンスのいずれかとして Windows Server Essentials をインストールするにダウン グレード権を行使する場合は、何も追加購入する必要はありません。  
   >   
   >  ボリューム ライセンス チャネルを通じて Windows Server 2012 R2 Standard を購入する場合は、Windows Server 2012 R2 Standard ボリューム ライセンス サービス センター (VLSC) からの ISO イメージとプロダクト キーをダウンロードできます。  
   >   
   >  ISO イメージと評価版のプロダクト キーをダウンロードから Windows Server Essentials の他のチャネルから Windows Server 2012 R2 Standard を購入した場合、 [TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx)します。 次の手順に記載されている移行操作を実行すると、評価版の製品がフル ライセンス版のサポート対象製品に変換されます。  
  
2. 管理者として Windows PowerShell を開き、次のコマンドを実行します。  
  
    **dism /online /set-edition:ServerStandard /accepteula /productkey:** *プロダクト キー* (場所*プロダクト キー*は Windows Server 2012 R2 Standard のコピーのプロダクト キー)。  
  
    サーバーが再起動すると、移行プロセスが完了します。  
  
   切り替えた後は、Windows Server Essentials の機能は、サーバー上に残ります、最大 100 人のユーザーと 200 台のデバイスのサポートされています。  
  
## <a name="see-also"></a>関連項目  
  

-   [サーバー データの Windows Server Essentials への移行](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [サーバー データの Windows Server Essentials への移行](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

