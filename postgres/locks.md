https://stackoverflow.com/questions/46303951/how-to-debug-sharelock-in-postgres



### 1. ShareLock

```
ERROR:  deadlock detected
DETAIL:  Process 15136 waits for ShareLock on transaction 579932427; blocked by process 21885.
Process 21885 waits for ShareLock on transaction 579932412; blocked by process 15136.
HINT:  See server log for query details.
CONTEXT:  while updating tuple (4772,1) in relation "driver"
SQL statement "UPDATE FLEETDRIVER.DRIVER
        SET STREAKS_JSONB = v_return
        WHERE CLIENTID = p_clientid
                AND FLEETID = v_fleetId
                AND DRIVERID = v_driverId"
PL/pgSQL function calculate_driver_streak(character varying,jsonb) line 391 at SQL statement
SQL statement "SELECT fleetdriver.calculate_driver_streak(
                p_clientid,
                JSONB_BUILD_OBJECT(
                        'fleetId', v_driverRecord.FLEETID,
                        'driverId', v_driverRecord.DRIVERID
                ))"
PL/pgSQL function fleetdriver.process_driver_streak() line 85 at SQL statement

```

