# DNPR Package

This package provides very useful data manipulation features for JSON Objects in Python platform. Using this anyone can perform the following operations -

### Functions

## Distinct of JSON Payloads

As of now, no available package in Python, which can operate on JSON Payloads & to provide unique Payload based on the total number of supplied fields in it. Using this distinct function - you can eliminate that. This is specially useful for NoSQL databases, where distinct might be a challange due to distributed nature of the architecture.

> You need to use the following pattern to invoke this function:
>

    distinct(Input Json, Output Json)
	
> Where Input Json is your supplied JSON & Output will be the unique JSON output.

## NVL To check a specific fields NULL Value & replaced with any supplied default value in the JSON Payloads

Keeping a specific business logic in mind, this NVL function will check if there is any NULL value or empty string & based on the business logic it will replace that with the default supplied value as per business logic.

> You need to use the following pattern to invoke this function:
>
	
    nvl(Input Json, Prospective Null Column Name, Dafult Value in case of Null, Output Json)
	
> Where Input Json is your supplied JSON, You have to provide the complete/full column name as per JSON structure, Default Value will be supplied value that you want to replace your null or empty string & Output will be the unique JSON output.

## Use of Partition By clause with the specific fields of JSON Payloads

Partition by would be another place where you can manipulate your JSON data just like any SQL queries.

> You need to use the following pattern to invoke this function:
>
	
    partition_by(Input Json, Group By Column List, Group By Operation, Candidate Column Name, Output Column Name, Output Json)
	
> Where Input JSON is your supplied JSON. Also, you need to provide the group of column list, which will be part of your partition window. Again, you need to provide complete/full column name. Then you need to mention what kind of operation that you want to perform. It can be MAX/MIN/SUM/AVG. Then you need to mention - on what column you want to perform the aggregate in Candidate Column Name field. Output Column name by default is NULL. However, you can provide a different name for aggregate column. In that case, your output JSON doesn't contain the old column name & it will contain this new column name. But, make sure you are using the same path for this new column. 

## Use of Regular Expression with the specific fields of JSON Payloads

And, finally, we've introduced these following regular expression function on JSON, which I think will be very handy.

> You need to use the following pattern to invoke this function:
>
	
    regex_like(Input Json, Target Column, Pattern To Match, Output Json)
	regex_replace(Input Json, Target Column, Pattern to Replace, Output Json)
	regex_substr(Input Json, Target Column, Pattern to substring, Output Json)
	
> From the above function, the parameters are self explanatory. For details, please refer the examples.

------------------------------------------------------------------------------------------
                         callJson_DNPR.py
