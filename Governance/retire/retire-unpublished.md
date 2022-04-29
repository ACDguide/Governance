# Use case: unpublished data

This use case addresses the plethora of data that is associated with published data creation. That is, storage use including, but not limited to:

- Model configuration data
- Failed model run output
- Successful model run output
- Data prepared for collaborative sharing but not publication/DOI
- Intermediate data products

How each of these scenarios is handled will typically be determined on a project basis, with a view to the importance of **reproducibility** and considering relative **compute or storage costs**.

## Suggested procedures

**If compute is readily available but storage is limited**

1. Maintain a database or wiki of model runs
2. Create zip archives of model configurationsand move to slow access tape storage if they are required to be kept for reproducibility 
3. If model run failed, remove data immediately
4. If model run was successful and post-processing has been completed (and if bit-reproducibility across systems is not a concern), then data can be removed, perhaps after an initial quarantine period for data validation
5. Intermediate data products and collaborative data can be retired at the end of their active projects, following a quaratine period

5a. Some intermediate data may not have a logical project end, such as regridded CMIP data - such data might follow a similar approach as the replciated data use case.

**If compute is limited but deep storage is readily available**

Repeat steps 1-3 as above.

4. Following post-processing and validation, or at project close, data should be tarred and trasnferred to a deep storage system
