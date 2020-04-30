---
title: bitsadmin
description: '**Bitsadmin**の Windows コマンドに関するトピック。これは、ジョブの作成、ダウンロード、アップロード、および進行状況の監視に使用されるコマンドラインツールです。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4853036e-1df8-45ad-8be6-cfb097b8dd27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a9cbf715474621b7102d0baf0c448e0ee578bf9
ms.sourcegitcommit: 1d83ca198c50eef83d105151551c6be6f308ab94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2020
ms.locfileid: "82605562"
---
# <a name="bitsadmin"></a>bitsadmin

> **適用対象**: windows Server (半期チャネル)、windows server 2016、windows Server 2012 R2、windows server 2012、windows 10

Bitsadmin は、ジョブの作成、ダウンロード、アップロード、および進行状況の監視に使用されるコマンドラインツールです。 Bitsadmin ツールは、実行する作業を識別するためにスイッチを使用します。 または`bitsadmin /help`を`bitsadmin /?`呼び出して、スイッチの一覧を取得できます。

ほとんどのスイッチに`<job>`はパラメーターが必要です。これは、ジョブの表示名または GUID に設定します。 ジョブの表示名は一意である必要はありません。 **/Create**スイッチと **/list**スイッチは、ジョブの GUID を返します。

既定では、自分のジョブに関する情報にアクセスできます。 別のユーザーのジョブに関する情報にアクセスするには、管理者特権が必要です。 ジョブが管理者特権で作成された場合は、管理者特権のウィンドウから**bitsadmin**を実行する必要があります。それ以外の場合は、ジョブへの読み取り専用アクセス権が付与されます。

