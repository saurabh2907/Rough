BEGIN
   DBMS_SCHEDULER.create_job (
      job_name        => 'daily_rider_prem_job',
      job_type        => 'STORED_PROCEDURE',
      job_action      => 'Daily_RiderPrem',
      start_date      => TRUNC(SYSDATE) + 9/24,  -- sets start at 9 AM today (or tomorrow if current time > 9 AM)
      repeat_interval => 'FREQ=DAILY; BYHOUR=9; BYMINUTE=0; BYSECOND=0',
      enabled         => TRUE,
      auto_drop       => FALSE,
      comments        => 'Job to run the Daily_RiderPrem procedure every day at 9 AM'
   );
END;
