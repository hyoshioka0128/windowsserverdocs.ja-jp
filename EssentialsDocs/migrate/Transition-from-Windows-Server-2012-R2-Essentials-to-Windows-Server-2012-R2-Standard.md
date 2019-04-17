---
title: "Windows Server Essentials から Windows Server 2012 R2 Standard への移行"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: d371e24b17310c0687666185f56fe07a135ff91f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-r2-standard"></a>Windows Server Essentials から Windows Server 2012 R2 Standard への移行

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Windows Server 2016 とは、簡単にクラウド コンピューティングへの移行の新しいテクノロジを紹介する際、現在のワークロードをサポートしているクラウドの準備完了のオペレーティング システムです。 Windows Server 2016 のコンテンツでは、準備することができます。

 Windows Server Essentials は、最大 25 ユーザーおよび 50 台のデバイス サポートしています。 制限を超える必要がある場合、Windows Server Essentials から Windows Server 2012 R2 Standard へライセンスに準拠を維持する、ライセンスのインプレース移行を実行できます。  
  
 Windows Server 2012 R2 Standard への移行後、ユーザー アカウントとデバイスの制限がなくなる一方、な (ダッシュ ボード、リモート Web アクセス、クライアント コンピューターのバックアップなど)、Windows Server Essentials に固有の機能を引き続き利用できます。 ただし、これらの機能の技術的な制限は、最大 100 ユーザー アカウントと 200 台のデバイスのサポートします。 クライアント コンピューターのバックアップ機能では、最大で 75 人のデバイスのバックアップをサポートします。  
  
> [!IMPORTANT]
>   Windows Server 2012 R2 Standard の各ユーザーまたはデバイスを環境内でクライアント アクセス ライセンス (CAL) が必要です。 これは、CAL モデルを使用せず、Cal が付属していませんが、Windows Server Essentials とは異なるです。 Windows Server Essentials から Windows Server 2012 R2 Standard への遷移、時に、適切な数と種類の Cal (ほとんどのお客様は user Cal を購入) 環境を購入する必要があります。  
  
## <a name="before-the-transition"></a>移行する前に  
  
-   Windows Server Essentials から Windows Server 2012 R2 Standard への移行、する前に、サーバー データを完全にバックアップを必要があります。  
  
    > [!IMPORTANT]
    >  せず、サーバーの完全バックアップ、移行前された状態にサーバーを復元することはできません。  
  
-   さらに、読み取りして Windows Server 2012 R2 Standard のエンド ユーザー ライセンス契約 (EULA) を理解することを確認してください。 EULA を表示します。  
  
    1.  管理者としてコマンド ウィンドウを開きます。  
  
    2.  次のコマンドを実行します。  
  
         **dism/online//set-edition: ServerStandard /geteula:***eula path* (ここで*eula のパス*、EULA ファイルの保存する場所を表します例: C:\ws8std_eula.rtf)。 必ずファイル名拡張子として .rtf を使用します。  
  
    3.  ファイルを保存する場所を開きを開くには、ファイルをダブルクリックします。  
  
## <a name="transition-to--windows-server-2012-r2-standard"></a>Windows Server 2012 R2 Standard への移行  
 後に転換する Windows Server Essentials から Windows Server 2012 R2 Standard、完全なこれら 2 つの手順を決定します。  
  
1.  Windows Server 2012 R2 Standard と、適切な数のユーザーや、環境のクライアント アクセス ライセンスのライセンスを購入します。  
  
     販売店、ディストリビュータからまたはのヘルプで、Windows Server 2012 R2 Standard のライセンスを購入することができます、[Microsoft パートナー](https://pinpoint.microsoft.com/SelectCulture.aspx)します。  
  
    > [!NOTE]
    >  Windows Server 2012 R2 Standard を最初に購入してため、2 つの仮想インスタンスのいずれかとして Windows Server Essentials をインストールするにダウン グレード権を行使した場合は、何も追加購入する必要はありません。  
    >   
    >  ボリューム ライセンス チャネルを通じて Windows Server 2012 R2 Standard を購入する場合は、Windows Server 2012 R2 Standard ボリューム ライセンス サービス センター (VLSC) からの ISO イメージとプロダクト キーをダウンロードできます。  
    >   
    >  ISO イメージと評価版のプロダクト キーをダウンロードから Windows Server Essentials の他の任意のチャンネルから Windows Server 2012 R2 Standard を購入した場合、[TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx)します。 次の手順の説明に従って、移行を実行すると、評価版の製品が完全にライセンス サポートされている製品に変換されます。  
  
2.  管理者は、Windows PowerShell を開き、次のコマンドを実行します。  
  
     **dism/online//set-edition: ServerStandard /accepteula /productkey:***プロダクト キー* (ここで*プロダクト キー*は Windows Server 2012 R2 Standard のコピーのプロダクト キー)。  
  
     移行プロセスを終了するサーバーを再起動します。  
  
 移行後、Windows Server Essentials の機能はサーバーに残り、最大 100 ユーザーおよび 200 台のデバイスでサポートされて  
  
## <a name="see-also"></a>参照してください。  
  

-   [Windows Server Essentials へのサーバー データを移行します。](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server Essentials へのサーバー データを移行します。](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

