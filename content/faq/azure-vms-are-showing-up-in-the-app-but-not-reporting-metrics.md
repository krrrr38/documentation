---
title: Azure VMs are showing up in the App but not reporting metrics
kind: faq
customnav: main_references
---

After properly installing the Azure Integration within Datadog, metrics from you Azure VMs and other services should begin to flow in ~15 minutes.

If after this time you see Azure VMs in your infrastructure list but no metrics are being reported, a few things can be happening.

1. Make sure you are looking for the right metrics.
    "Classic" virtual machine metrics will begin with the azure.vm namespace and ARM deployed virtual machine metrics will begin with the azure.compute_virtualmachines namespace.

2. If neither of these namespaces are returning metrics, make sure "Diagnostics" is turned on for the Virtual Machines within the Azure Portal. NOTE, only Boot diagnostics and Basic metrics are required.
    * For "Classic" VMs:
    {{< img src="faq/classic_vm.png" alt="classic_vm" responsive="true" >}}

    * For ARM deployed VMs:
    {{< img src="faq/arm_deployed_vm.png" alt="arm_deployed_vm" responsive="true" >}}


3. Make sure the Virtual machine is running.
    Our integration will not collect performance metrics for stopped/deallocated machines. However, the azure.vm.status metric will return 1 if the machine is running OR stopped (which will result in stopped VMs showing up in the infrastructure list). The associated status tag allows you to differentiate between running and not_running hosts. Make sure the host in question has status:running (and is running in the Azure portal!)
    {{< img src="faq/azure_vm_running.png" alt="azure_vm_running" responsive="true" >}}