スイッチの多くは、 [BITS インターフェイス](https://docs.microsoft.com/windows/win32/bits/bits-interfaces)のメソッドに対応しています。 スイッチの使用に関連する可能性のあるその他の詳細については、対応するメソッドを参照してください。

ジョブの作成、ジョブのプロパティの設定と取得、およびジョブの状態の監視を行うには、次のスイッチを使用します。 これらのスイッチのいくつかを使用してタスクを実行する方法を示す例については、「 [bitsadmin の例](bitsadmin-examples.md)」を参照してください。

## <a name="available-switches"></a>使用可能なスイッチ

- [bitsadmin/addfile](bitsadmin-addfile.md)
- [bitsadmin/addfileset](bitsadmin-addfileset.md)
- [bitsadmin/addfilewithranges](bitsadmin-addfilewithranges.md)
- [bitsadmin/cache](bitsadmin-cache.md)
- [bitsadmin/cache/delete](bitsadmin-cache-and-delete.md)
- [bitsadmin/cache/deleteurl](bitsadmin-cache-and-deleteurl.md)
- [bitsadmin/cache/getexpirationtime](bitsadmin-cache-and-getexpirationtime.md)
- [bitsadmin/cache/getlimit](bitsadmin-cache-and-getlimit.md)
- [bitsadmin/cache/help](bitsadmin-cache-and-help.md)
- [bitsadmin/cache/info](bitsadmin-cache-and-info.md)
- [bitsadmin/cache/list](bitsadmin-cache-and-list.md)
- [bitsadmin/cache/setexpirationtime](bitsadmin-cache-and-setexpirationtime.md)
- [bitsadmin/cache/setlimit](bitsadmin-cache-and-setlimit.md)
- [bitsadmin/cache/clear](bitsadmin-cache-clear.md)
- [bitsadmin/cancel](bitsadmin-cancel.md)
- [bitsadmin/完了](bitsadmin-complete.md)
- [bitsadmin/create](bitsadmin-create.md)
- [bitsadmin/例](bitsadmin-examples.md)
- [bitsadmin/getaclflags](bitsadmin-getaclflags.md)
- [bitsadmin/getbytestotal](bitsadmin-getbytestotal.md)
- [bitsadmin/getbytestransferred](bitsadmin-getbytestransferred.md)
- [bitsadmin/getclientcertificate](bitsadmin-getclientcertificate.md)
- [bitsadmin/getcompletiontime](bitsadmin-getcompletiontime.md)
- [bitsadmin/getcreationtime](bitsadmin-getcreationtime.md)
- [bitsadmin/getcustomheaders](bitsadmin-getcustomheaders.md)
- [bitsadmin/getdescription](bitsadmin-getdescription.md)
- [bitsadmin/getdisplayname](bitsadmin-getdisplayname.md)
- [bitsadmin/geterror](bitsadmin-geterror.md)
- [bitsadmin/geterrorcount](bitsadmin-geterrorcount.md)
- [bitsadmin/getfilestotal](bitsadmin-getfilestotal.md)
- [bitsadmin/getfilestransferred](bitsadmin-getfilestransferred.md)
- [bitsadmin/gea のフラグ](bitsadmin-gethelpertokenflags.md)
- [bitsadmin/gepertokensid](bitsadmin-gethelpertokensid.md)
- [bitsadmin/gethttpmethod](bitsadmin-gethttpmethod.md)
- [bitsadmin/getmaxdownloadtime](bitsadmin-getmaxdownloadtime.md)
- [bitsadmin/getminretrydelay](bitsadmin-getminretrydelay.md)
- [bitsadmin/getmodificationtime](bitsadmin-getmodificationtime.md)
- [bitsadmin/getnoprogresstimeout](bitsadmin-getnoprogresstimeout.md)
- [bitsadmin/getnotifycmdline](bitsadmin-getnotifycmdline.md)
- [bitsadmin/getnotifyflags](bitsadmin-getnotifyflags.md)
- [bitsadmin/getnotifyinterface](bitsadmin-getnotifyinterface.md)
- [bitsadmin/getowner](bitsadmin-getowner.md)
- [bitsadmin/getpeercachingflags](bitsadmin-getpeercachingflags.md)
- [bitsadmin/getpriority](bitsadmin-getpriority.md)
- [bitsadmin/getproxybypasslist](bitsadmin-getproxybypasslist.md)
- [bitsadmin/getproxylist](bitsadmin-getproxylist.md)
- [bitsadmin/getproxyusage](bitsadmin-getproxyusage.md)
- [bitsadmin/getreplydata](bitsadmin-getreplydata.md)
- [bitsadmin/getreplyfilename](bitsadmin-getreplyfilename.md)
- [bitsadmin/getreplyprogress](bitsadmin-getreplyprogress.md)
- [bitsadmin/getsecurityflags](bitsadmin-getsecurityflags.md)
- [bitsadmin/getstate](bitsadmin-getstate.md)
- [bitsadmin/gettemporaryname](bitsadmin-gettemporaryname.md)
- [bitsadmin/gettype](bitsadmin-gettype.md)
- [bitsadmin/getvalidationstate](bitsadmin-getvalidationstate.md)
- [bitsadmin/help](bitsadmin-help.md)
- [bitsadmin/情報](bitsadmin-info.md)
- [bitsadmin/list](bitsadmin-list.md)
- [bitsadmin/listfiles](bitsadmin-listfiles.md)
- [bitsadmin/makecustomheaderswriteonly](bitsadmin-makecustomheaderswriteonly.md)
- [bitsadmin/モニタ](bitsadmin-monitor.md)
- [bitsadmin/nowrap](bitsadmin-nowrap.md)
- [bitsadmin/ピアキャッシュ](bitsadmin-peercaching.md)
- [bitsadmin/ピアキャッシュ/getconfigurationflags](bitsadmin-peercaching-and-getconfigurationflags.md)
- [bitsadmin/ピアキャッシュ/help](bitsadmin-peercaching-and-help.md)
- [bitsadmin/ピアキャッシュ/setconfigurationflags](bitsadmin-peercaching-and-setconfigurationflags.md)
- [bitsadmin/ピア](bitsadmin-peers.md)
- [bitsadmin/ピア/clear](bitsadmin-peers-and-clear.md)
- [bitsadmin/検出](bitsadmin-peers-and-discover.md)
- [bitsadmin/ピア/help](bitsadmin-peers-and-help.md)
- [bitsadmin/ピア/list](bitsadmin-peers-and-list.md)
- [bitsadmin/rawreturn](bitsadmin-rawreturn.md)
- [bitsadmin/removeclientcertificate](bitsadmin-removeclientcertificate.md)
- [bitsadmin/removecredentials](bitsadmin-removecredentials.md)
- [bitsadmin/replaceremoteprefix](bitsadmin-replaceremoteprefix.md)
- [bitsadmin/リセット](bitsadmin-reset.md)
- [bitsadmin/再開](bitsadmin-resume.md)
- [bitsadmin/setaclflag](bitsadmin-setaclflag.md)
- [bitsadmin/setclientcertificatebyid](bitsadmin-setclientcertificatebyid.md)
- [bitsadmin/setclientcertificatebyname](bitsadmin-setclientcertificatebyname.md)
- [bitsadmin/setcredentials](bitsadmin-setcredentials.md)
- [bitsadmin/setcustomheaders](bitsadmin-setcustomheaders.md)
- [bitsadmin/setdescription](bitsadmin-setdescription.md)
- [bitsadmin/setdisplayname](bitsadmin-setdisplayname.md)
- [bitsadmin/sesetpertoken](bitsadmin-sethelpertoken.md)
- [bitsadmin/sepertokenflags](bitsadmin-sethelpertokenflags.md)
- [bitsadmin/sethttpmethod](bitsadmin-sethttpmethod.md)
- [bitsadmin/setmaxdownloadtime](bitsadmin-setmaxdownloadtime.md)
- [bitsadmin/setminretrydelay](bitsadmin-setminretrydelay.md)
- [bitsadmin/setnoprogresstimeout](bitsadmin-setnoprogresstimeout.md)
- [bitsadmin/setnotifycmdline](bitsadmin-setnotifycmdline.md)
- [bitsadmin/setnotifyflags](bitsadmin-setnotifyflags.md)
- [bitsadmin/setpeercachingflags](bitsadmin-setpeercachingflags.md)
- [bitsadmin/setpriority](bitsadmin-setpriority.md)
- [bitsadmin/setproxysettings](bitsadmin-setproxysettings.md)
- [bitsadmin/setreplyfilename](bitsadmin-setreplyfilename.md)
- [bitsadmin/setsecurityflags](bitsadmin-setsecurityflags.md)
- [bitsadmin/setvalidationstate](bitsadmin-setvalidationstate.md)
- [bitsadmin/中断](bitsadmin-suspend.md)
- [所有権の bitsadmin/獲得](bitsadmin-takeownership.md)
- [bitsadmin/転送](bitsadmin-transfer.md)
- [bitsadmin/util](bitsadmin-util.md)
- [bitsadmin/ユーティリティ/enableanalytics チャネル](bitsadmin-util-and-enableanalyticchannel.md)
- [bitsadmin/util/getieproxy](bitsadmin-util-and-getieproxy.md)
- [bitsadmin/util/help](bitsadmin-util-and-help.md)
- [bitsadmin/util/repairservice](bitsadmin-util-and-repairservice.md)
- [bitsadmin/util/setieproxy](bitsadmin-util-and-setieproxy.md)
- [bitsadmin/util/version](bitsadmin-util-and-version.md)
- [bitsadmin/wrap](bitsadmin-wrap.md)
