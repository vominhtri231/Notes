* Pluggable database (PDB) is introduced from Oracle 12c. It is a collection of portable schemas and objects 
  that appear to clients as a separate database. DBA_PDBS will list the pluggable databases.

* PDBs can be plugged/unplugged from the container database(CDB). Each CDB contains:
    1. Zero or more PDBs
    2. Exactly one CDB$ROOT, the keeper of all PDBs.
    3. Exactly one PDB$SEED, a template from which new PDB can be created. User can not modify/ add objects in the seed.
       ![](http://logicalread.com/wp-content/uploads/2014/11/fig1-15.jpg)

  See more at [oracle side](https://docs.oracle.com/database/121/CNCPT/cdbovrvw.htm#CNCPT89235)
