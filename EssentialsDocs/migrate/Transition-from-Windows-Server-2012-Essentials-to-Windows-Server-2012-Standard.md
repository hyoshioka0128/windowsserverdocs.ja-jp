---
title: "Windows Server Essentials から Windows Server 2012 Standard への移行"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51bcf124-c215-4e9d-9fa8-a90fa2c2fa22
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d2005b72adede72b718fa5b49b93435f5fbac1bd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-standard"></a>Windows Server Essentials から Windows Server 2012 Standard への移行

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

 Windows Server® 2012 Essentials は、最大 25 ユーザーおよび 50 台のデバイス サポートしています。 制限を超える必要がある場合、Windows Server Essentials から Windows Server 2012 Standard へライセンスに準拠を保つために、ライセンスのインプレース移行を実行できます。  
  
## <a name="how-the-transition-affects-user-and-device-limits"></a>ユーザーとデバイスの移行の影響を制限します。  
 Windows Server 2012 Standard への移行後、ユーザー アカウントとデバイスの制限がなくなる一方、な (ダッシュ ボード、リモート Web アクセス、クライアント コンピューターのバックアップなど)、Windows Server Essentials に固有の機能を引き続き利用できます。 ただし、これらの機能の技術的な制限は、最大で 75 のユーザー アカウントと 75 台のデバイスのサポートします。 75 を超えるユーザー アカウントまたはデバイスの追加が必要になった場合は、Windows Server Essentials の機能をオフにして Windows Server 2012 Standard のネイティブ ツールを使用してユーザー アカウントとデバイスを管理する必要があります。  
  
> [!IMPORTANT]
>   Windows Server 2012 Standard の各ユーザーまたはデバイスを環境内でクライアント アクセス ライセンス (CAL) が必要です。 これは、CAL モデルを使用せず、Cal が付属していませんが、Windows Server Essentials とは異なるです。  Windows Server Essentials から Windows Server 2012 Standard への遷移、時に、適切な数と種類の Cal (ほとんどのお客様は user Cal を購入) 環境を購入する必要があります。  
  
## <a name="before-the-transition"></a>移行する前に  
  
-   Windows Server Essentials から Windows Server 2012 Standard への移行、する前に、サーバー データを完全にバックアップを必要があります。  
  
    > [!IMPORTANT]
    >  せず、サーバーの完全バックアップ、移行前された状態にサーバーを復元することはできません。  
  
-   さらに、読み取りを理解して、エンド ユーザー ライセンス契約 (EULA) の Windows Server 2012 Standard を確認します。 EULA を表示します。  
  
    1.  管理者としてコマンド ウィンドウを開きます。  
  
    2.  次のコマンドを実行します。  
  
         **dism/online//set-edition: ServerStandard /geteula: eula のパス**  
  
         ここで**eula path**、EULA ファイルを保存する場所を表します。 たとえば、C:\ws8std_eula.rtf します。  必ずファイル名拡張子として .rtf を使用します。  
  
    3.  ファイルを保存する場所を開きを開くには、ファイルをダブルクリックします。  
  
## <a name="transition-to--windows-server-2012-standard"></a>Windows Server 2012 Standard への移行  
 後に移行する Windows Server Essentials から Windows Server 2012 Standard へ、完全なこれら 2 つの手順を決定します。  
  
