---
title: bitsadmin
description: '**Bitsadmin**の Windows コマンドのトピック bitsadmin は、ジョブの作成、ダウンロード、アップロード、および進行状況の監視に使用できるコマンドラインツールです。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4853036e-1df8-45ad-8be6-cfb097b8dd27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b53293b28a83ecced34d248741996c958531d517
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380096"
---
# <a name="bitsadmin"></a>bitsadmin

> **適用対象**:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10

bitsadmin はコマンドラインツールです。このツールを使用すると、ジョブのダウンロードやアップロードを行ったり、ジョブの進行状況を監視したりすることができます。 Bitsadmin ツールは、実行する作業を識別するためにスイッチを使用します。  スイッチの一覧を取得するには、`bitsadmin /?` または `bitsadmin /HELP` を呼び出します。

ほとんどのスイッチでは、ジョブの表示名 (GUID) に設定する @no__t 0Job @ no__t パラメーターが必要です。 ジョブの表示名は一意ではない場合があることに注意してください。 **/Create**スイッチと **/list**スイッチは、ジョブの GUID を返します。

既定では、自分のジョブに関する情報にアクセスできます。 別のユーザーのジョブに関する情報にアクセスするには、管理者特権が必要です。 ジョブが管理者特権で作成された場合は、管理者特権のウィンドウから bitsadmin を実行する必要があります。それ以外の場合は、ジョブへの読み取り専用アクセス権が付与されます。

スイッチの多くは、 [BITS インターフェイス](/windows/desktop/bits/bits-interfaces)のメソッドに対応しています。 スイッチの使用に関連する可能性のあるその他の詳細については、対応するメソッドを参照してください。

ジョブの作成、ジョブのプロパティの設定と取得、およびジョブの状態の監視を行うには、次のスイッチを使用します。 これらのスイッチのいくつかを使用してタスクを実行する方法を示す例については、「 [bitsadmin の例](bitsadmin-examples.md)」を参照してください。

## <a name="switches"></a>スイッチ

