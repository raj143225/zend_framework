#### Production ########
*/15 * * * * php /var/www/my.rapidfunnel.com/public/cron/mailSendUser.php Production
*/15 * * * * php /var/www/my.rapidfunnel.com/public/cron/mailSendCampaign.php Production
*/15 * * * * php /var/www/my.rapidfunnel.com/public/cron/mailLogMailgun.php Production

1 0 * * * php /var/www/my.rapidfunnel.com/public/cron/accountIncentive.php Production
35 0 * * * php /var/www/my.rapidfunnel.com/public/cron/accountPayment.php Production
5 1 * * * php /var/www/my.rapidfunnel.com/public/cron/accountPrePayNotification.php Production
1 2 * * * php /var/www/my.rapidfunnel.com/public/cron/accountUserPayment.php Production
Remove cron for accountUserPrePayNotification
1 3 * * * php /var/www/my.rapidfunnel.com/public/cron/accountUserPrePayNotification.php Production
0 2 * * * php /var/www/my.rapidfunnel.com/public/cron/accountUserStatusUpdate.php Production



#### QA #######
*/10 * * * * php /var/www/qa1.rapidfunnel.com/public/cron/mailSendUser.php QA
*/10 * * * * php /var/www/qa1.rapidfunnel.com/public/cron/mailSendCampaign.php QA
*/10 * * * * php /var/www/qa1.rapidfunnel.com/public/cron/mailLogMailgun.php QA

1 4 * * * php /var/www/qa1.rapidfunnel.com/public/cron/accountIncentive.php QA
15 4 * * * php /var/www/qa1.rapidfunnel.com/public/cron/accountPayment.php QA
25 4 * * * php /var/www/qa1.rapidfunnel.com/public/cron/accountPrePayNotification.php QA
45 4 * * * php /var/www/qa1.rapidfunnel.com/public/cron/accountUserPayment.php QA
Remove cron for accountUserPrePayNotification
0 5 * * * php /var/www/qa1.rapidfunnel.com/public/cron/accountUserPrePayNotification.php QA
0 2 * * * php /var/www/qa1.rapidfunnel.com/public/cron/accountUserStatusUpdate.php QA


#### Staging ######
*/10 * * * * php /var/www/s1.rapidfunnel.com/public/cron/mailSendUser.php Staging
*/10 * * * * php /var/www/s1.rapidfunnel.com/public/cron/mailSendCampaign.php Staging
*/10 * * * * php /var/www/s1.rapidfunnel.com/public/cron/mailLogMailgun.php Staging

1 4 * * * php /var/www/s1.rapidfunnel.com/public/cron/accountIncentive.php Staging
10 4 * * * php /var/www/s1.rapidfunnel.com/public/cron/accountPayment.php Staging
[4:34:32 PM] rajanikant beero: 25 4 * * * php /var/www/s1.rapidfunnel.com/public/cron/accountPrePayNotification.php Staging
45 4 * * * php /var/www/s1.rapidfunnel.com/public/cron/accountUserPayment.php Staging
Remove cron for accountUserPrePayNotification
0 5 * * * php /var/www/s1.rapidfunnel.com/public/cron/accountUserPrePayNotification.php Staging
0 2 * * * php /var/www/s1.rapidfunnel.com/public/cron/accountUserStatusUpdate.php Staging
