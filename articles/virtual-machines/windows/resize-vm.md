---
title: PowerShell を使って Azure 内の Windows VM のサイズを変更する | Microsoft Docs
description: Resource Manager デプロイメント モデルで作成された Windows 仮想マシンのサイズを Azure Powershell を使用して変更します。
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: cynthn
ms.openlocfilehash: d2010ee9017416360069c74118b8ae25e71e1da7
ms.sourcegitcommit: 1362e3d6961bdeaebed7fb342c7b0b34f6f6417a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2018
---
# <a name="resize-a-windows-vm"></a>Windows VM のサイズ変更
この記事では、Resource Manager デプロイメント モデルで作成された Windows VM のサイズを Azure Powershell を使用して変更する方法について説明します。

仮想マシン (VM) を作成した後、VM のサイズを変更することで、VM をスケールアップまたはスケールダウンできます。 場合によっては、先に VM の割り当てを解除する必要があります。 これは、現在 VM をホストしているハードウェア クラスターで新しいサイズを使用できない場合に発生する可能性があります。

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>可用性セット内にない Windows VM のサイズ変更
1. VM がホストされているハードウェア クラスターで使用できる VM のサイズを一覧表示します。 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. 目的のサイズが表示される場合は、次のコマンドを実行して VM のサイズを変更します。 目的のサイズが表示されない場合は、手順 3. に進みます。
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. 目的のサイズが表示されない場合は、次のコマンドを実行して VM の割り当てを解除します。その後、VM のサイズを変更して、再起動します。
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -Name $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> VM の割り当てを解除すると、VM に割り当てられているすべての動的 IP アドレスが解放されます。 OS とデータ ディスクには影響しません。 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>可用性セット内の Windows VM のサイズ変更
現在 VM をホストしているハードウェア クラスターで可用性セット内の VM の新しいサイズを使用できない場合、可用性セット内のすべての VM の割り当てを解除して、VM のサイズを変更する必要があります。 また、1 つの VM のサイズを変更した後、可用性セット内の他の VM のサイズを更新する必要がある場合もあります。 可用性セット内の VM のサイズを変更するには、次の手順を実行します。

1. VM がホストされているハードウェア クラスターで使用できる VM のサイズを一覧表示します。
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. 目的のサイズが表示される場合は、次のコマンドを実行して VM のサイズを変更します。 表示されない場合は、手順 3. に進みます。
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. 目的のサイズが表示されない場合は、次の手順を続行して、可用性セット内のすべての VM の割り当てを解除し、VM のサイズを変更してから再起動します。
4. 可用性セット内のすべての VM を停止します。
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. 可用性セット内の VM のサイズを変更して、再起動します。
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a>次の手順
* スケーラビリティを高めるには、複数の VM インスタンスを実行してスケール アウトします。詳細については、[仮想マシン スケール セットでのマシンの自動スケール](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md)に関するページを参照してください。

