#Roles
in database admin => in system application admin (AA)
in database support-admin => in system support admin (SA)
in database account-admin => in system account admin (Admin)

#CRON setup guide
Cron files are inside public/cron directory
"cronConfig.php" is the cron configuration file. DON'T set this as cron.
In "cronConfig.php" line 3-4 set the include path to have zend library.

In "lib/RapidFunnel/Config/app.ini" set timezone according to environment.
For Ex: set timezone for
QA server inside the block "[QA-account-payment : QA]" ,
Staging server inside the block "[Staging-account-payment : Staging]" , so on..

Now need to set with environment like
"php public/cron/accountPayment.php QA"

#CRON Account Incentive:
@description: It is to calculate the incentives for the account users based on the opt in contact(leads) generated
It should run on start of every day. Hence it will calculate the incentives of users of the previous days,
if the "leadsGenerated" column of the "account incentive" table is not updated.
To Run Use:
php PATH-TO-PROJECT-FOLDER/public/cron/accountIncentive.php ENVIRONMENT