------------------------------------------------------------------------------------------

    ##############################################
    #### Written By: SATYAKI DE               ####
    #### Written On: 08-Sep-2019              ####
    ####                                      ####
    #### Objective: Main calling scripts.     ####
    ##############################################
    
    from dnpr.clsDnpr import clsDnpr
    import datetime as dt
    import json
    
    # Disbling Warning
    def warn(*args, **kwargs):
        pass
    
    import warnings
    warnings.warn = warn
    
    # Lookup functions from
    
    
    def main():
        try:
            srcJson = [
                        {"FirstName": "Satyaki", "LastName": "De", "Sal": 1000},
                        {"FirstName": "Satyaki", "LastName": "De", "Sal": 1000},
                        {"FirstName": "Archi", "LastName": "Bose", "Sal": 500},
                        {"FirstName": "Archi", "LastName": "Bose", "Sal": 7000},
                        {"FirstName": "Deb", "LastName": "Sen", "Sal": 9500}
                      ]

            print("=" * 157)
            print("Checking distinct function!")
            print("=" * 157)
            print()
    
            print("*" * 157)
            print("Input Data: ")
            srcJsonFormat = json.dumps(srcJson, indent=1)
            print(str(srcJsonFormat))
            print("*" * 157)
    
            # Initializing the class
            t = clsDnpr()
    
            print("1. Checking distinct functionality!")
    
            var1 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("Start Time: ", str(var1))
    
            # Invoking the distinct function
            tarJson = t.distinct(srcJson)
    
            print("*" * 157)
            print("Output Data: ")
            tarJsonFormat = json.dumps(tarJson, indent=1)
            print(str(tarJsonFormat))
            print("*" * 157)
    
            if not tarJson:
                print()
                print("No relevant output data!")
                print("*" * 157)
            else:
                print()
                print("Relevant output data comes!")
                print("*" * 157)
    
            var2 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("End Time: ", str(var2))
    
            print("=" * 157)
            print("End of distinct function!")
            print("=" * 157)
    
            print("2. Checking nvl functionality!")
    
            srcJson_1 = [
                {"FirstName": "Satyaki", "LastName": "", "Sal": 1000},
                {"FirstName": "Archi", "LastName": "Bose", "Sal": 500},
                {"FirstName": "Deb", "LastName": "", "Sal": 9500}
            ]
    
            var3 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("Start Time: ", str(var3))
    
            strDef = 'FNU'
            print("Default Value: ", strDef)
            srcColName = 'LastName'
            print('Candidate Column for NVL: ', srcColName)
    
            # Invoking the nvl function
            tarJson_1 = t.nvl(srcJson_1, srcColName, strDef)
    
            print("*" * 157)
            print("Output Data: ")
            tarJsonFormat_1 = json.dumps(tarJson_1, indent=1)
            print(str(tarJsonFormat_1))
            print("*" * 157)
    
            if not tarJson_1:
                print()
                print("No relevant output data!")
                print("*" * 157)
            else:
                print()
                print("Relevant output data comes!")
                print("*" * 157)
    
            var4 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("End Time: ", str(var4))
    
            print("=" * 157)
            print("End of nvl function!")
            print("=" * 157)
    
            print("3. Checking partition-by functionality!")
    
            srcJson_2 = [
                {"FirstName": "Satyaki", "LastName": "", "Location":"Sunnyvale", "Sal": 1000},
                {"FirstName": "Satyaki", "LastName": "", "Location":"Sunnyvale", "Sal": 700},
                {"FirstName": "Archi", "LastName": "Bose", "Location":"San Ramon", "Sal": 500},
                {"FirstName": "Deb", "LastName": "", "Location":"Palo Alto", "Sal": 9500},
                {"FirstName": "Archi", "LastName": "Bose", "Location":"Freemont", "Sal": 4500}
            ]
    
            var5 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("Start Time: ", str(var5))
    
            GrList = ['FirstName', 'LastName']
            print("Partition By Columns::: ", str(GrList))
            grOperation = 'Max'
            print('Operation toe be performed: ', grOperation)
            strCandidateColumnName = 'Sal'
            print('Column Name on which the aggregate function will take place: ', strCandidateColumnName)
    
            # Invoking the partition by function - MAX
            tarJson_1 = t.partitionBy(srcJson_2, GrList, grOperation, strCandidateColumnName)
    
            print("*" * 157)
            print("Output Data: ")
            tarJsonFormat_1 = json.dumps(tarJson_1, indent=1)
            print(str(tarJsonFormat_1))
            print("*" * 157)
    
            if not tarJson_1:
                print()
                print("No relevant output data!")
                print("*" * 157)
            else:
                print()
                print("Relevant output data comes!")
                print("*" * 157)
    
            var6 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("End Time: ", str(var6))
    
            var7 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("Start Time: ", str(var7))
    
            grOperation_1 = 'Min'
            print('Operation toe be performed: ', grOperation_1)
    
            # Invoking the Partition By function - MIN
            tarJson_2 = t.partitionBy(srcJson_2, GrList, grOperation_1, strCandidateColumnName)
    
            print("*" * 157)
            print("Output Data: ")
            tarJsonFormat_2 = json.dumps(tarJson_2, indent=1)
            print(str(tarJsonFormat_2))
            print("*" * 157)
    
            if not tarJson_2:
                print()
                print("No relevant output data!")
                print("*" * 157)
            else:
                print()
                print("Relevant output data comes!")
                print("*" * 157)
    
            var8 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("End Time: ", str(var8))
    
            var9 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("Start Time: ", str(var9))
    
            grOperation_2 = 'Avg'
            print('Operation toe be performed: ', grOperation_2)
    
            # Invoking the Partition By function - Avg
            tarJson_3 = t.partitionBy(srcJson_2, GrList, grOperation_2, strCandidateColumnName)
     
            print("*" * 157)
            print("Output Data: ")
            tarJsonFormat_3 = json.dumps(tarJson_3, indent=1)
            print(str(tarJsonFormat_3))
            print("*" * 157)
    
            if not tarJson_3:
                print()
                print("No relevant output data!")
                print("*" * 157)
            else:
                print()
                print("Relevant output data comes!")
                print("*" * 157)
    
            var10 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("End Time: ", str(var10))
    
            var11 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("Start Time: ", str(var11))
    
            grOperation_3 = 'Sum'
            print('Operation toe be performed: ', grOperation_3)
    
            # Invoking the Partition By function - Sum
            tarJson_4 = t.partitionBy(srcJson_2, GrList, grOperation_3, strCandidateColumnName)
    
            print("*" * 157)
            print("Output Data: ")
            tarJsonFormat_4 = json.dumps(tarJson_4, indent=1)
            print(str(tarJsonFormat_4))
            print("*" * 157)
    
            if not tarJson_4:
                print()
                print("No relevant output data!")
                print("*" * 157)
            else:
                print()
                print("Relevant output data comes!")
                print("*" * 157)
    
            var12 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("End Time: ", str(var12))
    
            print("=" * 157)
            print("End of partition function!")
            print("=" * 157)
    
            print("4. Checking regular expression functionality!")
            print()
    
            var13 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("Start Time: ", str(var13))
    
            print('::Function Regex_Like:: ')
            print()
    
            tarColumn = 'FirstName'
            print('Target Column for Rexex_Like: ', tarColumn)
            inpPattern = r"\bSa"
            print('Input Pattern: ', str(inpPattern))
    
            # Invoking the regex_like function
            tarJson = t.regex_like(srcJson, tarColumn, inpPattern)
    
            print('End of Function Regex_Like!')
            print()
    
            print("*" * 157)
            print("Output Data: ")
            tarJsonFormat = json.dumps(tarJson, indent=1)
            print(str(tarJsonFormat))
            print("*" * 157)
    
            if not tarJson:
                print()
                print("No relevant output data!")
                print("*" * 157)
            else:
                print()
                print("Relevant output data comes!")
                print("*" * 157)
    
            var14 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("End Time: ", str(var14))
    
            var15 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("Start Time: ", str(var15))
    
            print('::Function Regex_Replace:: ')
            print()
    
            tarColumn = 'FirstName'
            print('Target Column for Rexex_Replace: ', tarColumn)
            inpPattern = r"\bSa"
            print('Input Pattern: ', str(inpPattern))
            replaceString = 'Ka'
            print('Replacing Character: ', replaceString)
    
            # Invoking the regex_replace function
            tarJson = t.regex_replace(srcJson, tarColumn, inpPattern, replaceString)
    
            print('End of Function Rexex_Replace!')
            print()
    
            print("*" * 157)
            print("Output Data: ")
            tarJsonFormat = json.dumps(tarJson, indent=1)
            print(str(tarJsonFormat))
            print("*" * 157)
    
            if not tarJson:
                print()
                print("No relevant output data!")
                print("*" * 157)
            else:
                print()
                print("Relevant output data comes!")
                print("*" * 157)
    
            var16 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("End Time: ", str(var16)) 
    
            var17 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("Start Time: ", str(var17))
    
            print('::Function Regex_Substr:: ')
            print()
    
            tarColumn = 'FirstName'
            print('Target Column for Regex_Substr: ', tarColumn)
            inpPattern = r"\bSa"
            print('Input Pattern: ', str(inpPattern))
    
            # Invoking the regex_substr function
            tarJson = t.regex_substr(srcJson, tarColumn, inpPattern)
    
            print('End of Function Regex_Substr!')
            print()
    
            print("*" * 157)
            print("Output Data: ")
            tarJsonFormat = json.dumps(tarJson, indent=1)
            print(str(tarJsonFormat))
            print("*" * 157)
    
            if not tarJson:
                print()
                print("No relevant output data!")
                print("*" * 157)
            else:
                print()
                print("Relevant output data comes!")
                print("*" * 157)
    
            var18 = dt.datetime.now().strftime("%Y-%m-%d %H-%M-%S")
            print("End Time: ", str(var18))
    
            print("=" * 157)
            print("End of regular expression function!")
            print("=" * 157)
    
    
        except ValueError:
            print("No relevant data to proceed!")
    
        except Exception as e:
            print("Top level Error: args:{0}, message{1}".format(e.args, e.message))
    
    if __name__ == "__main__":
        main()
    
		
------------------------------------------------------------------------------------------
                 End Of Sample Code - callJson_DNPR.py
------------------------------------------------------------------------------------------

> Bug Fix: Let me know - if you face any bug. This is first release.
>
> Fixed: Partition By Bug!
>
> Notification: Distinct will only work simple JSON payload. We're working on to bring the 
> same feature for complex JSON as well.
>
> Dependancy Package: You need to install followig packages in order to run this package -
>
>                     pip install pandas
>                     pip install regex
------------------------------------------------------------------------------------------
    Directory Structure shoould be like ->
------------------------------------------------------------------------------------------
    -> \callJson_DNPR.py
------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------
