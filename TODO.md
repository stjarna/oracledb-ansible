# TODO
- Get rid of TASK [prepare-oracle-env : Install required libraries] ************************************************************************************************************************************************************************************************************************************************************************
[DEPRECATION WARNING]: Invoking "yum" only once while using a loop via squash_actions is deprecated. Instead of using a loop to supply multiple items and specifying `name: {{ item }}`, please use `name: u'{{ packages_list }}'` and remove the loop. This feature will be removed in version 2.11. Deprecation warnings can
 be disabled by setting deprecation_warnings=False in ansible.cfg.
- Amend readme
- Rename name of project to ansible-oracle

sqlplus sys as sysdba (password=oracle)

sqlplus "sys/password@database as sysdba"
sqlplus sys/oracle@ORCL as sysdba