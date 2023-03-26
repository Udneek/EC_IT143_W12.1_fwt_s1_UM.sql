# EC_IT143_W12.1_fwt_s1_UM.sql

/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s1_UM.sql
PURPOSE: Fun with Triggers--- Start with a question.  How to keep track of when a record was last modified?

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
-- Q1: How to keep track of when a record was last modified?



/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s2_UM.sql
PURPOSE: Fun with Triggers--- Create an answer

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
-- Q1: Let's query the database for an answer.






/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s3_UM.sql
PURPOSE: Fun with Triggers--- Research and test a solution:

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
--- We can use an after-update trigger to update the "DateModified" column whenever a record is updated.

    




/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s4_UM.sql
PURPOSE: Fun with Triggers--- Create an after-update trigger.

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
--- We can use an after-update trigger to update the "DateModified" column whenever a record is updated.

    CREATE TRIGGER trgAfterUpdate_t_w3_schools_customers
    ON [dbo].[t_w3_schools_customers]
    AFTER UPDATE
   AS
BEGIN
    UPDATE [dbo].[t_w3_schools_customers]
    SET DateModified = GETDATE()
    WHERE CustomerID IN (SELECT CustomerID FROM inserted)
END




/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s5_UM.sql
PURPOSE: Fun with Triggers--- Test results to see if they are as expected.

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
--- We can test the trigger by updating a record in the [dbo].[t_w3_schools_customers] table and checking 
--- if the "DateModified" column is updated with the current date and time.




/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s6_UM.sql
PURPOSE: Fun with Triggers--- Ask the next question.

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
Q2: How to keep track of who last modified a record?




/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s1_UM.sql
PURPOSE: Fun with Triggers--- Ask the next question. How to keep track of who last modified a record?

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
Q2: How to keep track of who last modified a record?




/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s2_UM.sql
PURPOSE: Fun with Triggers--- Create an answer.

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
--- Let's query the database for the answer.




/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s3_UM.sql
PURPOSE: Fun with Triggers--- Research and test a solution.

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
--- We can create an after-update trigger that will capture the user who last modified the record:




/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s4_UM.sql
PURPOSE: Fun with Triggers--- Create an after-update trigger.

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
--- We can create an after-update trigger that will capture the user who last modified the record and test it against the database:

        CREATE TRIGGER tr_Customer_Modified
        ON [dbo].[t_w3_schools_customers]
    AFTER UPDATE
    AS
    BEGIN
        SET NOCOUNT ON;

    UPDATE [dbo].[t_w3_schools_customers]
        SET [Date modified] = GETDATE(),
      [Modified by] = SYSTEM_USER;
        FROM [dbo].[t_w3_schools_customers] c
        INNER JOIN inserted i ON c.CustomerID = i.CustomerID;
END


        
        
        
/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s5_UM.sql
PURPOSE: Fun with Triggers--- Test results to see if they are as expected.

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
--- To test the trigger, we can update a record in the [dbo].[t_w3_schools_customers] table and then check the 
--- values in the [Date modified] and [Modified by] columns:

       UPDATE [dbo].[t_w3_schools_customers]
      SET [CustomerName] = 'New Customer Name'
        WHERE [CustomerID] = 1;
        
--- After running this update statement, we can check the [Date modified] and [Modified by] columns for the updated record:

      SELECT [CustomerName], [Date modified], [Modified by]
      FROM [dbo].[t_w3_schools_customers]
      WHERE [CustomerID] = 1;
      
      
      
/*****************************************************************************************************************
NAME:    My Script Name   EC_IT143_W2.1_fwt_s6_UM.sql
PURPOSE: Fun with Triggers--- Ask the next question

MODIFICATION LOG:
Ver      Date        Author        Description
-----   ----------   -----------   -------------------------------------------------------------------------------
1.0     03/24/2023   Uduak Mbaba       1. Built this script for EC IT143


RUNTIME: 
Xm Xs

NOTES:This script is for T-SQL Data Manipulation - Fun with Triggers  

*****************************************************************************************************************
--- Ask the next question.


