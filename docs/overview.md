# Miesh Integrations

<!-- tabs:start -->

#### **Scenario 01**

Simple PerPersonal import and export processes with a single data type.

In this scenario, the records are imported into a data-type and then when the export process is executed, it reads the 
records of the same data-type, prepares and sends the file to the cloud.

## Import PerPersonal from SAP-SF

1. Create the [authorization](authorizations/sap-success-factors.md) 
2. Create the [connection](connections/sap-success-factors.md)
3. Create the [webhook](webhooks/sap-success-factors-get-perpersonal.md)
4. Create the [data-type](data-types/SAPSuccessFactors-PerPersonal.md)
5. Create the parser [translator](translators/parse_from_sapsf_api_response_to_sapsf_perpersonal.md)
6. Create the setup algorithm [before submit](algorithms/sapsf-setup_import_before_submit.md)
7. Create the pagination algorithm [after callback](algorithms/sapsf-setup_import_next_page_after_callback.md)
8. Create the [flow](flows/sapsf-do_import_from_sapsf_perpersonal.md)

## Export PerPersonal records to SFTPStore

1. Create the [authorization](authorizations/sftp-store.md) 
2. Create the [connection](connections/sftp-store.md)
3. Create the [webhook](webhooks/sftp-store-upload-file.md)
4. Create the template [translator](translators/parse_from_sapsf_perpersonal_to_sftpstore_uplaod_request.md)
5. Create the [encrypt](algorithms/miesh-encrypt.md) algorithm
6. Create the [flow](flows/sapsf-do_export_to_sftpstore_perpersonal.md)

#### **Scenario 02**

Import all PerPersonal records into a data-type, consolidate them into a single record immediately upon completion of the import, 
and finally export them to a file in the cloud upon completion of the consolidated record.

In this scenario, an after-callback algorithm is used to start the conversion flow and an event after_create to start the export flow.

## Import PerPersonal from SAP-SF

1. Create the [authorization](authorizations/sap-success-factors.md) 
2. Create the [connection](connections/sap-success-factors.md)
3. Create the [webhook](webhooks/sap-success-factors-get-perpersonal.md)
4. Create the [data-type](data-types/SAPSuccessFactors-PerPersonal.md)
5. Create the parser [translator](translators/parse_from_sapsf_api_response_to_sapsf_perpersonal.md)
6. Create the setup algorithm [before submit](algorithms/sapsf-setup_import_before_submit.md)
7. Create the pagination algorithm [after callback](algorithms/sapsf-setup_import_next_page_after_callback.md)
8. Create the conversion algorithm [after callback](algorithms/sapsf-convert_import_perpersonal_after_callback.md)
9. Create the [flow](flows/sapsf-do_import_from_sapsf_perpersonal.md)

## Convert PerPersonal records to a single consolidated record

1. Create the [data-type](data-types/SFTPStore-PerPersonal.md)
2. Create the converter [translator](translators/parse_from_sapsf_perpersonal_to_sftpstore_uplaod_request.md)
3. Create the after-create [data-event](observers/SFTPStore-PerPersonal-throw_after_creating.md)
4. Create the [flow](flows/sftpstore-do_convert_from_sapsf_perpersonal.md)

## Export consolidated PerPersonal record to SFTPStore

1. Create the [authorization](authorizations/sftp-store.md) 
2. Create the [connection](connections/sftp-store.md)
3. Create the [webhook](webhooks/sftp-store-upload-file.md)
4. Create the template [translator](translators/parse_from_sapsf_perpersonal_to_sftpstore_uplaod_request.md)
5. Create the [encrypt](algorithms/miesh-encrypt.md) algorithm
6. Create the [flow](flows/sftpstore-do_export_to_sftpstore_perpersonal.md)

<!-- tabs:end -->

<hr />

> For more details see also [CenitIO documentation](https://cenit-io.github.io/docs)