[bitsadmin addfile](bitsadmin-addfile.md)  
[bitsadmin addfileset](bitsadmin-addfileset.md)  
[bitsadmin addfilewithranges](bitsadmin-addfilewithranges.md)  
[bitsadmin cache](bitsadmin-cache.md)  
[bitsadmin cancel](bitsadmin-cancel.md)  
[bitsadmin complete](bitsadmin-complete.md)  
[bitsadmin create](bitsadmin-create.md)  
[bitsadmin getaclflags](bitsadmin-getaclflags.md)  
[bitsadmin getbytestotal](bitsadmin-getbytestotal.md)  
[bitsadmin getbytestransferred](bitsadmin-getbytestransferred.md)  
[bitsadmin getclientcertificate](bitsadmin-getclientcertificate.md)  
[bitsadmin getcompletiontime](bitsadmin-getcompletiontime.md)  
[bitsadmin getcreationtime](bitsadmin-getcreationtime.md)  
[bitsadmin getcustomheaders](bitsadmin-getcustomheaders.md)  
[bitsadmin getdescription](bitsadmin-getdescription.md)  
[bitsadmin getdisplayname](bitsadmin-getdisplayname.md)  
[bitsadmin geterror](bitsadmin-geterror.md)  
[bitsadmin geterrorcount](bitsadmin-geterrorcount.md)  
[bitsadmin getfilestotal](bitsadmin-getfilestotal.md)  
[bitsadmin getfilestransferred](bitsadmin-getfilestransferred.md)  
[bitsadmin gethelpertokenflags](bitsadmin-gethelpertokenflags.md)  
[bitsadmin gethelpertokensid](bitsadmin-gethelpertokensid.md)  
[bitsadmin gethttpmethod](bitsadmin-gethttpmethod.md)
[bitsadmin getmaxdownloadtime](bitsadmin-getmaxdownloadtime.md)  
[bitsadmin getminretrydelay](bitsadmin-getminretrydelay.md)  
[bitsadmin getmodificationtime](bitsadmin-getmodificationtime.md)  
[bitsadmin getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)  
[bitsadmin getnotifycmdline](bitsadmin-getnotifycmdline.md)  
[bitsadmin getnotifyflags](bitsadmin-getnotifyflags.md)  
[bitsadmin getnotifyinterface](bitsadmin-getnotifyinterface.md)  
[bitsadmin getowner](bitsadmin-getowner.md)  
[bitsadmin getpeercachingflags](bitsadmin-getpeercachingflags.md)  
[bitsadmin getpriority](bitsadmin-getpriority.md)  
[bitsadmin getproxybypasslist](bitsadmin-getproxybypasslist.md)  
[bitsadmin getproxylist](bitsadmin-getproxylist.md)  
[bitsadmin getproxyusage](bitsadmin-getproxyusage.md)  
[bitsadmin getreplydata](bitsadmin-getreplydata.md)  
[bitsadmin getreplyfilename](bitsadmin-getreplyfilename.md)  
[bitsadmin getreplyprogress](bitsadmin-getreplyprogress.md)  
[bitsadmin getsecurityflags](bitsadmin-getsecurityflags.md)  
[bitsadmin getstate](bitsadmin-getstate.md)  
[bitsadmin gettemporaryname](bitsadmin-gettemporaryname.md)  
[bitsadmin gettype](bitsadmin-gettype.md)  
[bitsadmin getvalidationstate](bitsadmin-getvalidationstate.md)  
[bitsadmin help](bitsadmin-help.md)  
[bitsadmin info](bitsadmin-info.md)  
[bitsadmin list](bitsadmin-list.md)  
[bitsadmin listfiles](bitsadmin-listfiles.md)  
[bitsadmin makecustomheaderswriteonly](bitsadmin-makecustomheaderswriteonly.md)
[bitsadmin monitor](bitsadmin-monitor.md)  
[bitsadmin nowrap](bitsadmin-nowrap.md)  
[bitsadmin peercaching](bitsadmin-peercaching.md)  
[bitsadmin peers](bitsadmin-peers.md)  
[bitsadmin rawreturn](bitsadmin-rawreturn.md)  
[bitsadmin removeclientcertificate](bitsadmin-removeclientcertificate.md)  
[bitsadmin removecredentials](bitsadmin-removecredentials.md)  
[bitsadmin replaceremoteprefix](bitsadmin-replaceremoteprefix.md)  
[bitsadmin reset](bitsadmin-reset.md)  
[bitsadmin resume](bitsadmin-resume.md)  
[bitsadmin setaclflag](bitsadmin-setaclflag.md)  
[bitsadmin setclientcertificatebyid](bitsadmin-setclientcertificatebyid.md)  
[bitsadmin setclientcertificatebyname](bitsadmin-setclientcertificatebyname.md)  
[bitsadmin setcredentials](bitsadmin-setcredentials.md)  
[bitsadmin setcustomheaders](bitsadmin-setcustomheaders.md)  
[bitsadmin setdescription](bitsadmin-setdescription.md)  
[bitsadmin setdisplayname](bitsadmin-setdisplayname.md)  
[bitsadmin sethelpertoken](bitsadmin-sethelpertoken.md)  
[bitsadmin sethelpertokenflags](bitsadmin-sethelpertokenflags.md)  
[bitsadmin sethttpmethod](bitsadmin-sethttpmethod.md)
[bitsadmin setmaxdownloadtime](bitsadmin-setmaxdownloadtime.md)  
[bitsadmin setminretrydelay](bitsadmin-setminretrydelay.md)  
[bitsadmin setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)  
[bitsadmin setnotifycmdline](bitsadmin-setnotifycmdline.md)  
[bitsadmin setnotifyflags](bitsadmin-setnotifyflags.md)  
[bitsadmin setpeercachingflags](bitsadmin-setpeercachingflags.md)  
[bitsadmin setpriority](bitsadmin-setpriority.md)  
[bitsadmin setproxysettings](bitsadmin-setproxysettings.md)  
[bitsadmin setreplyfilename](bitsadmin-setreplyfilename.md)  
[bitsadmin setsecurityflags](bitsadmin-setsecurityflags.md)  
[bitsadmin setvalidationstate](bitsadmin-setvalidationstate.md)  
[bitsadmin suspend](bitsadmin-suspend.md)  
[bitsadmin takeownership](bitsadmin-takeownership.md)  
[bitsadmin transfer](bitsadmin-transfer.md)  
[bitsadmin util](bitsadmin-util.md)  
[bitsadmin wrap](bitsadmin-wrap.md)  
