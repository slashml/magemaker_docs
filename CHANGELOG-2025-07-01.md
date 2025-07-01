Title: Streamlined Deployment Instance Handling  
Date: 01/07/2025  

Added:  
- Support for deploying to specific instances, giving teams finer control over rollout targets  

Changed:  
- Deployment workflow now auto-detects the target instance, removing the need for manual flags  

Fixed:  
- Resolved a deployment failure that occurred when an instance flag was not provided  

Removed:  
- Deprecated the --instance flag from deployment commands, simplifying the deployment configuration

---
*Generated from PR #88: deployment instance*

**Source commits:**
- `41578ba` deployment instance by eff-kay
- `99e8e55` removed instance flag, fixed deployment bug by eff-kay

**Original PR:** https://github.com/slashml/magemaker/pull/88
