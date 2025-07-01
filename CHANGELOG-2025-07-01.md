Title: Deployment Process Improvements  
Date: 01/07/2025  

Added:  
- Support for deploying a dedicated instance, enabling more flexible environment setups  

Changed:  
- Streamlined the overall deployment workflow for clearer, faster releases  

Fixed:  
- Resolved a bug that could cause deployments to fail during instance creation  
- Corrected an issue where the Enter key action behaved unexpectedly during deployment commands  

Removed:  
- Deprecated “instance” flag from deployment commands, reducing configuration confusion

---
*Generated from PR #88: deployment instance*

**Source commits:**
- `41578ba` deployment instance by eff-kay
- `99e8e55` removed instance flag, fixed deployment bug by eff-kay
- `1655cd7` fixed enter by eff-kay

**Original PR:** https://github.com/slashml/magemaker/pull/88