1.  Windows Server 2012 Standard および環境内のユーザーまたはデバイスのクライアント アクセス ライセンスの適切な数のライセンスを購入します。  
  
     販売店、ディストリビュータからまたはの支援を Windows Server 2012 Standard 用ライセンスを購入することができます、[Microsoft パートナー](https://pinpoint.microsoft.com/SelectCulture.aspx)します。  
  
    > [!NOTE]
    >  Windows Server 2012 Standard を最初に購入してため、2 つの仮想インスタンスのいずれかとして Windows Server Essentials をインストールするにダウン グレード権を行使した場合は、何も追加購入する必要はありません。  
    >   
    >  ボリューム ライセンス チャネルを通じて Windows Server 2012 Standard を購入する場合は、Windows Server 2012 Standard ボリューム ライセンス サービス センター (VLSC) からの ISO イメージとプロダクト キーをダウンロードできます。  
    >   
    >  その他のすべてのチャンネルから Windows Server 2012 Standard を購入する場合は、ダウンロードできます ISO イメージと評価版のプロダクト キーから Windows Server Essentials の[TechNet Evaluation Center](https://technet.microsoft.com/evalcenter/jj659306.aspx)します。 次の手順の説明に従って、移行を実行すると、評価版の製品が完全にライセンス サポートされている製品に変換されます。  
  
2.  管理者は、Windows PowerShell を開き、次のコマンドを実行します。  
  
     **dism/online//set-edition: ServerStandard /accepteula /productkey:***プロダクト キー*  
  
     ここで*プロダクト キー*は Windows Server 2012 Standard のコピーのプロダクト キーです。  
  
     移行プロセスを終了するサーバーを再起動します。  
  
 移行後、Windows Server Essentials の機能はサーバーに残り、最大で 75 人のユーザーと 75 台のデバイスでサポートされて これらの制限のどちらかを超える場合は、ユーザー アカウントとデバイスを管理する Windows Server 2012 Standard ネイティブ ツールを使用する必要があります。  
  
 さらに、Windows Server 2012 Standard への移行後の Windows Server Essentials メディア機能は利用できなくします。 これには、リモート Web アクセス、およびダッシュ ボードのメディア設定のメディア機能が含まれます。  
  
## <a name="turn-off--windows-server-essentials-features"></a>Windows Server Essentials の機能をオフにします。  
 サーバーを管理するには、Windows Server Essentials ダッシュ ボードまたはその他の付加価値機能を不要な場合は、機能をオフにして、サーバーからそれらを削除します。  
  
 **Windows Server Essentials 機能のウィザードをオフにする**、機能をアンインストールするのに役立ちます。 Windows Server Essentials サーバー ソフトウェアによって作成されたファイルのサーバーもクリーンアップされます。  一部のクリーニング操作は、他のユーザーは、サーバーを再起動した後、開始中に、すぐに実行されます。  
  
 **Windows Server Essentials 機能のウィザードをオフにする**ウィザードを完了する前にすべてのアドインを手動でアンインストールすることが必要です。 インストールされているアドインの一覧を表示するには、ダッシュ ボードで [アプリケーション] ページを開きます。 ウィザードはアラートを生成する場合は、インストールされているアドインを検出し、それらをアンインストールするように求められます。  
  
 **Windows Server Essentials 機能のウィザードをオフにする**、Windows Server Essentials の機能を無効にした後のコンピューターのクライアントのバックアップ ファイルを保持するかどうかを選択することができます。  
  
 実行する 2 つの方法がある、**Windows Server Essentials 機能のウィザードをオフにする**ダッシュ ボードから。  
  
#### <a name="from-the-alert"></a>アラートから  
  
1.  ダッシュ ボードで、アラート ビューアーを開きます。  
  
2.  [整理] 一覧で、移行後、Windows Server Essentials の機能を無効化について報告しているアラートを選択します。  
  
3.  をクリックして、アラートの**Windows Server Essentials の機能をオフにする**します。  
  
#### <a name="from-the-get-help-and-support-pane"></a>ヘルプとサポート] ウィンドウから  
  
1.  ホーム ページ、[ヘルプを取得およびサポートします。  
  
2.  をクリックして**Windows Server Essentials 機能のウィザードをオフにする**します。  
  
 によって一部のタスクを実行することは、**Windows Server Essentials 機能のウィザードをオフにする**は正常に完了しません。 場合によっては、これは、実行、ダッシュ ボードをできなきます。 このような場合は、ファイルを実行して、ウィザードを手動で開始することができます。  
  
 **%systemdrive%\Program files \windows Server\Bin\TurnOffFeaturesWizard.exe**  
  
## <a name="see-also"></a>参照してください。  
  

-   [Windows Server 2012 R2 Standard への移行](Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [Windows Server Essentials へのサーバー データを移行します。](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server 2012 R2 Standard への移行](../migrate/Transition-from-Windows-Server-2012-R2-Essentials-to-Windows-Server-2012-R2-Standard.md)  
  
-   [Windows Server Essentials へのサーバー データを移行します。](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

