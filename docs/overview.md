# Miesh Integrations

<!-- tabs:start -->

## **Scenario 01**
## Scenario 01

Simple PerPersonal import and export processes with a single data type.

In this scenario, the records are imported into a data-type and then when the export process is executed, it reads the 
records of the same data-type, prepares and sends the file to the cloud.

### Import PerPersonal from SAP-SF

1. Create or use the [authorization](authorizations/sap-success-factors.md) 
2. Create or use the [connection](connections/sap-success-factors.md)
3. Create or use the [webhook](webhooks/sap-success-factors-get-perpersonal.md)
4. Create or use the [data-type](data-types/SAPSuccessFactors-PerPersonal.md)
5. Create or use the parser [translator](translators/parse_from_sapsf_api_response_to_sapsf_perpersonal.md)
6. Create or use the setup algorithm [before submit](algorithms/sapsf-setup_import_before_submit.md)
7. Create or use the pagination algorithm [after callback](algorithms/sapsf-setup_import_next_page_after_callback.md)
8. Create or use the [flow](flows/sapsf-do_import_from_sapsf_perpersonal.md)

### Export PerPersonal records to SFTPStore

1. Create or use the [authorization](authorizations/sftp-store.md) 
2. Create or use the [connection](connections/sftp-store.md)
3. Create or use the [webhook](webhooks/sftp-store-upload-file.md)
4. Create or use the template [translator](translators/parse_from_sapsf_perpersonal_to_sftp_server_uplaod_request.md)
5. Create or use the [encrypt](algorithms/miesh-encrypt.md) algorithm
6. Create or use the [flow](flows/sapsf-do_export_to_sftpstore_perpersonal.md)

## **Scenario 02**
## Scenario 02

Import all PerPersonal records into a data-type, consolidate them into a single record immediately upon completion of the import, 
and finally export them to a file in the cloud upon completion of the consolidated record.

In this scenario, an after-callback algorithm is used to start the conversion flow and an event after_create to start the export flow.

### Import PerPersonal from SAP-SF

1. Create or use the [authorization](authorizations/sap-success-factors.md) 
2. Create or use the [connection](connections/sap-success-factors.md)
3. Create or use the [webhook](webhooks/sap-success-factors-get-perpersonal.md)
4. Create or use the [data-type](data-types/SAPSuccessFactors-PerPersonal.md)
5. Create or use the parser [translator](translators/parse_from_sapsf_api_response_to_sapsf_perpersonal.md)
6. Create or use the setup algorithm [before submit](algorithms/sapsf-setup_import_before_submit.md)
7. Create or use the pagination algorithm [after callback](algorithms/sapsf-setup_import_next_page_after_callback.md)
8. Create or use the conversion algorithm [after callback](algorithms/sapsf-convert_import_perpersonal_after_callback.md)
9. Create or use the [flow](flows/sapsf-do_import_from_sapsf_perpersonal.md)

### Convert PerPersonal records to a single consolidated record

1. Create or use the [data-type](data-types/SFTPStore-PerPersonal.md)
2. Create or use the converter [translator](translators/parse_from_sapsf_perpersonal_to_sftp_server_uplaod_request.md)
3. Create or use the after-create [data-event](observers/SFTPStore-PerPersonal-throw_after_creating.md)
4. Create or use the [flow](flows/sftpstore-do_convert_from_sapsf_perpersonal.md)

### Export consolidated PerPersonal record to SFTPStore

1. Create or use the [authorization](authorizations/sftp-store.md) 
2. Create or use the [connection](connections/sftp-store.md)
3. Create or use the [webhook](webhooks/sftp-store-upload-file.md)
4. Create or use the template [translator](translators/parse_from_sftpstore_perpersonal_to_sftpstore_uplaod_request.md)
5. Create or use the [encrypt](algorithms/miesh-encrypt.md) algorithm
6. Create or use the [flow](flows/sftpstore-do_export_to_sftp_server_perpersonal.md)

## **Scenario 03**
## Scenario 03

Import encrypted PerPersonal data from a SFTP-Server, decrypt and save in SFTPStore:PerPersonal data-type.
Apply a conversion flow to extract the imported data and store it in separate records in SAPSuccessFactors: PerPersonal data-type.
Make some modifications to some records of the SAPSuccessFactors:PerPersonal data-type and re-export them.

### Import PerPersonal data from SFTP-Server

1. Create or use the [authorization](authorizations/sftp-store.md) 
2. Create or use the [connection](connections/sftp-store.md)
3. Create or use the [webhook](webhooks/sftp-store-download-file.md)
4. Create or use the [data-type](data-types/SFTPStore-PerPersonal.md)
5. Create or use the parser [translator](translators/parse_from_sftp_server_download_response_to_sftpstore_perpersonal.md)
6. Create or use the setup algorithm [before submit](algorithms/sftpstore-setup_import_before_submit.md)
9. Create or use the [flow](flows/sftpstore-do_import_from_sftp_server_perpersonal.md)

### Convert PerPersonal consolidated record to multiples records

1. Create or use the [data-type](data-types/SAPSuccessFactors-PerPersonal.md)
2. Create or use the converter [translator](translators/)
3. Create or use the after-update [data-event](observers/)
4. Create or use the [flow](flows/)

### Re-Export PerPersonal records to SFTPStore

1. Update some records of the SAPSuccessFactors:PerPersonal data-type
2. Apply the flow to Convert PerPersonal records to a single consolidated record described in *Scenario 02*.
3. Apply the flow to Export consolidated PerPersonal record to SFTPStore described in *Scenario 02*

<!-- tabs:end -->

<hr />

> For more details see also [CenitIO documentation](https://cenit-io.github.io/docs)