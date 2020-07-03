---
title: wdsutil
description: Windows 展開サービスサーバーの管理に使用されるコマンドラインユーティリティである wdsutil のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3a1965a0-8677-40cc-9495-30ae806808d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 14fa0d962d1104279211696c7ff8b80d0f1b6fbf
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930833"
---
# <a name="wdsutil"></a>wdsutil

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

wdsutil は、Windows 展開サービスサーバーの管理に使用するコマンドラインユーティリティです。 これらのコマンドを実行するには、[**スタート**] ボタンをクリックし、[**コマンドプロンプト**] を右クリックして、[**管理者として実行**] をクリックします。
## <a name="commands"></a>コマンド
|コマンド|説明|
|------|--------|
|[[追加] コマンドを使用する](using-the-add-command.md)|オブジェクトまたはプレステージコンピューターを追加します。|
|[承認-AutoaddDevices コマンドの使用](using-the-approve-autoadddevices-command.md)|管理者の承認待ちのコンピューターを承認します。|
|[RiprepImage コマンドの使用](using-the-convert-riprepimage-command.md)|既存のリモートインストール準備 (RIPrep) イメージを Windows イメージ (.wim) ファイルに変換します。|
|[Copy コマンドの使用](using-the-copy-command.md)|イメージ、ドライバー グループをコピーします。|
|[Delete AutoaddDevices コマンドの使用](using-the-delete-autoadddevices-command.md)|自動追加データベースにあるコンピューターのうち、サーバー上のコンピューターに関する情報を格納するコンピューターを削除します。|
|[無効にするコマンドを使用してください。](using-the-disable-command.md)|Windows 展開サービスのすべてのサービスを無効にします。|
|[クライアント接続を切断コマンドを使用してください。](using-the-disconnect-client-command.md)|マルチキャスト転送または名前空間を使用して、クライアントを切断します。|
|[有効にするコマンドを使用してください。](using-the-enable-command.md)|Windows 展開サービスのすべてのサービスを有効にします。|
|[イメージのエクスポート コマンドを使用してください。](using-the-export-image-command.md)|イメージストアから .wim ファイルにイメージをエクスポートします。|
|[Get コマンドを使用します。](using-the-get-command.md)|指定したオブジェクトに関するプロパティと属性を取得します。|
|[Initialize サーバー コマンドを使用してください。](using-the-initialize-server-command.md)|初期使用のために Windows 展開サービスサーバーを構成します。|
|[新しいコマンドを使用してください。](using-the-new-command.md)|新しいキャプチャと検出イメージだけでなく、マルチキャスト転送と名前空間を作成します。|
|[コマンドの進行状況](the-progress-command.md)|コマンドの実行中に進行状況の状態を表示します。|
|[拒否 AutoaddDevices コマンドの使用](using-the-reject-autoadddevices-command.md)|管理者の承認待ちのコンピューターを拒否します。|
|[[削除] コマンドの使用](using-the-remove-command.md)|オブジェクトを削除します。|
|[置換イメージのコマンドを使用してください。](using-the-replace-image-command.md)|ブートイメージまたはインストールイメージを、そのイメージの新しいバージョンに置き換えます。|
|[Set コマンド](the-set-command.md)|指定したオブジェクトのプロパティと属性を設定します。|
|[[サーバーの開始] コマンド](the-start-server-command.md)|マルチキャスト転送、名前空間、トランスポートサーバーなど、Windows 展開サービスサーバー上のすべてのサービスを開始します。|
|[停止サーバー コマンド](the-stop-server-command.md)|Windows 展開サービスサーバー上のすべてのサービスを停止します。|
|[非サーバー オプション](the-uninitialize-server-option.md)|サーバーの初期化中に行われた変更を元に戻します。|
|[更新プログラム ServerFiles コマンド](the-update-serverfiles-command.md)|RemoteInstall 共有上のサーバーファイルを更新します。|
|[Verbose コマンド](the-verbose-command.md)|指定したコマンドの詳細出力を表示します。|
