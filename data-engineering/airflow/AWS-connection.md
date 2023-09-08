
**[AWS S3]**

Considering that the current Jenkins instance is located in the BTS account and in general, the S3 buckets and other services are located in the main account, we might face some issues handling the connection between accounts.  
  
The Forecasting Team has been doing some exploration but hasn’t found a solution to maintain the connection for large run periods.  
  
**Resources**

-   [![](https://cdn.sstatic.net/Sites/stackoverflow/Img/favicon.ico?v=ec617d715196)How to setup S3 connection using .env variables in Airflow using Docker?](https://stackoverflow.com/questions/68826336/how-to-setup-s3-connection-using-env-variables-in-airflow-using-docker)
-   [![](https://airflow.apache.org/docs/apache-airflow-providers-amazon/stable/_static/pin_32.png)Amazon Web Services Connection — apache-airflow-providers-amazon Documentation](https://airflow.apache.org/docs/apache-airflow-providers-amazon/stable/connections/aws.html)
	- https://github.com/apache/airflow/pull/21778/files
-   Explored alternatives by Forecasting Team ([Slack conversation](https://glovo.slack.com/archives/C03H5SYGS3F/p1663755969378379 "https://glovo.slack.com/archives/C03H5SYGS3F/p1663755969378379")) 
	- [Handover Doc](https://arrow-icicle-748.notion.site/Handover-Doc-5d01159b48474d49ab9da9ad5ae06551)
- [Sourcing credentials with an external process](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sourcing-external.html)
- [How to refresh the boto3 credetials when python script is running indefinitely](https://stackoverflow.com/questions/63724485/how-to-refresh-the-boto3-credetials-when-python-script-is-running-indefinitely)
