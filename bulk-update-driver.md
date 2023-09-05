```
line 15 at SQL statement", "message: ": "numeric field overflow",



 Error in saving Trip data {"context: ": "SQL statement \"INSERT INTO TRIP \n (ENDPOINTVERSION,FLEETID,DRIVERID,TRIPID,CLIENTID,\n DEVICE,ASSET,DRIVERNAME,ASSETID,\n ONGOING,IGNITIONID,IGNITIONTRIPINDEX,\n TIMEZONEID,TIMEZONEOFFSET,\n TRIPDISTANCE, TRIPDURATION,\n DRIVERASSIGNED,DIDSTARTTRIPAUTOMATICALLY,DVRCONSENT,\n EDVRCONSENT, \n FIRSTLOCATION,LASTLOCATION,LASTKNOWNLOCATION,\n\t\t CAMERASERIALID,\n STATUSUPDATETIMESTAMP,MULTISTREAMENABLED,\n STARTTIMEUTC,ENDTIMEUTC,\n STARTTIME,ENDTIME,\n REGIONID,CUSTOM,\n CAMERAMOUNTINGSTATUSFILES,MOUNTINGSTATUS,\n DVRENABLED_FLAG,EDVRENABLED_FLAG,\n VIOLATION_JSON,EXTERNAL_JSON , SCORE , DIVISION, TRIPDATAUPLOADED_FLAG, \n\t\t SAMPLEDRIVERIMAGE, SAMPLEDRIVERIMAGEFACECOORDINATES,FRPERSONSLIST,\n\t\t DOCUPDATEDAT,DOCCREATEDAT,\n\t\t HASDRIVERCAMERA_FLAG,RECORDEDINFO_JSON,ALWAYSONLINEENABLED_FLAG,\n\t\t ISSURVEILLANCETRIP_FLAG, REFERENCETRIPID, SDK\n )\n SELECT \n p_trip_jsonb->>'endpointVersion' ,v_fleetId,TRIM(p_trip_jsonb->>'driverId'),p_trip_jsonb->>'tripId',p_client_id,\n p_trip_jsonb->'device',p_trip_jsonb->'asset',COALESCE(p_trip_jsonb->>'driverName', 'None'),TRIM(p_trip_jsonb->'asset'->>'assetId'),\n COALESCE(CONVERT_BOOLEAN(p_trip_jsonb->>'ongoing'),TRUE) ,p_trip_jsonb->>'ignitionId',CONVERT_SMALLINT(p_trip_jsonb->>'ignitionTripIndex'),\n p_trip_jsonb->>'timeZoneId', CONVERT_INTEGER(p_trip_jsonb->>'timezoneOffset') ,\n v_tripdistance ,v_tripduration,\n COALESCE(CONVERT_BOOLEAN(p_trip_jsonb->>'driverAssigned'),FALSE), COALESCE(CONVERT_BOOLEAN(p_trip_jsonb->>'didStartTripAutomatically'),FALSE) , COALESCE(CONVERT_BOOLEAN(p_trip_jsonb->>'dvrConsent'),FALSE),\n COALESCE(CONVERT_BOOLEAN(p_trip_jsonb->>'edvrConsent'),FALSE), \n COALESCE(p_trip_jsonb->'firstLocation','{}'::JSONB), p_trip_jsonb->'lastLocation', p_trip_jsonb->'lastKnownLocation',\n\t\t p_trip_jsonb->>'cameraSerialId',\n COALESCE(CONVERT_TIMESTAMP(p_trip_jsonb->>'statusUpdateTimestamp'), date_utc_to_localX((now() at time zone 'utc'),v_timezoneoffset)), COALESCE(CONVERT_BOOLEAN(p_trip_jsonb->>'multiStreamEnabled'),FALSE),\n v_startTimeUTC,v_endTimeUTC , \n v_starttime, v_endtime,\n COALESCE(CONVERT_INTEGER(p_trip_jsonb->'common'->>'regionId'),CONVERT_INTEGER(p_trip_jsonb->>'regionId'),0), NULL, \n p_trip_jsonb->'cameraMountingStatusFiles',p_trip_jsonb->'mountingStatus',\n COALESCE(CONVERT_BOOLEAN(p_trip_jsonb->>'dvrEnabled'),FALSE), \n\t\t COALESCE(COALESCE(CONVERT_BOOLEAN(p_trip_jsonb->>'edvrenabled'), CONVERT_BOOLEAN(p_trip_jsonb->>'edvrConsent') AND CASE WHEN POSITION('edvr' IN LOWER(p_trip_jsonb->'asset'->>'packages')) >0 THEN TRUE ELSE FALSE END),FALSE),\n v_violation_jsonb,v_external_jsonb,GET_VIOLATION_SCORE(v_violation_jsonb,v_tripdistance) ,COALESCE(p_trip_jsonb->>'division' ,'_UNIDENTIFIED'),\n\t\t COALESCE((CASE WHEN (p_trip_jsonb->'webhookTrigger'->>0 IS NOT NULL) THEN p_trip_jsonb->>'webhookTrigger' LIKE TRIM('%TRIP_DATA_UPLOADED%' ) ELSE FALSE END),FALSE) ,\n\t\t p_trip_jsonb->>'sampleDriverImage', COALESCE(p_trip_jsonb->'sampleDriverImageFaceCoordinates','{}'::JSONB),p_trip_jsonb->'frPersonsList',\n\t\t COALESCE(CONVERT_TIMESTAMP(p_trip_jsonb->>'docUpdatedAt'),NOW() at time zone 'utc'),CONVERT_TIMESTAMP(p_trip_jsonb->>'docCreatedAt'),\n\t\t CONVERT_BOOLEAN(p_trip_jsonb->>'hasDriverCamera'),p_trip_jsonb->'recordedInfo',CONVERT_BOOLEAN(p_trip_jsonb->>'isAlwaysOnlineEnabled'),\n\t\t COALESCE(CONVERT_BOOLEAN(p_trip_jsonb->>'isSurveillanceTrip'),FALSE), p_trip_jsonb->>'referenceTripId', p_trip_jsonb->'sdk'\"\nPL/pgSQL function trip.t_trip_create(character varying,jsonb,jsonb,jsonb) line 88 at SQL statement\nSQL statement \"SELECT TRIP.T_TRIP_CREATE(p_clientid,p_trip_jsonb,NULL,NULL)\"\nPL/pgSQL function trip.t_staging_trip(character varying,jsonb) line 33 at SQL statement\nSQL statement \"SELECT TRIP.T_STAGING_TRIP(p_clientid, p_jsonb)\"\nPL/pgSQL function staging.process_trip_warehouse(character varying,integer,jsonb) line 9 at SQL statement\nSQL statement \"SELECT staging.process_trip_warehouse(p_clientid,p_batch,p_jsonb)\"\nPL/pgSQL function staging.process_trip(character varying,boolean,integer,jsonb) line 63 at PERFORM\nSQL statement \"SELECT STAGING.PROCESS_TRIP(p_clientid,v_warehouseenabled,p_batch,p_jsonb)\"\nPL/pgSQL function process_staging(character varying,character varying,integer,jsonb,text) line 75 at SQL statement\nSQL statement \"SELECT STAGING.PROCESS_STAGING(p_clientid,p_database,p_batch,(i-'seq_no'), i->>'seq_no')\"\nPL/pgSQL function process_stagingx(character varying,character varying,integer,jsonb) line 15 at SQL statement", "message: ": "numeric field overflow", "sqlstate: ": "22003"}
```





```
fleetdriver.f_bulk_update_driver_post_trip
fleetdriver.f_preview_update_driver_bulk_trips
fleetdriver.f_list_update_driver_requests
```





```sql

CREATE TABLE IF NOT EXISTS fleetdriver.update_trip_driver_request
(
    id SERIAL PRIMARY KEY,
    clientid character varying COLLATE pg_catalog."default" NOT NULL,
    fleetid character varying COLLATE pg_catalog."default" NOT NULL,
    olddriverid character varying COLLATE pg_catalog."default" NOT NULL,
    newdriverid character varying COLLATE pg_catalog."default" NOT NULL,
    status character varying COLLATE pg_catalog."default" NOT NULL,
    createdate timestamp without time zone NOT NULL DEFAULT timezone('utc'::text, now()),
    request_payload jsonb NOT NULL,
    result jsonb
	
)
TABLESPACE pg_default;

COMMENT ON TABLE fleetdriver.update_trip_driver_request
    IS 'Bulk or single post trip driver updates';
```



admin.grant_privileges_to_client_user

```sql
	EXECUTE format('GRANT SELECT, INSERT, UPDATE ON TABLE FLEETDRIVER.UPDATE_TRIP_DRIVER_REQUEST TO %1$s', v_client_user);

```

