```plsql
CREATE OR REPLACE FUNCTION link_entity_attribute (
	p_clientid character varying,
	p_inputjsonb jsonb
) RETURNS jsonb
    LANGUAGE 'plpgsql'
    COST 100
    VOLATILE PARALLEL UNSAFE
AS $BODY$
DECLARE
	v_returnjsonb jsonb;
	v_fleetId character varying;

BEGIN
END;
$BODY$;
```