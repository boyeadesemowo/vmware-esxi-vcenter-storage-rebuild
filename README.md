# From a Broken vCenter Deployment to a Clean VMware ESXi Rebuild

![Broken vs Clean ESXi Deployment](images/esxi-broken-vs-clean-rebuild.png)

## Overview
This project documents a real-world VMware ESXi and vCenter Server deployment
failure caused by improper storage design and the clean rebuild that resolved it.

The issue did not originate in vCenter itself, but lower in the stack at the ESXi
storage layer.

---

## Initial Symptoms

- Datastores were missing
- A 7.27 TB disk appeared as `MYDATA` with 0 B capacity
- VMFS creation was blocked
- vCenter Server deployment could not proceed

---

## Root Cause Analysis

The ESXi host was installed on the same 7 TB disk intended for VMFS storage.

Because ESXi does not allow VMFS creation on its own system disk:
- The datastore was unusable by design
- vCenter had nowhere to deploy
- The platform behaved exactly as designed

---

## Resolution Strategy

The environment was rebuilt with a correct disk layout:
- Dedicated system disk for ESXi
- Separate disk for VMFS datastore

---

## Results

✅ VMFS datastore created successfully  
✅ Datastores appeared correctly  
✅ vCenter deployed cleanly  
✅ Licensing applied  
✅ Environment stabilized  

---

## Key Lessons

- Storage design affects the entire VMware stack
- Not all failures originate at the application layer
- Rebuilding is sometimes the safest and fastest solution
- Understanding ESXi and VMFS behavior is critical
