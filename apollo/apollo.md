## summarize

 1. [apollo](https://github.com/ctripcorp/apollo)
    背景，携程apollo一些运维脚本
    
 2.  删除ApolloPortalDB 中无用的AppId
 
    (```)
     set @appId = 'bb';     
     Use `ApolloPortalDB`;     
     update `App` set `IsDeleted` = 1 where `AppId` = @appId and `IsDeleted` = 0;  
     update `AppNamespace` set `IsDeleted` = 1 where `AppId` = @appId and `IsDeleted` = 0;  
     update `Favorite` set `IsDeleted` = 1 where `AppId` = @appId and `IsDeleted` = 0;  
     
     # handle roles and permissions  
     create temporary table `PermissionIds` as select `Id` from `Permission` where (`TargetId` = @appId or `TargetId` like CONCAT(@appId, '+%'))  and `IsDeleted` = 0;  
     update `Permission` set `IsDeleted` = 1 where `Id` in (select `Id` from `PermissionIds`);  
     update `RolePermission` set `IsDeleted` = 1 where `PermissionId` in (select `Id` from `PermissionIds`);  
     drop temporary table `PermissionIds`;  
     
     create temporary table `RoleIds` as select `Id` from `Role` where (`RoleName` = CONCAT('Master+', @appId) or `RoleName` like CONCAT('ModifyNamespace+', @appId, '+%') or `RoleName` like CONCAT('ReleaseNamespace+', @appId, '+%')) and `IsDeleted` = 0;  
     update `Role` set `IsDeleted` = 1 where `Id` in (select `Id` from `RoleIds`);  
     update `UserRole` set `IsDeleted` = 1 where `RoleId` in (select `Id` from `RoleIds`);  
     update `ConsumerRole` set `IsDeleted` = 1 where `RoleId` in (select `Id` from `RoleIds`);  
     drop temporary table `RoleIds`;  
    (```) 
      
 3. 删除ApolloConfigDB中的无用AppId   
 
 
     set @appId = '90000000';     
     Use `ApolloConfigDB`;  
     
     update `App` set `IsDeleted` = 1 where `AppId` = @appId and `IsDeleted` = 0;  
     update `AppNamespace` set `IsDeleted` = 1 where `AppId` = @appId and `IsDeleted` = 0;  
     update `Cluster` set `IsDeleted` = 1 where `AppId` = @appId and `IsDeleted` = 0;  
     update `Commit` set `IsDeleted` = 1 where `AppId` = @appId and `IsDeleted` = 0;  
     update `GrayReleaseRule` set `IsDeleted` = 1 where `AppId` = @appId and `IsDeleted` = 0;  
     update `Release` set `IsDeleted` = 1 where `AppId` = @appId and `IsDeleted` = 0;  
     update `ReleaseHistory` set `IsDeleted` = 1 where `AppId` = @appId and `IsDeleted` = 0;  
     delete from `Instance` where `AppId` = @appId;  
     delete from `InstanceConfig` where `ConfigAppId` = @appId;  
     delete from `ReleaseMessage` where `Message` like CONCAT(@appId, '+%');  
     
     # handle namespaces and items  
     create temporary table `NamespaceIds` as select `Id` from `Namespace` where `AppId` = @appId and `IsDeleted` = 0;  
     update `Namespace` set `IsDeleted` = 1 where `Id` in (select `Id` from `NamespaceIds`);  
     update `Item` set `IsDeleted` = 1 where `NamespaceId` in (select `Id` from `NamespaceIds`);  
     delete from `NamespaceLock` where `NamespaceId` in (select `Id` from `NamespaceIds`);  
     drop temporary table `NamespaceIds`;    
       
 4. ApolloPortalDB中替换账号
     
     
     set @olduser = 'zhangsan@**.com';
     set @newuser = 'zhangsan@**.com';
     
     USE   `apolloportaldb`;
     
     update `users`  set `Username`  = @newuser, `Email` =@newuser where `Username`  = @olduser;
     
     update `userrole`  set `UserId`  =@newuser where `UserId` =@olduser;
     update `userrole` set `DataChange_CreatedBy`  = @newuser where `DataChange_CreatedBy`  = @olduser;
     update `userrole` set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  =@olduser;
     
     update `authorities`  set `username`  = @newuser where `username`  = @olduser;
     
     update `role`  set `DataChange_CreatedBy` =@newuser  where `DataChange_CreatedBy` =@olduser;
     update `role`  set `DataChange_LastModifiedBy` =@newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     
     update `rolepermission`  set `DataChange_CreatedBy` =@newuser where `DataChange_CreatedBy`  = @olduser;
     update `rolepermission`  set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     update `permission`  set `DataChange_CreatedBy` =@newuser where `DataChange_CreatedBy`  = @olduser;
     update `permission`  set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     update `favorite`  set `UserId`  = @newuser where `UserId`  =@olduser;
     update `favorite`  set `DataChange_CreatedBy` = @newuser where `DataChange_CreatedBy`  = @olduser;
     update `favorite`  set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     
     update `app`  set `OwnerName`  = @newuser where `OwnerName`  = @olduser;
     update `app`  set `OwnerEmail`  = @newuser where `OwnerEmail`  = @olduser;
     update `app`  set `DataChange_CreatedBy`  = @newuser where `DataChange_CreatedBy`  = @olduser;
     update `app`  set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     update `appnamespace`  set `DataChange_CreatedBy`  =@newuser where `DataChange_CreatedBy`  = @olduser;
     update `appnamespace`  set `DataChange_LastModifiedBy` = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     
     USE  `bingo`;
     update `members`  set `email`  = @newuser where `email`  = @olduser;  
     
     
 5. ApolloConfig中替换账号
    
    
     set @olduser = 'zhangsi@shouqiaba.com';
     set @newuser = 'zhangsi@shouqianba.com';
     
     
     USE   `apolloconfigdb`;
     
     
     update `app`  set `OwnerName`  = @newuser where `OwnerName`  = @olduser;
     update `app`  set `OwnerEmail`  = @newuser where `OwnerEmail`  = @olduser;
     update `app`  set `DataChange_CreatedBy`  = @newuser where `DataChange_CreatedBy`  = @olduser;
     update `app`  set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     
     update `appnamespace`  set `DataChange_CreatedBy`  =@newuser where `DataChange_CreatedBy`  = @olduser;
     update `appnamespace`  set `DataChange_LastModifiedBy` = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     
     update `audit`  set `DataChange_CreatedBy`  = @newuser where `DataChange_CreatedBy`  = @olduser;
     update `audit`  set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     update `cluster`  set `DataChange_CreatedBy`  = @newuser where `DataChange_CreatedBy`  = @olduser;
     update `cluster`  set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     
     update `commit`  set `DataChange_CreatedBy`  = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     update `commit`  set `DataChange_LastModifiedBy` =@newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     update `item`  set `DataChange_CreatedBy`  =@newuser where `DataChange_CreatedBy`  =@olduser;
     update `item`  set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @olduser;
     
     update `namespace`  set `DataChange_CreatedBy`  = @newuser where `DataChange_CreatedBy`  = @olduser;
     update `namespace`  set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @newuser;
     
     
     update `release`   set `DataChange_CreatedBy`  = @newuser where `DataChange_CreatedBy`  = @olduser;
     update `release`   set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @newuser;
     
     update `releasehistory`   set `DataChange_CreatedBy`  = @newuser where `DataChange_CreatedBy`  = @olduser;
     update `releasehistory`   set `DataChange_LastModifiedBy`  = @newuser where `DataChange_LastModifiedBy`  = @newuser;
    
    