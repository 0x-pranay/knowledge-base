### Setting up cron job in aws aurora 

https://aws.amazon.com/blogs/database/schedule-jobs-with-pg_cron-on-your-amazon-rds-for-postgresql-or-amazon-aurora-for-postgresql-databases/



### common queries



SELECT * FROM pg_extension WHERE extname = 'pg_cron';



SELECT * FROM cron.job;



SELECT * FROM cron.job_run_details