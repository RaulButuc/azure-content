<properties 
	pageTitle="How to add a users to an elastic database pool" 
	description="You must add a user with privileges to each db in the pool" 
	metaKeywords="azure sql database elastic databases credentials" 
	services="sql-database" documentationCenter=""  
	manager="jeffreyg" 
	authors="ddove"/>

<tags 
	ms.service="sql-database" 
	ms.workload="sql-database" 
	ms.tgt_pltfrm="na" 
	ms.devlang="na" 
	ms.topic="article" 
	ms.date="11/03/2015" 
	ms.author="ddove; sidneyh" />

# How to add users to an Elastic Database pool

The **Elastic Database jobs** feature (preview) enables you to run a Transact-SQL script across a group of databases including custom-defined collection of databases, an **Elastic Database pool** or an **Elastic Database shard set** in Azure SQL Database. To run the script, a user with the appropriate permissions must be added to every database in which the job will execute. For more information, see [Managing Databases and Logins in Azure SQL Database](sql-database-manage-logins.md) or [Adding Users to Your SQL Azure Database](http://azure.microsoft.com/blog/2010/06/21/adding-users-to-your-sql-azure-database/)

## Prerequisites
* Install the [elastic job components](sql-database-elastic-jobs-service-installation.md). 

## How to add the users to the databases

1.	First connect to **master** of the Azure SQL Database server where the databases in your elastic database pool reside and create a new login using the same credentials provided when installing **elastic database jobs**.

		CREATE LOGIN login1 WITH password='<ProvidePassword>';

2. Log into each database in the pool and create a user using the same name and password. The user must have sufficient permissions to execute the job. This code must be run on each database.

		CREATE USER admin1 FROM LOGIN login1;
		
3. The user must have permissions as well, sufficient to execute the script specified for the job. Use the [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) to provide the user with the minimum required permissions for the script to execute succesfully. 

## Next steps

To create and manage jobs with the Azure portal, see [Creating and managing elastic database jobs](sql-database-elastic-jobs-create-and-manage.md). To create jobs with PowerShell, see [Create and manage a SQL Database elastic database jobs using PowerShell (preview)](sql-database-elastic-jobs-powershell.md)

[AZURE.INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-overview/elastic-jobs.png
<!--anchors-->

 