---
title: Azure デバイス ツインを使用して MXChip IoT DevKit ユーザー LED を制御する | Microsoft Docs
description: このチュートリアルでは、Azure IoT Hub デバイス ツインを使用して DevKit の状態を監視し、ユーザー LED を制御する方法について説明します。
services: iot-hub
documentationcenter: ''
author: liydu
manager: timlt
tags: ''
keywords: ''
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2018
ms.author: liydu
ms.openlocfilehash: 33d8a36cc88bd1c263f2c4a38a59e04e1253357c
ms.sourcegitcommit: e2adef58c03b0a780173df2d988907b5cb809c82
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2018
---
# <a name="mxchip-iot-devkit"></a>MXChip IoT DevKit

この例を使用すると、MXChip IoT DevKit の WiFi 情報とセンサーの状態を監視し、Azure IoT Hub デバイス ツインを使用してユーザー LED の色を制御することができます。

## <a name="what-you-learn"></a>学習内容

- MXChip IoT DevKit センサーの状態を監視する方法。
- Azure デバイス ツインを使用して DevKit の RGB LED の色を制御する方法。

## <a name="what-you-need"></a>必要なもの

- [ファースト ステップ ガイド](https://docs.microsoft.com/azure/iot-hub/iot-hub-arduino-iot-devkit-az3166-get-started)に従って開発環境を設定してください。
- GitBash ターミナル ウィンドウ (または他の Git コマンドライン インターフェイス) から、次のコマンドを入力します。
    - `git clone https://github.com/DevKitExamples/DevKitState.git`
    - `cd DevKitState`
    - `code .`

## <a name="provision-azure-services"></a>Azure サービスのプロビジョニング

1. Visual Studio Code で **[タスク]** ドロップダウン メニューをクリックし、**[タスクの実行]** - **[cloud-provision]** を選択します。
2. **[ようこそ]** パネルの **[端末]** タブに進行状況状況が表示されます。
3. *"What subscription would you like to choose"* (どのサブスクリプションを選択しますか) というメッセージが表示されたら、サブスクリプションを選択します。
4. リソース グループを選択します。 
 
    > [!NOTE]
    > 無料の IoT Hub が既にある場合、この手順はスキップされます。

5. *"What IoT hub would you like to choose"* (どの IoT Hub を選択しますか) というメッセージが表示されたら、IoT Hub を選択します。
6. *関数アプリ: 関数アプリ名: xxx* のような内容が表示されます。 関数アプリ名を書き留めます。これは後の手順で使用します。
7. Azure Resource Manager テンプレートのデプロイが完了するまで待ちます。完了すると、*"Resource Manager template deployment: Done"* (Resource Manager テンプレートのデプロイ: 完了) というメッセージが表示されます。

## <a name="deploy-function-app"></a>関数アプリのデプロイ

1. Visual Studio Code で **[タスク]** ドロップダウン メニューをクリックし、**[タスクの実行]** - **[cloud-deploy]** を選択します。
2. 関数のアプリ コードのアップロード プロセスが完了するまで待ちます。*"function app deploys: Done"* (関数アプリのデプロイ: 完了) というメッセージが表示されます。

## <a name="configure-iot-hub-device-connection-string-in-devkit"></a>DevKit で IoT Hub デバイスの接続文字列を構成する

1. MXChip IoT DevKit をコンピューターに接続します。
2. Visual Studio Code で **[タスク]** ドロップダウン メニューをクリックし、**[タスクの実行]** - **[config-device-connection]** を選択します。
3. MXChip IoT DevKit で、**[A]** ボタンを押したまま **[リセット]** ボタンを押し、**[A]** ボタンを放すと、DekKit が構成モードに切り替わります。
4. 接続文字列の構成プロセスが完了するまで待ちます。

## <a name="upload-arduino-code-to-devkit"></a>DevKit に Arduino コードをアップロードする

MXChip IoT DevKit がコンピューターに接続されている状態で、次の手順を実行します。
1. Visual Studio Code で **[タスク]** ドロップダウン メニューをクリックし、**[ビルド タスクの実行]** を選択します。Arduino スケッチがコンパイルされ、DevKit にアップロードされます。
2. スケッチが正常にアップロードされると、*"Build & Upload Sketch: success"* (スケッチのビルドとアップロード: 成功) というメッセージが表示されます。

## <a name="monitor-devkit-state-in-browser"></a>ブラウザーで DevKit の状態を監視する

1. Web ブラウザーで、「[必要なもの](#whatyouneed)」の手順で作成した `DevKitState\web\index.html` ファイルを開きます。
2. 次の Web ページが表示されます。![関数アプリ名を指定します。](media/iot-hub-arduino-iot-devkit-az3166-devkit-state/devkit-state-function-app-name.png)
1. 書き留めた関数アプリ名を入力します。
2. **[接続]** ボタンをクリックします
3. 数秒間でページが更新され、DevKit の WiFi 接続状態とオンボード センサーの状態が表示されます。

## <a name="control-the-devkits-user-led"></a>DevKit のユーザー LED を制御する

1. Web ページの図にあるユーザー LED のグラフィックをクリックします。
2. 数秒間で画面が更新され、ユーザー LED の現在の色の状態が表示されます。
3. RGB スライダー コントロールのさまざまな場所をクリックして、RGB LED の色の値を変更してみてください。

## <a name="example-operation"></a>操作の例

![テスト手順の例](media/iot-hub-arduino-iot-devkit-az3166-devkit-state/devkit-state.gif)

## <a name="next-steps"></a>次の手順

ここでは、以下の方法について学習しました。
- MXChip IoT DevKit デバイスを Azure IoT Suite に接続する。
- Azure IoT デバイス ツイン関数を使用して、DevKit の RGB LED の色を検出して制御します。

推奨される次の手順は以下のとおりです。

* [Azure IoT Suite の概要](https://docs.microsoft.com/azure/iot-suite/)
* [MXChip IoT DevKit デバイスを Microsoft IoT Central アプリケーションに接続する](https://docs.microsoft.com/microsoft-iot-central/howto-connect-devkit)
