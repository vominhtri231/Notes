![](https://lh3.googleusercontent.com/pw/ACtC-3c8PCw1dmEL8oClOV-1WU3czLlsRsvoO_9h6NdNuQ6z5WGeS9p0iPycOycNaXgA-hytnZTftlpf25LwZlBIPKaSNSmPHGUg2Ke4R-ievEGgcz-JErdWNQVi2QVDV9hmSJ7sG8TFF6P8UxGesCRr-vEk=w1050-h623-no)

### When DML code run:
1. The data is both load to buffer cache and saved in undo segments. Data in undo segments is kept unchanged and used for:
    1. Rollback operation
    2. Provide read consistency
    3. Flashback operation
2. Lock all related blocks
3. The changes are written to the redo log buffer first, then to the buffer cache for data consistency (Write-ahead Logging)
4. Server returns the feedback
### When user commit
1. A commit log record is created
2. Log writer process writes all related log to redo log files (including the commit log)
3. The database writer process writes the dirty blocks to the dish and free up undo segments.
4. Unlock related blocks
5. Server returns the feedback
