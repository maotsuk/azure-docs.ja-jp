---
title: SELECT INTO を使用した Azure Stream Analytics クエリのデバッグ
description: この記事では、クエリ構文で SELECT INTO ステートメントを使って、Azure Stream Analytics ジョブでのクエリ中にデータをサンプリングする方法について説明します。
services: stream-analytics
author: jseb225
ms.author: jeanb
manager: kfile
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 04/20/2017
ms.openlocfilehash: ccaa6203e4bfe52758e26416646f9152ac5378ea
ms.sourcegitcommit: 5b2ac9e6d8539c11ab0891b686b8afa12441a8f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2018
---
# <a name="debug-queries-by-using-select-into-statements"></a>SELECT INTO ステートメントを使用したクエリのデバッグ

リアルタイムのデータ処理では、クエリの実行中にデータの状況を把握することが役に立つ場合があります。 Azure Stream Analytics ジョブの入力またはステップは複数回読み取ることができるため、追加の SELECT INTO ステートメントを記述することができます。 これを実行すると、中間データがストレージに出力され、データの正確性を確認できるようになります。これは、プログラムをデバッグする際に "*watch 変数*" によって行われる確認とまったく同じです。

## <a name="use-select-into-to-check-the-data-stream"></a>SELECT INTO を使用したデータ ストリームの確認

Azure Stream Analytics ジョブの次のサンプル クエリには、1 つのストリーム入力と 2 つの参照データ入力があり、Azure Table Storage に出力が行われます。 このクエリはイベント ハブと 2 つの参照 BLOB からのデータを結合し、名前とカテゴリの情報を取得します。

![SELECT INTO クエリの例](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

ジョブが実行中なのに出力でイベントが生成されていないことに注意してください。 次に示す **[監視]** タイルでは、入力からデータが生成中であることがわかります。しかし、**JOIN** のどのステップが原因ですべてのイベントが欠落したのかはわかりません。

![[監視] タイル](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
この状況では、いくつかの SELECT INTO ステートメントを追加して、JOIN の中間結果と入力から読み取られたデータの "ログを記録" することができます。

この例では、2 つの "一時的な出力" を新しく追加しました。 これらの出力には任意のシンクを使用してかまいません。 ここでは例として Azure Storage を使用します。

![SELECT INTO ステートメントの追加](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

クエリは次のように書き換えることができます。

![書き換えられた SELECT INTO クエリ](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

もう一度ジョブを開始して、数分間実行します。 temp1 と temp2 の各クエリによって、Visual Studio Cloud Explorer で次のテーブルが生成されます。

**temp1 テーブル**
![SELECT INTO temp1 テーブル](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)

**temp2 テーブル**
![SELECT INTO temp2 テーブル](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)

ご覧のとおり、temp1 と temp2 のどちらにもデータがあり、temp2 では名前列が正しく入力されています。 しかし出力には依然としてデータがなく、何らかの問題が発生していることがわかります。

![データのない SELECT INTO output1 テーブル](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

データをサンプリングすることで、2 番目の JOIN に問題があることがほぼ確実にわかります。 BLOB から参照データをダウンロードして確認できます。

![SELECT INTO 参照テーブル](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

ご覧のとおり、この参照データの GUID の形式が temp2 の "from" 列の形式と異なります。 これが、データが想定どおりに output1 に届かなかった原因です。

データ形式を修正して参照 BLOB にアップロードし、やり直すことができます。

![SELECT INTO 一時テーブル](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

今度は、出力のデータが想定どおりに書式設定されて入力されます。

![SELECT INTO 最終テーブル](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a>問い合わせ

さらにサポートが必要な場合は、 [Azure Stream Analytics フォーラム](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureStreamAnalytics)を参照してください。

## <a name="next-steps"></a>次のステップ

* [Azure Stream Analytics の概要](stream-analytics-introduction.md)
* [Azure Stream Analytics の使用](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics ジョブのスケーリング](stream-analytics-scale-jobs.md)
* [Stream Analytics Query Language Reference (Stream Analytics クエリ言語リファレンス)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics management REST API reference (Azure ストリーム分析の管理 REST API リファレンス)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

