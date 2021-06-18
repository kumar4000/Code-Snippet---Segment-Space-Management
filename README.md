# Code-Snippet---Segment-Space-Management
Segment Space Management

The package pkg_Segment_Space_Cleanup is created to perform Segment Space management on all types of Tablespaces within the Oracle Database.

**Pre-requisite:** The requirement is to create a DBA user with the database and it should have the DBA role provided (SCBDBA as mentioned in the snippet)

**Temporary Tables:** MOVE_SEGMENTS_STG - Staging table to capture the segments information
                      MOVE_SEG_SPACE_ERR - Staging table to capture the error information
                   PROC_START_END_TBL - Staging table to track the stages of the procedure call within the package

**Package:** pkg_Segment_Space_Cleanup - Package to cleanup the datafile as per the size we need to shrink

The below procedures within the package are to perform various tasks that are required for segment space management.

          PROCEDURE sp_Populate_Stg_Tbl (p_Block_Size NUMBER, p_File_Id NUMBER, p_Resize_Size NUMBER);
  
          PROCEDURE sp_Stmt_Generate (p_tbl_tblspace VARCHAR2, p_indx_tblspace VARCHAR2,p_lob_tblspace VARCHAR2);
  
          PROCEDURE sp_Row_Enable;
  
          PROCEDURE sp_Row_Disable;
	  
          PROCEDURE sp_Move_Tbl(p_index_tblspace VARCHAR2, p_index_status VARCHAR2);
  
          PROCEDURE sp_Rebuild_Indexes;
  
          PROCEDURE sp_Move_Lobs;
  
          PROCEDURE sp_Unusable_Indexes(p_owner VARCHAR2, p_index_status VARCHAR2);

**Procedure:**  The procedure sp_Cleandata_log is to call the package and pass the arguments to perform various steps. The sample call for the procedure is as below:

begin
   scbdba.sp_Cleandata_log ('sp_Populate_Stg_Tbl','SCHEMANAME','8192','4','0','SCHEMANAME_DATA','SCHEMANAME_INDX','SCHEMANAME_LOB','UNUSABLE');
   scbdba.sp_Cleandata_log ('sp_Stmt_Generate','SCHEMANAME','8192','4','0','SCHEMANAME_DATA','SCHEMANAME_INDX','SCHEMANAME_LOB','UNUSABLE');
   scbdba.sp_Cleandata_log ('sp_Row_Enable','SCHEMANAME','8192','4','0','SCHEMANAME_DATA','SCHEMANAME_INDX','SCHEMANAME_LOB','UNUSABLE');
   scbdba.sp_Cleandata_log ('sp_Move_Tbl','SCHEMANAME','8192','4','0','SCHEMANAME_DATA','SCHEMANAME_INDX','SCHEMANAME_LOB','UNUSABLE');
   scbdba.sp_Cleandata_log ('sp_Row_Disable','SCHEMANAME','8192','4','0','SCHEMANAME_DATA','SCHEMANAME_INDX','SCHEMANAME_LOB','UNUSABLE');
   scbdba.sp_Cleandata_log ('sp_Move_Lobs','SCHEMANAME','8192','4','0','SCHEMANAME_DATA','SCHEMANAME_INDX','SCHEMANAME_LOB','UNUSABLE');
   scbdba.sp_Cleandata_log ('sp_Move_Lobs','SCHEMANAME','8192','4','0','SCHEMANAME_DATA','SCHEMANAME_INDX','SCHEMANAME_LOB','UNUSABLE');
end;
/
              

